---
title: centos安装mysql5.7
categories:
  - linux
tags:
  - centos
  - mysql
date: 2022-11-17 20:24:48
mp3: /music/Anesthesia-Vexento.mp3
cover: /img/StockSnap_2W0L5IENXQ.jpg
---

# 安装
**1、检查Linux是否安装了mariadb数据库，mariadb数据库是mysql的分支**

```shell
#执行命令：
yum list installed | grep mariadb 
```

**2、如果Linux中安装了mariadb数据库，先卸载掉，因为CentOS 7.6 内部集成了mariadb，而安装mysql的话会和mariadb的文件冲突，所以需要先卸载掉mariadb**

```shell
#执行命令：
yum -y remove mariadb-libs.x86_64
```

**3、下载mysql安装包**

```shell
#执行命令：
wget https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.32-linux-glibc2.12-x86_64.tar.gz
#然后移动到/usr/local下
mv mysql-5.7.32-linux-glibc2.12-x86_64.tar.gz /usr/local
```

**4、解压**

```shell
#解压下载下来的mysql软件压缩包，执行命令：
tar -zxvf mysql-5.7.32-linux-glibc2.12-x86_64.tar.gz
```

**5、更名**

```shell
#解压下载下来的mysql软件压缩包，执行命令：
mv mysql-5.7.32-linux-glibc2.12-x86_64 mysql
#然后进入目录
cd mysql
```

**6、在mysql-5.7.32文件夹目录下创建一个/data/3306文件夹**

```shell
#执行命令：
mkdir -vp ./data 
#（v表示创建新目录都显示信息，p表示递归创建）
```

**7、添加mysql用户及用户组**

```shell
#执行命令：
groupadd mysql

useradd mysql -g mysql 
#（-g: 是指定用户所在组）
```

**8、切换到./bin目录下执行：**

```shell
./mysqld --initialize-insecure --user=mysql --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql
#（--initialize-insecure标识不设置密码， root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.）
```

**9、在mysql/bin目录下**

```shell
#执行命令：
./mysql_ssl_rsa_setup --datadir=/usr/local/mysql/data （表示安全连接访问，生成RSA私钥）
```

**10、更改mysql-5.7.32整个文件夹目录权限所属**

```shell
#执行命令：
chown -R mysql:mysql /usr/local/mysql （-R表示迭代递归）
#chmod：文件/目录权限设置命令
```

**11、在/etc 目录下创建my.cnf文件**

```shell

[client]
port = 3306
socket = /opt/mysql5.7.32/data/3306/mysql.sock
default-character-set=utf8

[mysqld]
port = 3306
socket = /opt/mysql5.7.32/data/3306/mysql.sock
datadir = /opt/mysql5.7.32/data/3306
log-error = /opt/mysql5.7.32/data/3306/error.log
pid-file = /opt/mysql5.7.32/data/3306/mysql.pid
lower_case_table_names=1
character-set-server=utf8mb4
#skip-grant-tables

[mysql]
default-character-set=utf8mb4

```

至此MySQL安装完成;

**12、启动MySQL服务**

```shell
#在mysql-5.7.24/bin目录下执行命令：
./mysqld_safe --defaults-file=/etc/my.cnf
```

**13、修改密码**

```shell
#登录进入mysql，在mysql-5.7.32/bin目录下执行命令：
./mysql -uroot -p -P3306 -h127.0.0.1
#修改mysql的密码，执行：
alter user 'root'@'localhost' identified by '123456';
#然后刷新
flush privileges; 
```

**14授权远程访问**

```shell
#登录进入mysql执行命令：（这样远程客户端才能访问）
grant all privileges on *.* to root@'%' identified by '123456';
#其中*.* 的第一个*表示所有数据库名，第二个*表示所有的数据库表；
#root@'%' 中的root表示用户名，%表示ip地址，%也可以指定具体的ip地址，比如root@localhost，root@xx.xx.xx.xx
#然后刷新
flush privileges; 
```

**15、关闭MySQL服务**

```shell
# 进入mysql-5.7.32/bin目录下执行命令：
./mysqladmin -uroot -p -P3306 -h127.0.0.1 shutdown
```

# 配置环境变量

```shell
#vim /etc/profile -- 所有用户生效
#vim ~/.bash_profile --当前用户生效
export MYSQL_HOME="/usr/local/mysql"
export PATH="$PATH:$MYSQL_HOME/bin"
```

# 刷新环境变量

```shell
 source  /etc/profile
```

# 设置到开机启动

```shell
 cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld  

 cp //usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysql

 chmod 700 /etc/init.d/mysql   

	# 加入到系统服务命令
 chkconfig --add mysqld    

 chkconfig --level 2345 mysqld on 
```

# 其他命令

```shell
#启动
 service mysql start
#停止
 service mysql stop
#重启
 service mysql restart
```