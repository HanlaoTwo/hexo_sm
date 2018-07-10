---
title: MySQL
date: 2018-07-10 21:09:19
tags: mysql
---
- #### 修改用户名密码：
```
UPDATE user SET password=PASSWORD('123456') WHERE user='root';
FLUSH PRIVILEGES;
```
- #### 查勘表结构
```
show Create table 【tablename】
```
- #### update
```
UPDATE [LOW_PRIORITY] [IGNORE] tbl_name  
SET col_name1=expr1 [, col_name2=expr2 ...]  
[WHERE where_definition]  
[ORDER BY ...]  
[LIMIT row_count] 
```
- #### 用户权限和远程连接
```
mysql> USE mysql; -- 切换到 mysql DB

Database changed

mysql> SELECT User, Password, Host FROM user; -- 查看现有用户,密码及允许连接的主机

+------+----------+-----------+
| User | Password | Host      |
+------+----------+-----------+
| root |          | localhost |
+------+----------+-----------+
1 row in set (0.00 sec)

 

mysql> -- 只有一个默认的 root 用户, 密码为空, 只允许 localhost 连接
12
mysql> -- 下面我们另外添加一个新的 root 用户, 密码为空, 只允许 192.168.1.100 连接

mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.100' IDENTIFIED BY '' WITH GRANT OPTION;

 

mysql> -- @'192.168.1.100'可以替换为@‘%’就可任意ip访问，当然我们也可以直接用 UPDATE 更新 root 用户 Host, 但不推荐, SQL如下:

mysql> -- UPDATE user SET Host='192.168.1.100' WHERE User='root' AND Host='localhost' LIMIT 1;

mysql> flush privileges;

Query OK, 0 rows affected (0.00 sec)
```
[更多](http://www.cnblogs.com/jyginger/archive/2011/04/27/2030017.html)