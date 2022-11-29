---
title: centos7配置maven
categories:
  - linux
tags:
  - centos
  - maven
mp3: /music/分手在那个秋天-浩瀚.mp3
cover: /img/4k123123.jpg
date: 2022-11-23 11:55:41
---

### 下载
```
wget https://dlcdn.apache.org/maven/maven-3/3.8.2/binaries/apache-maven-3.8.2-bin.tar.gz
```

### 解压
```
tar -zxvf apache-maven-3.8.2-bin.tar.gz
```

### 配置环境变量

```
vim /etc/profile

export MAVEN_HOME=/opt/apache-maven-3.8.2
export PATH=$PATH:$MAVEN_HOME/bin
```

### 刷新配置
```
source /etc/profile
```