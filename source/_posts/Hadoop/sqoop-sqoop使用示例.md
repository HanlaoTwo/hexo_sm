---
title: sqoop-sqoop使用示例
date: 2018-07-10 21:09:19
tags: Hadoop
---
### sqoop
Sqoop是一款开源的工具，主要用于在HADOOP不传统的数据库(mysql、postgresql等)进行数据的传递，可以将一个关系型数据库（例如：MySQL、Oracle、Postgres等）中的数据导进到Hadoop的HDFS中，也可以将HDFS的数据导进到关系型数据库中。Sqoop中一大亮点就是可以通过hadoop的mapreduce把数据从关系型数据库中导入数据到HDFS。
### 参数配置
##### 1.使用参数
```
sqoop import --connect jdbc:mysql://localhost/db --username foo --table TEST
```
##### 2.使用文件
```
sqoop --options-file /users/homer/work/import.txt --table TEST
```
import.txt如下：
```
import
--connect
jdbc:mysql://localhost/db
--username
foo
```
配置文件支持添加注释
```
#
# Options file for Sqoop import
#
# Specifies the tool being invoked
import
# Connect parameter and value
--connect
jdbc:mysql://localhost/db
# Username parameter and value
--username
foo
#
# Remaining options should be specified in the command line.
```
### 数据导入
#### 1.连接数据库
连接

    $ sqoop import --connect jdbc:mysql://database.example.com/employees
    
    #添加用户名和密码配置
    sqoop import --connect jdbc:mysql://localhost/db --username foo --table TEST
安全考虑可以把password放在文件里

    sqoop import --connect jdbc:mysql://database.example.com/employees \
    --username venkatesh --password-file ${user.home}/.password

#### 2.选择导出数据
--table可以配置要导出的表
    
    sqoop import --connect jdbc:mysql://localhost/db --username foo --table TEST
--columns 可以配置要导出的列名

     --columns "name,employee_id,jobtitle"
     
     sqoop import --connect jdbc:mysql://localhost/db --username foo --password pwd --table user \
     --columns "name,id,age"
--where 设置选择条件

    --where "age > 400"
    sqoop import --connect jdbc:mysql://localhost/db --username foo --password pwd --table user \
    --where "age > 400"
    
#### 3.使用sql语句
--query 和--target-dir一起使用

    sqoop import --connect jdbc:mysql://localhost/db --username foo --password pwd\
    --query 'SELECT a.*, b.* FROM a JOIN b on (a.id == b.id) WHERE $CONDITIONS' \
    --split-by a.id --target-dir /user/foo/joinresults

 -m [number] 设置map数量
 
    #设置1个map
    sqoop import --connect jdbc:mysql://localhost/db --username foo --password pwd\
    --query 'SELECT a.*, b.* FROM a JOIN b on (a.id == b.id) WHERE $CONDITIONS' \
    -m 1 --split-by a.id --target-dir /user/foo/joinresults

#### 4.分隔取出的数据

 --fields-terminated-by 设置字段之间的分隔符  --lines-terminated-by 设置每行之间的分隔符
    
    sqoop import --connect jdbc:mysql://localhost/db --username foo --password pwd\
    --fields-terminated-by "\0001"  --lines-terminated-by "\n";