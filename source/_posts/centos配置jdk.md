---
title: centos配置jdk
categories:
  - linux
tags:
  - centos
  - jdk
mp3: /music/光辉岁月.mp3
cover: /img/pexels-gabriel-hohol-3593923.jpg
date: 2022-11-29 11:41:40
---
# 下载
[jdk8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

# 解压
```
tar -zxvf  jdk-8u271-linux-x64.tar.gz.tar.gz
```

# 配置环境变量
```
#vim /etc/profile -- 所有用户生效
#vim ~/.bash_profile --当前用户生效
JAVA_HOME=/opt/jdk1.8.0_271 
JRE_HOME=/opt/jdk1.8.0_271/jre 
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib 
PATH=$JAVA_HOME/bin:$PATH 
export PATH JAVA_HOME CLASSPATH
```

# 刷新
```
source  /etc/profile
```