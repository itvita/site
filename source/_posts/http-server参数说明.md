---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: http-server参数说明
categories:
  - 分类1
tags:
  - 标签1
  - 标签2
mp3: 
cover:
date: 2022-12-23 14:55:27
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->



<!-- /code_chunk_output -->
http-server --cors
```
-p 端口号 (默认 8080)
-a IP 地址 (默认 0.0.0.0)
-d 显示目录列表 (默认 'True')
-i 显示 autoIndex (默认 'True')
-e or --ext 如果没有提供默认的文件扩展名(默认 'html')
-s or --silent 禁止日志信息输出
--cors 启用 CORS via the Access-Control-Allow-Origin header
-o 在开始服务后打开浏览器
-c 为 cache-control max-age header 设置Cache time(秒) , e.g. -c10 for 10 seconds (defaults to '3600'). 禁用 caching, 则使用 -c-1.
-U 或 --utc 使用UTC time 格式化log消息
-P or --proxy Proxies all requests which can't be resolved locally to the given url. e.g.: -P http://someurl.com
-S or --ssl 启用 https
-C or --cert ssl cert 文件路径 (default: cert.pem)
-K or --key Path to ssl key file (default: key.pem).
-r or --robots Provide a /robots.txt (whose content defaults to 'User-agent: *\nDisallow: /')

```