---
title: Hive
date: 2018-07-10 21:09:19
tags: Hadoop
---
- #### Hive默认的分隔符

Hive的表数据，不管导出到HDFS还是本地文件系统，如果用户在导出时没有指定分割符，那么Hive表的数据在写入文件时，会使用默认的分隔符作为列分隔符，该默认的分割是“CTR+A”，ASCII码排第二位的字符，是不可见字符，二进制表示：'\u0001'。

手动设置分隔符
```
drop table if exists hs_ods.tmp_acpt_busin_type ;
CREATE EXTERNAL TABLE hs_ods.tmp_acpt_busin_type(
acpt_busin_type string,
p45 string,
p46 string,
p47 string,
p50 String
)
LOCATION  '/user/hive/sourcetab/hs_ods/ods_tmp_acpt_busin_type';
ROW FORMAT DELIMITED FIELDS TERMINATED BY '~';
```
- #### 删除数去库语法
```
DROP DATABASE StatementDROP (DATABASE|SCHEMA) [IF EXISTS] database_name 
[RESTRICT|CASCADE];
```
- #### 修改表结构
```
CREATE TABLE test_change (a int, b int, c int);
 
// First change column a's name to a1.
ALTER TABLE test_change CHANGE a a1 INT;
 
// Next change column a1's name to a2, its data type to string, and put it after column b.
ALTER TABLE test_change CHANGE a1 a2 STRING AFTER b;
// The new table's structure is:  b int, a2 string, c int.
 
// Then change column c's name to c1, and put it as the first column.
ALTER TABLE test_change CHANGE c c1 INT FIRST;
// The new table's structure is:  c1 int, b int, a2 string.
 
// Add a comment to column a1
ALTER TABLE test_change CHANGE a1 a1 INT COMMENT 'this is column a1';
```

- #### 带参数的hivesql

sql脚本
```
vim hivesql_with_param.sql
use database;
select 
'${hiveconf:begin_date}'，'${hiveconf:end_date}'
from table;
```
运行命令

    hive -hiveconf begin_date=1 -hiveconf end_date=2 -f hivesql_with_param.sql

hive表增加分区

    alter table ods_hs_his_his_asset add partition (part_date='20170130') location '/user/hive/sourcetab/hs_ods/ods_hs_his_his_asset/20170130'; 

删除分区

    alter table ods_hs_data_assetdebit drop partition (part_date='20170103');

- #### 计算引擎 
hive.execution.engine