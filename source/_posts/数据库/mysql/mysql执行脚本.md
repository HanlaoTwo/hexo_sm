---
title: mysql执行脚本
date: 2018-07-10 21:09:19
tags: mysql
---
```
、创建包含sql命令的sql脚本文件
文件中包含一些列的sql语句，每条语句最后以;结尾，文件内容示例如下：
--创建表，使用“--”进行注释
create table 表名称
(                   
  Guid Varchar(38) not null primary key,  
  Title Varchar(255),       
              
) TYPE=InnoDB;
--在表A中增加字段Status
alter table A add Status TinyInt default '0';
--在表A上创建索引
create index XX_TaskId_1 on A(Id_);
--在A表中添加一条记录
Insert into A (Id,ParentId, Name) values(1,0,'名称');
--添加、修改、删除数据后，有可能需要提交事务
Commit;
2、执行sql脚本文件
方法一 使用cmd命令执行(windows下，unix或linux在的其控制台下)
【Mysql的bin目录】\mysql –u用户名 –p密码 –D数据库<【sql脚本文件路径全名】，示例：
D:\mysql\bin\mysql –uroot –p123456 -Dtest<d:\test\ss.sql
注意：
A、如果在sql脚本文件中使用了use 数据库，则-D数据库选项可以忽略
B、如果【Mysql的bin目录】中包含空格，则需要使用“”包含，如：“C:\Program Files\mysql\bin\mysql” –u用户名 –p密码 –D数据库<【sql脚本文件路径全名】

方法二 进入mysql的控制台后，使用source命令执行
Mysql>source 【sql脚本文件的路径全名】 或 Mysql>\. 【sql脚本文件的路径全名】，示例：
source d:\test\ss.sql 或者 \. d:\test\ss.sql