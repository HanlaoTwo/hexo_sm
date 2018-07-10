---
title: Linux 下MySQL安装卸载
date: 2018-07-10 21:09:19
tags: Linux
---
[卸载](http://www.cnblogs.com/kerrycode/p/4364465.html)
[安装](https://www.cnblogs.com/starof/p/4680083.html)
#### 1.环境
centos 6.5
#### 2.安装
```
 yum install -y mysql-server mysql mysql-deve
```
##### 报错：
```
Loading mirror speeds from cached hostfile
 * base: mirrors.163.com
 * extras: mirror.bit.edu.cn
 * updates: mirror.bit.edu.cn
没有可用软件包 mysql-server。
错误：无须任何处理
```
##### 原因：
> CentOS 7 版本将MySQL数据库软件从默认的程序列表中移除，用mariadb代替了。
MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可。开发这个分支的原因之一是：甲骨文公司收购了MySQL后，有将MySQL闭源的潜在风险，因此社区采用分支的方式来避开这个风险。MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。

##### 解决办法：

安装mariadb
```
yum install mariadb-server mariadb 
```
##### mariadb数据库的相关命令:



命令| 说明
---|---
systemctl start mariadb | #启动MariaDB
systemctl stop mariadb  | #停止MariaDB
systemctl restart mariadb | #重启MariaDB
systemctl enable mariadb | #设置开机启动

mariadb和mysql命令大部分一致，第一次登陆使用

    mysql -u root -p
密码是空直接enter

#### 链接：

[centos7 mysql数据库安装和配置](https://www.cnblogs.com/starof/p/4680083.html)

[CentOS6.4下Mysql数据库的安装与配置](http://www.cnblogs.com/xiaoluo501395377/archive/2013/04/07/3003278.html)