---
title: centos安装redis
categories:
  - linux
tags:
  - centos
  - redis
date: 2022-11-19 11:26:32
mp3: /music/Your Open Eyes-Xeuphoria.mp3
cover: /img/d1f7620ea8f039e4f606788715251212.jpg
---

# 1、redis最新版下载地址

[redis官网](https://redis.io/download)

[GitHub](https://github.com/redis/redis)

# 2、下载

```
wget https://download.redis.io/releases/redis-6.0.9.tar.gz
```

# 3、解压并进入目录

```
tar -zxvf redis-6.0.9.tar.gz
cd redis-6.0.9
```

# 4、编译安装

```
make && make install
```

# 5、移动脚本&配置文件

> 把redis-6.0.9/src目录下的mkreleasehdr.sh，redis-benchmark， redis-check-rdb， redis-cli， redis-server拷贝到redis-6.0.9/bin目录
>
> 并授予可执行权限 ，chmod + x *

# 6、修改redis.conf

```
#修改为守护模式
daemonize yes
#设置进程锁文件
pidfile /Users/liuqiang/tools/redis/redis_639.pid
#端口
port 6379
#客户端超时时间
timeout 300
#日志级别
loglevel debug
#日志文件位置
logfile /Users/liuqiang/tools/redis/log-redis.log
#设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id
databases 16
##指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合
#save <seconds> <changes>
#Redis默认配置文件中提供了三个条件：
save 900 1
save 300 10
save 60 10000
#指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，
#可以关闭该#选项，但会导致数据库文件变的巨大
rdbcompression yes
#指定本地数据库文件名
dbfilename dump.rdb
#指定本地数据库路径
dir /Users/liuqiang/tools/redis/db/
#指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能
#会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有
#的数据会在一段时间内只存在于内存中
appendonly no
#指定更新日志条件，共有3个可选值：
#no：表示等操作系统进行数据缓存同步到磁盘（快）
#always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全）
#everysec：表示每秒同步一次（折衷，默认值）
appendfsync everysec
#密码
requirepass 123456
```

# 7、启动

> 进入redis-6.0.9目录

```
./bin/redis-server ./redis.conf
```

# 8、停止

```
ps -ef|grep redis
kill -9 pid
```



# <font color="red">make[1]: *** [server.o] 错误 1</font>

*原因是因为gcc版本过低，yum安装的gcc是4.8.5的。因此需要升级gcc，升级过程如下*

```
yum -y install centos-release-scl

yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils

#这句是临时的
scl enable devtoolset-9 bash

#修改环境变量
echo "source /opt/rh/devtoolset-9/enable" >> /etc/profile

gcc -v
```

