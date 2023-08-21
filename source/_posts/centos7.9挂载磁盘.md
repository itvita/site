---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: centos7.9挂载磁盘
categories:
  - linux
tags:
  - centos
date: 2023-03-31 14:47:33
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [查看磁盘信息](#查看磁盘信息)
2. [以 root 用户执行以下命令，查看磁盘名称。](#以-root-用户执行以下命令查看磁盘名称)
3. [对 “/dev/vdb” 裸设备直接创建文件系统格式。](#对-devvdb-裸设备直接创建文件系统格式)
4. [新建挂载点。](#新建挂载点)
5. [5.将新建分区挂载至新建的挂载点。](#5将新建分区挂载至新建的挂载点)
6. [加入到磁盘信息](#加入到磁盘信息)
7. [查看磁盘信息](#查看磁盘信息-1)

<!-- /code_chunk_output -->

## 查看磁盘信息
```shell
df -h
```

## 以 root 用户执行以下命令，查看磁盘名称。
```shell
fdisk -l
```
![](/img/20230331144844.png)

>可以看到 /dev/vda 为系统盘，/dev/vdb 为数据盘，

## 对 “/dev/vdb” 裸设备直接创建文件系统格式。
```shell
mkfs -t ext4 /dev/vdb
```
## 新建挂载点。
```shell
mkdir /data
```
## 5.将新建分区挂载至新建的挂载点。
```shell
mount /dev/vdb /data
```

## 加入到磁盘信息
```shell
vim /etc/fstab
# 新增
/dev/vdb /data ext4 defaults 0 0
```

## 查看磁盘信息
```shell
df -h
```