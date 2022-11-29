---
title: springboot服务调优
categories:
  - springboot
tags:
  - springboot
  - tomcat
mp3: /music/放学后的音乐教室.m4a
cover: /img/003527-165738452757b4.jpg
date: 2022-10-09 19:44:53
---
> tomcat常用配置

```
## 等待队列长度，默认100。
server.tomcat.accept-count=1000
## 最大工作线程数，默认200。（4核8g内存，线程数经验值800，操作系统做线程之间的切换调度是有系统开销的，所以不是越多越好。）
server.tomcat.max-threads=800
## 最小工作空闲线程数，默认10。（适当增大一些，以便应对突然增长的访问量）
server.tomcat.min-spare-threads=100
```

> 修改长链接keepAlive相关配置，保证路由策略的性能高效。

```
/**
 * 当Spring容器内没有TomcatEmbeddedServletContainerFactory这个bean时，会把此bean加载金spring容器中
 */
@Component
public class WebServerConfiguration implements WebServerFactoryCustomizer<ConfigurableWebServerFactory>{
    @Override
    public void customize(ConfigurableWebServerFactory factory) {
        // 使用对应工厂类提供给我们的接口定制化我们的tomcat connector
        ((TomcatServletWebServerFactory) factory).addConnectorCustomizers(new TomcatConnectorCustomizer() {
            @Override
            public void customize(Connector connector) {
                Http11AprProtocol protocol = (Http11AprProtocol) connector.getProtocolHandler();
                // 定制化keepAliveTimeout，设置30秒内没有请求则服务端自动断开keepalive链接
                protocol.setKeepAliveTimeout(300000);
                // 当客户端发送超过10000个请求则自动断开keepalive链接
                protocol.setMaxKeepAliveRequests(10000);
            }
        });
    }
}
```

