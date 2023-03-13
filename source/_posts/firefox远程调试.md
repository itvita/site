---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: firefox远程调试
categories:
  - 分类1
tags:
  - 标签1
  - 标签2
mp3: 
cover: 
date: 2023-01-31 18:24:04
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [安装adb](#安装adb)
    1. [下载](#下载)
    2. [解压配置环境变量](#解压配置环境变量)
2. [安卓 firefox配置](#安卓-firefox配置)
3. [windows firefox配置](#windows-firefox配置)

<!-- /code_chunk_output -->


## 安装adb
### 下载
Windows版本：[https://dl.google.com/android/repository/platform-tools-latest-windows.zip](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
Mac版本：[https://dl.google.com/android/repository/platform-tools-latest-darwin.zip](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)
Linux版本：[https://dl.google.com/android/repository/platform-tools-latest-linux.zip](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)
### 解压配置环境变量
![](/img/20230131182908.png)
![](/img/20230131182943.png)
![](/img/20230131183007.png)


## 安卓 firefox配置
1. 设置中开始usb调试
2. usb连接电脑

## windows firefox配置
1. 地址栏输入 about:config 搜索 devtools.debugger.remote-enabled  设置为true
2. 更多工具中找到远程调试，打开
3. 启用usb调试
4. 打开命令行 执行 adb forward tcp:6000 tcp:6000
5. 刷新设备 连接即可