---
title: redis增删改查----控制台
date: 2018-07-10 21:09:20
tags: redis
---
```
### 进入redis控制台
redis-cli --raw    #加上raw,防止中文乱码

### 增
127.0.0.1:6379> LPUSH list0 "hello" #增加一个list
1
127.0.0.1:6379> LRANGE list0 0 -1 #查看list
hello

### 删
127.0.0.1:6379> DEL list0 #删除list
1
127.0.0.1:6379> LRANGE list0 0 -1 #删除结果

### 查
127.0.0.1:6379> keys list0 #查找一下

127.0.0.1:6379> LPUSH list0 "hello"
1

#### 改
## 修改list--增加元素
127.0.0.1:6379> LRANGE list0 0 -1 
hello
127.0.0.1:6379> LPUSH list0 world
2
127.0.0.1:6379> LRANGE list0 0 -1
world
hello

## 修改list--删了重建
127.0.0.1:6379> DEL list0 fuck
1
127.0.0.1:6379> LRANGE list0 0 -1

127.0.0.1:6379> LPUSH list hello
1
127.0.0.1:6379> LRANGE list0 0 -1
```