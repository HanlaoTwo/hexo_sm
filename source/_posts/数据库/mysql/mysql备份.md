---
title: mysql备份
date: 2018-07-10 21:09:19
tags: mysql
---
#### 备份一个数据库

　　mysqldump基本语法：

    mysqldump -u username -p dbname table1 table2 ...-> BackupName.sql

　　其中：

dbname参数表示数据库的名称；

table1和table2参数表示需要备份的表的名称，为空则整个数据库备份；

BackupName.sql参数表设计备份文件的名称，文件名前面可以加上一个绝对路径。通常将数据库被分成一个后缀名为sql的文件；

#### 备份多个数据库

　　语法：

    mysqldump -u username -p --databases dbname2 dbname2 > Backup.sql
　　加上了--databases选项，然后后面跟多个数据库

    mysqldump -u root -p --databases test mysql > D:\backup.sql
#### 备份所有数据库

　　mysqldump命令备份所有数据库的语法如下：

    mysqldump -u username -p -all-databases > BackupName.sql
　　示例：

    mysqldump -u -root -p -all-databases > D:\all.sql

#### 备份表
语句：

    select * from students where Age > 30 into outfile ‘/tmp/stud.txt' ;   //将年龄大于三十的同学的信息备份出来 

备份的目录路径必须让当前运行mysql服务器的用户mysql具有访问权限

可能会报错

    mysqldump: Got error: 1290以及secure-file-priv option

secure-file-priv参数是用来限制LOAD DATA, SELECT … OUTFILE, and LOAD_FILE()传到哪个指定目录的。

当secure_file_priv的值为null ，表示限制mysqld 不允许导入|导出

当secure_file_priv的值为/tmp/ ，表示限制mysqld 的导入|导出只能发生在/tmp/目录下

当secure_file_priv的值没有具体值时，表示不对mysqld 的导入|导出做限制

查看系统值

    show global variables like '%secure%'; 

修改系统值

mysql.cnf中的[mysqld]加入secure_file_priv = 