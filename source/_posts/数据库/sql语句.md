---
title: sql语句
date: 2018-07-10 21:09:19
tags: 数据库
---
- #### oracle 取前10条记录

 1) select * from tbname where rownum < 11;

 2) select * from (select * from tbname order by id desc ) where rownum<=10;