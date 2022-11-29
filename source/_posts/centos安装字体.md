---
title: centos安装字体
categories:
  - linux
tags:
  - centos
date: 2022-11-29 11:33:04
mp3: /music/这世界那么多人-莫文蔚.mp3
cover: /img/b467112d1e734a607c57ddf450c72cdc.jpg
---

# 事先安装
```shell
yum -y install fontconfig
yum -y install mkfontscale
```
# 查看已安装字体
```shell
fc-list
```
# 查看linux已安装中文字体
```shell
fc-list :lang=zh
```
# 安装字体
## 1. 进入字体目录
```
cd /usr/share/fonts
```
## 2. 新建目录 myfonts
```
mkdir myfonts
```
## 3. 上传字体到myfonts,并进入目录
> window字体目录 C:\Windows\Fonts 
## 4. 开始安装
```shell
# 更新字体库索引
mkfontscale
mkfontdir
# 更新字体缓存
fc-cache
```