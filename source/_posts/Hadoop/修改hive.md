---
title: 修改hive
date: 2018-07-10 21:09:19
tags: Hadoop
---
- #### 1.修改设置
修改配置hive.metastore.warehouse.dir

    hive.metastore.warehouse.dir = /hive/home/warehouse

- #### 2.删除原有数据库
```
drop database hello cascade;
```
- #### 3.重建数据库
不重建database会目录不会变