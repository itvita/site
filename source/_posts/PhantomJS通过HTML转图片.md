---
title: PhantomJS通过HTML转图片
categories:
  - html
tags:
  - phantomjs
  - html
mp3: /music/少女的祈祷.m4a
cover: /img/183737-16260862577694.jpg
date: 2022-11-29 18:12:09
---
## 前提条件
负责转换的服务器需要先安装phantomjs
- [淘宝镜像下载地址](http://npm.taobao.org/dist/phantomjs/)
- [官方下载地址](https://phantomjs.org/download.html)
- 解压放于软件目录即可
  >如：C:\tools\phantomjs-2.1.1-windows
### 使用
- [官方API](https://phantomjs.org/api/webpage/method/child-frames-count.html)
#### java代码
```java
package cn.itvita.system;

import lombok.extern.slf4j.Slf4j;

import java.io.*;

@Slf4j
public class Test2 {
    public static void main(String[] args) throws IOException {
        StringBuilder sb = new StringBuilder();
        sb.append("C:\\tools\\phantomjs-2.1.1-windows\\bin\\phantomjs.exe "); //phantomjs 安装地址
        sb.append("C:\\Users\\liuqiang\\Desktop\\test\\script.js "); //脚本地址
        sb.append("https://www.baidu.com/s?tn=59044660_hao_pg&ie=utf-8&wd=1 ");//html源地址
        sb.append("C:\\Users\\liuqiang\\Desktop\\test\\baidu.png ");//图片存放地址
        sb.append("1 ");//缩放级别

        Process process = Runtime.getRuntime().exec(sb.toString());//你的图片输出路径
        InputStream inputStream = process.getInputStream();
        BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
        String r;
        while ((r = reader.readLine()) != null) {
            log.info("PhantomJS输出：{}", r);
            if ("done".equals(r)) {
                if (process != null) {
                    process.destroy();
                    process = null;
                }
            }
        }
        if (reader != null) {
            reader.close();
        }
        System.out.println("渲染结束...");
        inputStream.close();
    }
}
```
#### javascript脚本代码
```javascript
/**
 * phantomJs 脚本 */
var page = require("webpage").create(),
  system = require("system"),
  address,
  output,
  size;
if (system.args.length < 3 || system.args.length > 5) {
  phantom.exit(1);
} else {
  address = system.args[1]; //转换地址
  output = system.args[2]; //输出地址
  page.zoomFactor = system.args[3]; //比例缩放
  console.log(address, output, page.zoomFactor)
  page.open(address, function(status) {
    console.log("Status: " + status);
    if (status === "success") {
      page.render(output);
    }
    page.close();
    console.log("done");
    phantom.exit();
  });
}
```