---
title: centos创建sftp账号
categories:
  - linux
tags:
  - centos
  - sftp
mp3: /music/只要平凡-张杰&张碧晨.mp3
cover: /img/15666531161ade.jpg
date: 2022-11-21 12:00:13
---

## 使用系统自带的internal-sftp搭建SFTP服务器。

打开命令终端窗口，按以下步骤操作。

1、查看openssh的版本

    ssh -V 
使用ssh -V 命令来查看openssh的版本，版本必须大于4.8p1，低于的这个版本需要升级。

2、创建sftp组

    groupadd sftp

 3、创建一个sftp用户，用户名为mysftp2020，密码为mysftp2020

> 修改用户密码和修改Linux用户密码是一样的：

> 注意：这里我们将mysftp2020用户的shell设置为/bin/false使他没有登陆shell的权限

    useradd -g sftp -s /bin/false mysftp2020  //用户名
    passwd mysftp2020  //密码

4、sftp组的用户的home目录统一指定到/data/sftp下，按用户名区分，这里先新建一个mysftp2020目录，然后指定mysftp2020的home为/data/sftp/mysftp2020
sftp组的用户的home目录统一指定到/data/sftp下

    mkdir -p /data/sftp/mysftp2020
然后指定mysftp2020的home为/data/sftp/mysftp2020

`usermod -d /data/sftp/mysftp2020 mysftp2020`

5、配置sshd_config

    vim /etc/ssh/sshd_config

找到如下这行，用#符号注释掉，大致在文件末尾处。

    #Subsystem      sftp    /usr/libexec/openssh/sftp-server  

在文件最后面添加如下几行内容，然后保存。

    Subsystem sftp internal-sftp  
    #匹配sftp组的用户，如果有多个组用逗号分割 也可以使用“Match
    Match Group sftp  
    #User mysftp2020”匹配用户，多个用户之间也是用逗号分割
    #用chroot将用户的根目录指定到/data/ftp/%u,%u代表用户名,%h表示用户根目录
    ChrootDirectory /data/sftp/%u  
    #指定sftp命令
    ForceCommand    internal-sftp  
    AllowTcpForwarding no
    #禁止用户使用端口转发 建立用户和组放
    X11Forwarding no

6、设定Chroot目录权限
    

    chown root:sftp /data/sftp/mysftp2020
    chmod 755 /data/sftp/mysftp2020

7、建立SFTP用户登入后可写入的目录
照上面设置后，在重启sshd服务后，用户mysftp2020已经可以登录。但使用chroot指定根目录后，根应该是无法写入的，所以要新建一个目录供mysftp2020上传文件。这个目录所有者为mysftp2020，所有组为sftp，所有者有写入权限，而所有组无写入权限。命令如下：

    mkdir /data/sftp/mysftp2020/upload
    chown mysftp2020:sftp /data/sftp/mysftp2020/upload
    chmod 755 /data/sftp/mysftp2020/upload

8、修改/etc/selinux/config

    vim /etc/selinux/config
将文件中的SELINUX=enforcing 修改为 SELINUX=disabled ，然后保存。

再输入命令

    setenforce 0

9、重启sshd服务

    service sshd restart

10、验证sftp环境
用mysftp2020用户名登录，yes确定，回车输入密码。

    sftp mysftp2020@127.0.0.1
显示 sftp> 则sftp搭建成功。

11、使用FileZilla FTP Client连接SFTP服务器

> 输入主机IP地址、用户名、密码、端口连接SFTP服务器，端口默认为22。