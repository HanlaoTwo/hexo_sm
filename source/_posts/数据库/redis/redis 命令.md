---
title: redis 命令
date: 2018-07-10 21:09:20
tags: redis
---
[菜鸟教程]()

[redis爱好者](http://doc.redisfans.com/)

查看所有key
```
keys * #*可以是正则表达式

KEYS pattern
查找所有符合给定模式 pattern 的 key 。

KEYS * 匹配数据库中所有 key 。
KEYS h?llo 匹配 hello ， hallo 和 hxllo 等。
KEYS h*llo 匹配 hllo 和 heeeeello 等。
KEYS h[ae]llo 匹配 hello 和 hallo ，但不匹配 hillo 。
特殊符号用 \ 隔开
```
设置key

    set keyname keyvalue

取String类型key的值

    get keyname
取List类型key的值

    lrange kenanme 0 -1 #0,-1是起始位置

删除

    del key

批量删除

    ./redis-cli keys "a-*" | xargs ./redis-cli del