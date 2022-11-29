---
title: mac无法打开或已损坏解决办法
categories:
  - mac
tags:
mp3: /music/黑桃A.mp3
cover: /img/1619189236e4d9.jpg
date: 2022-11-27 12:08:26
---


1、系统偏好设置... -> 安全性与隐私-->修改为任何来源

2、如果没有任何来源  ,打开终端执行:sudo spctl --master-disable

如果还不行 

sudo xattr -d com.apple.quarantine /Applications/Navicat\ for\ SQL\ Server.app


/Applications/Navicat\ for\ SQL\ Server.app 为app路径  

如果有空格，空格前加 \