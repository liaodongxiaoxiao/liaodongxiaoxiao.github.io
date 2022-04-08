---
layout: post
title:  树莓派安装MySQL
categories: [树莓派,MySQL]
tags:    [树莓派,MySQL]
date:   2022-04-07 12:00:00

---

      用树莓派做IoT项目或小程序常用到数据存储，那就一定离不开MySQL数据库，下面记录下在树莓派上安装MySQL的过程和远程连接使用。

### 0. 准备

树莓派安装软件第一步是更新系统source源和系统软件

> sudo apt update  
> sudo apt upgrade

### 1. 安装

> sudo apt install mariadb-server



### 2. 配置

数据库安装成功后，需要做root用户密码等相关配置，命令如下：

> sudo mysql_secure_installation

根据描述可以一步一步输入**Y** 或**N**，简单完成配置

- Enter current password for root (enter for none):

- Switch to unix_socket authentication [Y/n]

- Change the root password? [Y/n]

- Remove anonymous users? [Y/n]

- Disallow root login remotely? [Y/n]

- Remove test database and access to it? [Y/n] y

- Reload privilege tables now? [Y/n]

### 3. 连接MySQL

1. 设置**bind-address**
   
   > sudo vim /etc/mysql/mariadb.conf.d/50-server.cnf
   
   找到bind-address这一行，将其由默认的**127.0.0.1**修改成**0.0.0.0**，**:wq**保存并退出
   
   

2. 创建远程连接用户
   
   > GRANT ALL PRIVILEGES ON 库名.表名 TO '用户名'@'IP地址' IDENTIFIED BY '密码' WITH GRANT OPTION;
   
   例如：
   
   > GRANT ALL PRIVILEGES ON *.* TO 'pi'@'%' IDENTIFIED BY 'karl' WITH GRANT OPTION;  
   
   刷新设置：
   
   > FLUSH PRIVILEGES;
   
   3.连接MySQL
   
   通过**MySQL Workbench** 或其他窗口工具连接

### 4. 命令行启动(重启)/关闭MySQL服务

> sudo service mysql start
> 
> sudo service mysql restart
> 
> sudo service mysql stop

查看MySQL服务状态

> sudo service mysql stop



### -- the End --
