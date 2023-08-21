---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: centos安装nodejs
categories:
  - linux
tags:
  - centos
  - nodejs
date: 2023-03-28 10:18:40
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [下载node.js](#下载nodejs)
2. [下载通过sftp上传到centos或者通过wget直接下载到服务器](#下载通过sftp上传到centos或者通过wget直接下载到服务器)
3. [解压](#解压)
4. [配置环境变量](#配置环境变量)

<!-- /code_chunk_output -->
## 下载node.js
https://nodejs.cn/download/

![](/img/20230328101928.png)

## 下载通过sftp上传到centos或者通过wget直接下载到服务器
```
wget https://nodejs.org/dist/v16.9.1/node-v16.9.1-linux-x64.tar.gz
```
## 解压
```
tar -zxvf xxxx.tar.gz
```
## 配置环境变量

```
# 打开配置文件
vim /etc/profile
 
# 添加配置
export NODE_HOME=/data/node-v16.9.1-linux-x64
export PATH=$NODE_HOME/bin:$PATH
 pwd
 
# 重新加载profile文件
source /etc/profile
```
