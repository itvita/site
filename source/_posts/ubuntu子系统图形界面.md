---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: ubuntu子系统图形界面
categories:
  - 分类1
tags:
  - 标签1
  - 标签2
mp3: /music/.mp3
cover: /img/.jpg
date: 2023-03-24 14:51:09
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

- [安装图形界面](#安装图形界面)
- [安装并配置远程桌面服务xrdp](#安装并配置远程桌面服务xrdp)
  - [安装xrdp](#安装xrdp)
  - [配置xrdp端口（将远程端口改为3390，避免和本机的3389端口冲突）](#配置xrdp端口将远程端口改为3390避免和本机的3389端口冲突)
  - [配置xsession](#配置xsession)
  - [重启xrdp服务](#重启xrdp服务)
- [使用win10的远程桌面连接工具](#使用win10的远程桌面连接工具)

<!-- /code_chunk_output -->


## 安装图形界面
```
sudo apt install xorg
sudo apt install xfce4
```

## 安装并配置远程桌面服务xrdp
### 安装xrdp 
    sudo apt install xrdp
### 配置xrdp端口（将远程端口改为3390，避免和本机的3389端口冲突）
    sudo sed -i 's/port=3389/port=3390/g' /etc/xrdp/xrdp.ini
### 配置xsession
    sudo echo xfce4-session >~/.xsession
### 重启xrdp服务
    sudo service xrdp restart

## 使用win10的远程桌面连接工具
    localhost:3390