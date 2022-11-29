---
title: bbb视频会议系统搭建
categories:
  - linux
tags:
  - 视频会议
mp3: /music/偏偏喜欢你.mp3
cover: /img/1668498315bfb1.jpg
date: 2022-11-19 12:16:23
---
# 安装
> 要先准备云服务器，域名。

## 更新镜像

1、备份配置文件：

cp -a /etc/apt/sources.list /etc/apt/sources.list.bak

2、修改**sources.list**文件，将**http://archive.ubuntu.com**和**http://security.ubuntu.com**替换成**http://mirrors.huaweicloud.com**，可以参考如下命令：

```
sed -i "s@http://.*archive.ubuntu.com@http://mirrors.huaweicloud.com@g" /etc/apt/sources.list
sed -i "s@http://.*security.ubuntu.com@http://mirrors.huaweicloud.com@g" /etc/apt/sources.list
```

3、执行**apt-get update**更新索引

继续更新服务器，按顺序逐行执行命令

```
grep "multiverse" /etc/apt/sources.list
```

执行完此命令后如果没有看到

```
deb http://archive.ubuntu.com/ubuntu trusty multiverse
```

或者

```
deb http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse
```

则执行

```
echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty multiverse" | sudo tee -a /etc/apt/sources.list
```

然后执行命令

```
sudo apt-get update
sudo apt-get dist-upgrade
```

接下来安装LibreOffice（ppt转换工具）

```
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:libreoffice/libreoffice-4-4
```

## 然后根据官网安装（首先要配置防火墙）

http://docs.bigbluebutton.org/2.2/install.html#4--install-bigbluebutton

安装过程需要一晚上~

安装demo

配置ssl

# 问题

1. 问题详细提示如下:

   E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarly unavailable)

   E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is an other process using it?

2. 如何解决这种问题呢?

　　2.1 首先查看是否有apt-get这个程序在运行

```
ps aux|grep apt-get
```

　　2.2 如果发现存在这样的程序在运行那么就kill掉，否则执行2.3

　　2.3 直接删除锁文件

```
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/dpkg/lock
```

# 报错1007：

ICE协商失败** -浏览器和FreeSWITCH尝试协商用于流媒体的端口，并且协商失败。可能的原因：

- NAT阻止了连接
- 防火墙阻止UDP连接/端口

更新 FreeSWITCH配置

http://docs.bigbluebutton.org/2.2/configure-firewall.html#update-freeswitch



# 报错1020 ，无法启用视频

http://docs.bigbluebutton.org/2.2/configure-firewall.html#extra-steps-when-server-is-behind-nat

### Kurento安装方法

安装gunpg

```
apt-get update \`` ``&& apt-get ``install` `--no-``install``-recommends --``yes` `\``  ``gnupg
```

2、确定ubuntu版本

```
cat` `/etc/issue``Ubuntu 18.04.2 LTS \n \l ``#输出
```

3、设置变量（根据上一步的结果 ，下面2行选1行执行）

```
# Run ONLY ONE of these lines:``DISTRO=``"xenial"` `# KMS for Ubuntu 16.04 (Xenial)``DISTRO=``"bionic"` `# KMS for Ubuntu 18.04 (Bionic)
```

4、添加key

```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5AFA7A83
```

5、设置kurento.list

```
tee` `"/etc/apt/sources.list.d/kurento.list"` `>``/dev/null` `<`# Kurento Media Server - Release packages``deb [arch=amd64] http:``//ubuntu``.openvidu.io``/6``.10.0 $DISTRO kms6``EOF
```

注：这一步的作用，实际就是在"/etc/apt/sources.list.d/kurento.list" 这个文件中，追加一行deb [arch=amd64] http://ubuntu.openvidu.io/6.10.0 $DISTRO kms6。

执行时，terminal终端中，按顺序把上面4行，都复制进去就行（注：1个字符都不要少）

6、安装kurento media server

```
apt-get update \`` ``&& apt-get ``install` `--``yes` `kurento-media-server
```

7、启动/停止

```
sudo` `service kurento-media-server start``sudo` `service kurento-media-server stop
```

# Error: Unable to connect to the FreeSWITCH Event Socket Layer on port 8021

## FreeSWITCH无法绑定到端口8021

FreeSWITCH支持IPV4和IPV6。但是，如果您的服务器不支持IPV6，则FreeSWITCH将无法绑定到端口8021。如果运行`sudo bbb-conf --check`并看到以下错误

```
# Error: Found text in freeswitch.log:
#
#    Thread ended for mod_event_socket
#
# FreeSWITCH may not be responding to requests on port 8021 (event socket layer)
# and users may have errors joining audio.
#
```

可能是您的服务器已禁用IPV6（或不支持它）。您可以通过运行以下命令进行检查

```
$ sudo ip addr | grep inet6
inet6 ::1/128 scope host
...
```

如果看不到该行`inet6 ::1/128 scope host`，则您的服务器已禁用IPV6。在这种情况下，我们需要禁用FreeSWITCH对IPV6的支持。首先，编辑`/opt/freeswitch/etc/freeswitch/autoload_configs/event_socket.conf.xml`并更改行

```
    <param name="listen-ip" value="::"/>
```

至

```
    <param name="listen-ip" value="127.0.0.1"/>
```

这告诉FreeSWITCH，不是将端口8021绑定到本地IPV6地址，而是绑定到IPV4地址127.0.0.1。接下来，执行以下两个命令

```
$ sudo mv /opt/freeswitch/etc/freeswitch/sip_profiles/internal-ipv6.xml /opt/freeswitch/etc/freeswitch/sip_profiles/internal-ipv6.xml_
$ sudo mv /opt/freeswitch/etc/freeswitch/sip_profiles/external-ipv6.xml /opt/freeswitch/etc/freeswitch/sip_profiles/external-ipv6.xml_
```

然后使用命令重新启动BigBlueButton

```
$ sudo bbb-conf --clean
$ sudo bbb-conf --check
```