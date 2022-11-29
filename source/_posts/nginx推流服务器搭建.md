---
title: nginx推流服务器搭建
categories:
  - nginx
tags:
  - nginx
mp3: /music/无聊的夏天.m4a
cover: /img/225228-163145834897ce.jpg
date: 2022-11-29 18:05:05
---
## 预先下载
> nginx rtmp版本
1. nginx 1.7.11.3 Gryphon.zip 下载地址：http://nginx-win.ecsds.eu/download/
>nginx rtmp监控
2. nginx-rtmp-module-master.zip 下载地址：https://github.com/arut/nginx-rtmp-module/
>直播推流
3. OBS(Open Broadcaster Software) 下载地址：https://obsproject.com
>rtmp播放器
4. VLC 播放器 下载地址：https://www.videolan.org/

## 安装nginx
。。。
## 安装rtmp监控
只需解压  nginx-rtmp-module-master 到nginx目录

## nginx.conf 配置
```

worker_processes  1;   #Nginx进程数，建议设置为等于CPU总核数
 
events {
    worker_connections  1024;  #工作模式与连接数上限
}
 
rtmp_auto_push on;
 
 
#RTMP服务
rtmp  {
    server  {
        listen 1935;
        chunk_size 4096;
        application live  {
            live on;
            record off;
        }
        application live2  {
            live on;
            record off;
        }
        application vod  {
            play /var/flvs;
        }
        application vod_http  {
            play http://127.0.0.1/vod;
        }
        application hls  {
            live on;
            hls on;
            hls_path /tmp/hls;
        }
    }
}
 
 
#HTTP服务
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
 
    server {
        listen       80;
        server_name  localhost;
 
        location / {
            root   html;
            index  index.html index.htm;
        }
 
        location /live_hls{
		    types{
			    #m3u8 type设置
				application/vnd.apple.mpegurl m3u8;
				#ts分片文件设置
				video/mp2t ts;
			}
			#指向访问m3u8文件目录
			alias ./m3u8File;
			    add_header Cache-Control no-cache; #禁止缓存
		}
 
        location /control{
		    rtmp_control all;
		}
		
		location /stat{
		    rtmp_stat all;
			rtmp_stat_stylesheet stat.xsl;
		}
		location /stat.xsl{
		    root ./nginx-rtmp-module-master;
		}
 
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}

```

## nginx 常用命令
```
start nginx # 开启nginx
nginx -s stop # 关闭nginx
nginx -s reload # 重新启动nginx
nginx -v # 查看版本号
nginx -t # 验证配置文件是否正确
```

## 开启nginx
start ./nginx.exe

## 监控地址
http://127.0.0.1/stat
可以查看直播监控状态

## 推流
1. 打开 OBS
2. 添加场景
3. 添加来源
4. 开始推流
5. 设置->推流->服务器设置为：rtmp://127.0.0.1:1935/live
6. 登录监控地址http://127.0.0.1/stat 可以看到推流数据
   
## 拉流
1. 打开VCL
2. 媒体->打开网络串流->url设置为：rtmp://127.0.0.1:1935/live
  


## ffmpeg 转播摄像头画面
## 下载地址
https://github.com/FFmpeg/FFmpeg/releases
## 安装
。。。
## 大华摄像头rtsp地址
```
rtsp://帐号:密码@摄像头IP/cam/realmonitor?channel=1&subtype=1
```
## 海康摄像头rtsp地址
```
rtsp://帐号:密码@摄像头IP/cam/realmonitor?channel=1&subtype=1
```
## 转播到nginx rstp
```
ffmpeg -i "rtsp://admin:a123456789@192.168.31.27/cam/realmonitor?channel=1&subtype=1" -vcodec copy -acodec copy -f flv "rtmp://127.0.0.1:1935/live"
```