---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: centos7.9yum安装mysql8
categories:
  - linux
tags:
  - centos
  - mysql
date: 2023-03-28 13:42:25
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [mariadb数据库卸载](#mariadb数据库卸载)
    1. [检查Linux是否安装了mariadb数据库](#检查linux是否安装了mariadb数据库)
    2. [卸载](#卸载)
2. [安装官方yum源](#安装官方yum源)
    1. [下载](#下载)
    2. [安装](#安装)
    3. [更新yum本地缓存](#更新yum本地缓存)
3. [安装mysql](#安装mysql)
4. [msyql初始化设置](#msyql初始化设置)
5. [修改密码](#修改密码)
6. [开启远程连接](#开启远程连接)

<!-- /code_chunk_output -->

## mariadb数据库卸载
### 检查Linux是否安装了mariadb数据库
> mariadb数据库是mysql的分支

```shell
#执行命令：
yum list installed | grep mariadb 
```
### 卸载
> 如果Linux中安装了mariadb数据库，先卸载掉，因为CentOS 7 内部集成了mariadb，而安装mysql的话会和mariadb的文件冲突，所以需要先卸载掉mariadb

```shell
#执行命令：
yum -y remove mariadb-libs.x86_64
```
## 安装官方yum源
### 下载
https://dev.mysql.com/downloads/repo/yum/
![](/img/20230328134602.png)
```
wget https://repo.mysql.com//mysql80-community-release-el7-7.noarch.rpm
```

### 安装
```
yum localinstall mysql80-community-release-el7-7.noarch.rpm -y
```

### 更新yum本地缓存
```
yum clean all
yum makecache
```

## 安装mysql
```
yum install mysql-community-server -y
```

## msyql初始化设置

```
# 设置开机启动
systemctl enable mysqld.service
# 启动
systemctl start mysqld.service
# 关闭
systemctl stop mysqld.service
# 重启
systemctl restart mysqld.service
# 查询运行
ps -ef | grep mysql
netstat -lntup | grep 3306
```

## 修改密码
```
# 查看默认密码
cat /var/log/mysqld.log | grep password

# 登录修改密码
mysql -uroot -p

# 重设密码
ALTER user 'root'@'localhost' IDENTIFIED BY '123456@Aa'

```

## 开启远程连接
```
use mysql;
select user, host from user;
update user set host = '%' where user = 'root';
flush privileges;
```

