---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: docker命令
categories:
  - linux
tags:
  - docker
date: 2022-12-16 15:28:03
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [以nginx为例](#以nginx为例)
    1. [拉取镜像](#拉取镜像)
    2. [查看镜像](#查看镜像)
    3. [运行镜像](#运行镜像)
    4. [查看当前运行中应用](#查看当前运行中应用)
    5. [停止容器](#停止容器)
    6. [重启容器](#重启容器)
2. [安装并启动nacos 单机版](#安装并启动nacos-单机版)
3. [docker查看容器详细信息](#docker查看容器详细信息)

<!-- /code_chunk_output -->
## 以nginx为例
### 拉取镜像
```
docker pull nginx:latest
```

### 查看镜像
```
docker images
```

### 运行镜像
```
docker run --name nginx-test -p 8080:80 -d nginx
```
> 说明：
- **--name nginx-test：** 容器名称。
- **-p 8080:80：** 端口进行映射，将本地 8080 端口映射到容器内部的 80 端口。
- **-d nginx：** 设置容器在在后台一直运行。

### 查看当前运行中应用
```
docker ps
```
> 说明                  
- **CONTAINER ID：** 容器 ID
- **IMAGE：** 使用的镜像
- **COMMAND：** 启动容器时运行的命令
- **CREATED：** 容器的创建时间。
- **STATUS：** 容器状态
```
    created（已创建）
    restarting（重启中）
    running 或 Up（运行中）
    removing（迁移中）
    paused（暂停）
    exited（停止）
    dead（死亡）
```
- **PORTS：** 容器的端口信息和使用的连接类型（tcp\udp）。
-  **NAMES：** 自动分配的容器名称。

### 停止容器
```
docker stop <容器 ID>
```
### 重启容器
```
docker restart <容器 ID>
```

## 安装并启动nacos 单机版
```
docker run -d -e MODE=standalone  -p 8848:8848  --restart=always --name nacos nacos/nacos-server:2.0.2
```


## docker查看容器详细信息
```
docker inspect 容器ID
```