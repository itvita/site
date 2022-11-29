---
title: springboot动态数据源
categories:
  - springboot
tags:
  - springboot
mp3: /music/mysoul.m4a
cover: /img/152125-1656746485a706.jpg
date: 2022-11-29 18:16:18
---
### 目的

- 多数据源
- 通过注解切换数据源
- 通过传入参数动态切换数据源
- 可自定义切点等。。。

### 项目结构
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202201131055782.png)

### 代码
#### 数据源配置参数
```yml
dynamic:
  datasource:
    master:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/db_iv?useUnicode=true&characterEncoding=utf8&useSSL=true&serverTimezone=Asia/Shanghai
      username: root
      password: itvita2021
    slave1:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/db_iv1?useUnicode=true&characterEncoding=utf8&useSSL=true&serverTimezone=Asia/Shanghai
      username: root
      password: itvita2021
```

#### 数据源KEY定义
```java
package cn.itvita.system.config.datasource.commons;

// @formatter:off
/**       猪猪保佑 永无bug
 *  _._ _..._ .-',     _.._(`))
 * '-. `     '  /-._.-'    ',/
 *    )         \            '.
 *   / _    _    |             \
 *  |  a    a    /              |
 *  \   .-.                     ;
 *   '-('' ).-'       ,'       ;
 *      '-;           |      .'
 *         \           \    /
 *         | 7  .__  _.-\   \
 *         | |  |  ``/  /`  /
 *        /,_|  |   /,_/   /
 *           /,_/      '`-'
 *
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:39
 * @Description : 定义默认的数据源key
 */
// @formatter:on
public class DSK {
    public final static String DB_MASTER = "DB_MASTER";
    public final static String DB_SLAVE1 = "DB_SLAVE1";
}

```
#### 系统数据源配置

```JAVA
package cn.itvita.system.config.datasource.configuration;

import cn.itvita.system.config.datasource.commons.DSK;
import cn.itvita.system.config.datasource.commons.DynamicRoutingDataSource;
import com.alibaba.druid.pool.DruidDataSource;
import com.baomidou.mybatisplus.core.MybatisConfiguration;
import com.baomidou.mybatisplus.core.MybatisXMLLanguageDriver;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.type.JdbcType;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.SqlSessionTemplate;
import org.mybatis.spring.transaction.SpringManagedTransactionFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.PlatformTransactionManager;

import javax.sql.DataSource;
import java.util.HashMap;
import java.util.Map;

/**
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:46
 * @Description :系统数据源配置
 */
@Configuration
public class DynamicDataSourceConfiguration {

    @Value("${mybatis-plus.mapper-locations}")
    private String mapperLocations;

    @Value("${mybatis-plus.type-aliases-package}")
    private String typeAliasesPackage;

    /**
     * 主数据源配置
     */
    @Value("${dynamic.datasource.master.driver-class-name}")
    private String masterDriverClassName;
    @Value("${dynamic.datasource.master.url}")
    private String masterUrl;
    @Value("${dynamic.datasource.master.username}")
    private String masterUsername;
    @Value("${dynamic.datasource.master.password}")
    private String masterPassword;

    /**
     * 数据源1
     */
    @Value("${dynamic.datasource.slave1.driver-class-name}")
    private String slave1DriverClassName;
    @Value("${dynamic.datasource.slave1.url}")
    private String slave1Url;
    @Value("${dynamic.datasource.slave1.username}")
    private String slave1Username;
    @Value("${dynamic.datasource.slave1.password}")
    private String slave1Password;

    /**
     * 创建数据源对象
     *
     * @return data source
     */
    @Primary
    @Bean
    public DataSource dbMaster() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(masterDriverClassName);
        dataSource.setUrl(masterUrl);
        dataSource.setUsername(masterUsername);
        dataSource.setPassword(masterPassword);
        return dataSource;
    }

    @Bean
    public DataSource dbSlave1() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(slave1DriverClassName);
        dataSource.setUrl(slave1Url);
        dataSource.setUsername(slave1Username);
        dataSource.setPassword(slave1Password);
        return dataSource;
    }


    /**
     * @return 数据源实例
     * @Author : liu.q [916000612@qq.com]
     * @Date : 2019-03-27 22:44
     * 核心动态数据源 数据源整合
     */
    @Bean
    public DataSource dynamicDataSource() {
        DynamicRoutingDataSource dataSource = new DynamicRoutingDataSource();
        dataSource.setDefaultTargetDataSource(dbMaster());
        Map<Object, Object> dataSourceMap = new HashMap<>(4);
        dataSourceMap.put(DSK.DB_MASTER, dbMaster());
        dataSourceMap.put(DSK.DB_SLAVE1, dbSlave1());
        dataSource.setTargetDataSources(dataSourceMap);
        return dataSource;
    }

    @Bean
    public SqlSessionFactory sqlSessionFactory() throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dynamicDataSource());

        sqlSessionFactoryBean.setTypeAliasesPackage(typeAliasesPackage);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));

        MybatisConfiguration configuration = new MybatisConfiguration();
        configuration.setDefaultScriptingLanguage(MybatisXMLLanguageDriver.class);
        configuration.setJdbcTypeForNull(JdbcType.NULL);
        sqlSessionFactoryBean.setConfiguration(configuration);

        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }

    @Bean
    public SqlSessionTemplate sqlSessionTemplate() throws Exception {
        return new SqlSessionTemplate(sqlSessionFactory());
    }

    /**
     * 事务管理
     *
     * @return 事务管理实例
     */
    @Bean
    public PlatformTransactionManager platformTransactionManager() {
        return new DataSourceTransactionManager(dynamicDataSource());
    }

}

```
#### 数据源操作类
```java
package cn.itvita.system.config.datasource.commons;

import lombok.extern.slf4j.Slf4j;
// @formatter:off
/**       猪猪保佑 永无bug
 *  _._ _..._ .-',     _.._(`))
 * '-. `     '  /-._.-'    ',/
 *    )         \            '.
 *   / _    _    |             \
 *  |  a    a    /              |
 *  \   .-.                     ;
 *   '-('' ).-'       ,'       ;
 *      '-;           |      .'
 *         \           \    /
 *         | 7  .__  _.-\   \
 *         | |  |  ``/  /`  /
 *        /,_|  |   /,_/   /
 *           /,_/      '`-'
 *
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:43
 * @Description : 数据源操作类
 */
// @formatter:on
@Slf4j
public class DynamicDataSourceContextHolder {

    private static final ThreadLocal<String> currentDataSource = new ThreadLocal<>();

    /**
     * 清除当前数据源
     */
    public static void clear() {
        currentDataSource.remove();
    }

    /**
     * 获取当前使用的数据源
     *
     * @return 当前使用数据源的ID
     */
    public static String get() {
        return currentDataSource.get();
    }

    /**
     * 设置当前使用的数据源
     *
     * @param value 需要设置的数据源ID
     */
    public static void set(String value) {
        currentDataSource.set(value);
    }
}

```
#### 动态数据源切换
```java
package cn.itvita.system.config.datasource.commons;

import lombok.extern.slf4j.Slf4j;
import org.springframework.jdbc.datasource.lookup.AbstractRoutingDataSource;

import javax.sql.DataSource;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
// @formatter:off
/**       猪猪保佑 永无bug
 *  _._ _..._ .-',     _.._(`))
 * '-. `     '  /-._.-'    ',/
 *    )         \            '.
 *   / _    _    |             \
 *  |  a    a    /              |
 *  \   .-.                     ;
 *   '-('' ).-'       ,'       ;
 *      '-;           |      .'
 *         \           \    /
 *         | 7  .__  _.-\   \
 *         | |  |  ``/  /`  /
 *        /,_|  |   /,_/   /
 *           /,_/      '`-'
 *
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:43
 * @Description : 动态数据源切换
 */
// @formatter:on
@Slf4j
public class DynamicRoutingDataSource extends AbstractRoutingDataSource {


    //预备一份用于存储targetDataSource
    private ConcurrentHashMap<String, DataSource> backupTargetDataSources = new ConcurrentHashMap<>();

    @Override
    protected Object determineCurrentLookupKey() {
        String k = DynamicDataSourceContextHolder.get();
        if(null == k){ // 如果当前未设置数据源，系统会使用默认的数据源
            k = DSK.DB_MASTER;
            log.info("当前数据源为null,使用默认数据源{" + k + "}");
        }else{
            log.info("当前数据源{" + k + "}");
        }
        return DynamicDataSourceContextHolder.get();
    }

    public void addDataSourceToTargetDataSource(String key, DataSource ds) {
        this.backupTargetDataSources.put(key, ds);
        this.setTargetDataSource(this.backupTargetDataSources);
        DynamicDataSourceContextHolder.set(key);
    }

    public void setTargetDataSource(Map targetDataSource) {
        super.setTargetDataSources(targetDataSource);
        this.afterPropertiesSet();
    }
}

```
#### 自定义注解
```java
package cn.itvita.system.config.datasource.annotation;


import cn.itvita.system.config.datasource.commons.DSK;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
// @formatter:off
/**       猪猪保佑 永无bug
 *  _._ _..._ .-',     _.._(`))
 * '-. `     '  /-._.-'    ',/
 *    )         \            '.
 *   / _    _    |             \
 *  |  a    a    /              |
 *  \   .-.                     ;
 *   '-('' ).-'       ,'       ;
 *      '-;           |      .'
 *         \           \    /
 *         | 7  .__  _.-\   \
 *         | |  |  ``/  /`  /
 *        /,_|  |   /,_/   /
 *           /,_/      '`-'
 *
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:39
 * @Description : 数据源切换注解
 */
// @formatter:on
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface DS {
    String value() default DSK.DB_MASTER;
}

```

#### 动态切入数据源
```java
package cn.itvita.system.config.datasource.commons;

import cn.itvita.system.config.datasource.annotation.DS;
import cn.itvita.system.config.datasource.annotation.DS;
import lombok.extern.slf4j.Slf4j;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.aspectj.lang.reflect.MethodSignature;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import java.lang.reflect.Method;
// @formatter:off

/**
 * 猪猪保佑 永无bug
 * _._ _..._ .-',     _.._(`))
 * '-. `     '  /-._.-'    ',/
 * )         \            '.
 * / _    _    |             \
 * |  a    a    /              |
 * \   .-.                     ;
 * '-('' ).-'       ,'       ;
 * '-;           |      .'
 * \           \    /
 * | 7  .__  _.-\   \
 * | |  |  ``/  /`  /
 * /,_|  |   /,_/   /
 * /,_/      '`-'
 *
 * @Author : liu.q [916000612@qq.com]
 * @Date : 2019-03-27 22:40
 * @Description : 动态切入数据源
 */
// @formatter:on
@Aspect
@Order(-1)
@Component
@Slf4j
public class DynamicDataSourceAspect {

    /**
     * @param joinPoint 切点
     * @param ds        动态数据源
     * @Author : liu.q [916000612@qq.com]
     * @Date : 2019-03-27 22:40
     * @Description :执行方法前更换数据源
     */
    @Before("@annotation(ds)")
    public void doBefore(JoinPoint joinPoint, DS ds) {
        String dataSourceKey = ds.value();
        log.info(String.format("设置数据源为  %s", dataSourceKey));
        DynamicDataSourceContextHolder.set(dataSourceKey);
    }

    /**
     * @param joinPoint 切点
     * @param ds        动态数据源
     * @Author : liu.q [916000612@qq.com]
     * @Date : 2019-03-27 22:41
     * @Description :执行方法后清除数据源设置
     */
    @After("@annotation(ds)")
    public void doAfter(JoinPoint joinPoint, DS ds) {
        log.info(String.format("当前数据源  %s  执行清理方法", ds.value()));
        DynamicDataSourceContextHolder.clear();
    }
}

```

#### 使用
```java
  @ApiOperation("查询用户列表")
    @GetMapping("/getList")
    @ApiImplicitParams({
            @ApiImplicitParam(name = "year", value = "年份", required = true, paramType = "query")
    })
    @DS(DSK.DB_SLAVE1)  //通过注解设置数据源，不设置默认 主数据源
    public ReturnVo<PageBean<SysUser>> getList(Paging paging, String year) {
//        if ("2021".equals(year)) {  //通过传入参数动态设置数据源。
//            DynamicDataSourceContextHolder.set(DSK.DB_SLAVE1);
//        }
        PageUtil.Paging(paging, "created_time desc");
        QueryWrapper<SysUser> wrapper = new QueryWrapper();
        System.out.println(sysUserService.getByMap(new HashMap()));
        return new ReturnVo(new PageBean(sysUserService.list(wrapper)));
    }
```
