---
title: centos安装gitblit
categories:
  - linux
tags:
  - git
  - CentOs
mp3: /music/Anesthesia-Vexento.mp3
cover: /img/pexels-jill-wellington-40192.jpg
date: 2022-11-13 19:57:05
---
# 下载
http://gitblit.github.io/gitblit/
# 安装
1.  上传到centos /opt下，解压为 gitblit
2. 进入gitblit/data 修改默认配置文件
> default.properties
```
server.httpPort = 8088  #访问端口 
server.httpsPort = 0 (#0表示禁用此https端口，根据个人需求设置)
server.httpBindInterface = 主机IP (#默认为空，也可写成主机IP，为空时则可以通过远程访问gitblit，建议为空)
```
# 启动 
```
./gitblit.sh

后台启动：
nohup ./gitblit.sh &
```

# 配置nginx访问
1.nginx转发配置
```
    #gitblit
    server {
	    listen 80;
	    server_name  域名;
	
	    location / {
	        proxy_pass http://localhost:8088/;
	    }
    }

```
2.转码问题 （无法加载目录）
> default.properties
```
web.forwardSlashCharacter = !
```
3.仓库地址问题
```
web.canonicalUrl = http://域名
```