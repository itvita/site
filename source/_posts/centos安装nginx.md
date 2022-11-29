---
title: centos安装nginx
categories:
  - linux
tags:
  - centos
  - nginx
date: 2022-11-17 20:44:04
mp3: /music/Asgard-Electus.mp3
cover: /img/microsoft-edge-RoaneQUy84A-unsplash.jpg
---

# 下载地址

[nginx官网](http://nginx.org/en/download.html)

# 命令下载

```shell
wget http://nginx.org/download/nginx-1.18.0.tar.gz
```

# 安装依赖包

```shell
yum install gcc gcc-c++ pcre* openssl* gd-devel* zlib-devel pcre-devel
```

# 解压并进入目录

```shell
tar –zxvf nginx-1.18.0.tar.gz
cd nginx-1.18.0
```

# 创建nginx用户

```shell
useradd -M -s /sbin/nologin nginx
```

# 配置编译参数

```shell
./configure --prefix=/opt/nginx --with-http_stub_status_module --with-http_ssl_module --with-http_realip_module --with-http_flv_module --with-http_mp4_module --with-http_gzip_static_module --with-stream --with-stream_ssl_module #./configure –help
```

# 安装

```shell
make && make install
```

# 启动

```shell
cd /opt/nginx/sbin
./nginx
```

# 其它

```shell
刷新配置
./nginx -s reload
停止
./nginx -s stop
```

# 配置

## 腾讯云证书https的基本配置

```shell
upstream myproject {
    server 127.0.0.1:8000 weight=3; //weight 权重，数字越大轮到的几率越大
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
    server 127.0.0.1:8003;
 }

#myMiniProgram
server {  
	listen 80;  
	server_name xx.com;  
	rewrite ^(.*)$  https://$host$1 permanent;  
}

server {
	#SSL 访问端口号为 443
  listen 443 ssl; 
  #填写绑定证书的域名
  server_name cloud.tencent.com; 
  #证书文件名称
  ssl_certificate 1_cloud.tencent.com_bundle.crt; 
  #私钥文件名称
  ssl_certificate_key 2_cloud.tencent.com.key; 
  ssl_session_timeout 5m;
  #请按照以下协议配置
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2; 
  #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
  ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
  ssl_prefer_server_ciphers on;
	
	#代理转发
	location / {
	    #自定义请求头内容
		proxy_set_header X-Forwarded-Scheme  https;
		proxy_set_header X-Forwarded-port  443;
		client_max_body_size 1000m; 
		#设置主机头和客户端真实地址，以便服务器获取客户端真实IP
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
        #禁用缓存
        proxy_buffering off;
        #反向代理的地址
        proxy_pass http://localhost:7878; 
        # proxy_pass http://myproject; #用这行代替上面，实现负载均衡
        #启用支持websocket连接
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
	}
	#静态代理
	location /admin {
	   alias /usr/local/mymini/cpp-web;
       index login.html;
    }
}
```

# srpingboot request.get...uri ,还是http怎么办？

> 配置tomcat

```
server.tomcat.protocol-header=X-Forwarded-Proto # ssl forward headers
server.tomcat.remote-ip-header=X-Forwarded-For
```

#### 代理tcp协议链接mysql

```
stream {
    upstream cloudsocket {
       hash $remote_addr consistent;
      # $binary_remote_addr;
       server 127.0.0.1:3306 weight=5 max_fails=3 fail_timeout=30s;
    }
    server {
       listen 3306;#数据库服务器监听端口
       proxy_connect_timeout 10s;
       proxy_timeout 300s;#设置客户端和代理服务之间的超时时间，如果5分钟内没操作将自动断开。
       proxy_pass cloudsocket;
    }
}
```