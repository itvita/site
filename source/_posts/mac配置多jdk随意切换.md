---
title: mac配置多jdk随意切换
categories:
  - java
tags:
  - mac
  - jdk
mp3: http://np01.sycdn.kuwo.cn/12d1b29abe3f8f5a3848e9d2c84d5001/63834f20/resource/n2/5/55/3065754672.mp3
cover: /img/1.jpg
date: 2022-11-20 17:51:35
---

# 下载安装
[JDK6](https://support.apple.com/kb/DL1572?locale=zh_CN)
[JDK7]()
[JDK8]()
# 配置环境变量
```sh
open .bash_profile

export PATH=$PATH:/usr/local/apache-tomcat-7.0.79/bin
export JAVA_6_HOME=/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
export JAVA_7_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home
```

# 设置默认的jdk版本
```sh
export JAVA_HOME=$JAVA_8_HOME 
```

# 设置alias 用于切换
```sh
alias jdk8='export JAVA_HOME=$JAVA_8_HOME'
alias jdk7='export JAVA_HOME=$JAVA_7_HOME'
alias jdk6='export JAVA_HOME=$JAVA_6_HOME'
```

# 保存退出后刷新配置
```sh
source .bash_profile
```

# 切换jdk
```sh
命令行输入jdk6，再输入java -version 查看当前版本即可实现动态切换，jdk7，jdk8同样。
```
