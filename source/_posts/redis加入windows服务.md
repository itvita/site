---
title: redis加入windows服务
categories:
  - redis
tags:
  - redis
mp3: /music/装进夏日的晚风.m4a
cover: /img/195226-16567627465c0a.jpg
date: 2022-11-29 18:13:57
---

## 安装命令:
```shell
redis-server.exe --service-install redis.windows.conf --loglevel verbose 
```
## 卸载命令：
```shell
redis-server --service-uninstall  
```