---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: centos7.9升级cmake
categories:
  - linux
tags:
  - centos
date: 2023-03-29 11:13:45
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [查看当前版本](#查看当前版本)
2. [卸载](#卸载)
3. [下载高版本安装包](#下载高版本安装包)
4. [安装环境依赖](#安装环境依赖)
5. [编译链接](#编译链接)
6. [安装](#安装)
7. [创建链接](#创建链接)
8. [查看版本](#查看版本)

<!-- /code_chunk_output -->


**在centos7 yum源中和系统自带的cmake版本为2.8.12.2；在编译某些文件的时候会提醒cmake版本过低，本文旨在解决cmake的更新问题**

> cmake官网：https://cmake.org/
cmake下载：https://cmake.org/files/

## 查看当前版本
   ```
   cmake -version
   ```
## 卸载
```
yum remove -y cmake
```
## 下载高版本安装包
```
mkdir /opt/cmake
cd /opt/cmake
wget https://cmake.org/files/v3.16/cmake-3.16.6.tar.gz
tar -zxvf cmake-3.16.6.tar.gz
```

## 安装环境依赖
```
yum install -y gcc gcc-c++
yum install openssl-devel
```

## 编译链接
```
./configure --prefix=/data/cmake
```

## 安装
```
make && make install
```

## 创建链接
```
ln -s /data/cmake/bin/cmake /usr/bin/cmake
```
或者修改环境变量
```
vim /etc/profile 
export CMAKE_HOME=/data/cmake 
export PATH=$PATH:$CMAKE_HOME/bin
```
## 查看版本
```
cmake -version
```
