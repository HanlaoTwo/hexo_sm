---
title: sqoop-sqoop使用
date: 2018-07-10 21:09:19
tags: Hadoop
---
sql 中加入单引号包围的常量''
```
sqoop import 
--connect jdbc:oracle:thin:@//10.20.23.93:1521/HS2008 
--username hs_his
--password hundsun 
--query "SELECT 'bopcategory' as tag,a.* FROM hs_acpt.bopcategory a WHERE a.acpt_category_level = '2' and \$CONDITIONS" 
--split-by a.acpt_category_no 
--target-dir /usr/root/accept/bopcategory 
--fields-terminated-by "#"
```
