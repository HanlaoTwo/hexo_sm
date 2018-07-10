---
title: zookeeper客户端查看kafka配置
date: 2018-07-10 21:09:19
tags: kafka
---
- #### 连接
```
#连接
zookeeper-shell.sh hs01:2181,hs02:2181,hs03:2181

Connecting to hs01:2181,hs02:2181,hs03:2181
Welcome to ZooKeeper!
JLine support is disabled

WATCHER::

WatchedEvent state:SyncConnected type:None path:null

```
- #### 命令
```
    connect host:port
	get path [watch]
	ls path [watch]
	set path data [version]
	rmr path
	delquota [-n|-b] path
	quit 
	printwatches on|off
	create [-s] [-e] path data acl
	stat path [watch]
	close 
	ls2 path [watch]
	history 
	listquota path
	setAcl path acl
	getAcl path
	sync path
	redo cmdno
	addauth scheme auth
	delete path [version]
	setquota -n|-b val path
```
- #### ls [path]
```
ls /
[hs_jstorm, consumers, hive_zookeeper_namespace_hive, latest_producer_id_block, rmstore, yarn-leader-election, controller_epoch, isr_change_notification, admin, zookeeper, cluster, config, controller, brokers]

#查看broker的id
ls /brokers/ids
[3, 2, 0]

#查看消息
ls /brokers/topics
[new, __consumer_offsets, test, uf20, hahahhaahh, testfile, accountPosition, testFile]

#查看删除的消息
ls /admin/delete_topics
[account]
```
- #### get [path]
```
#查看broker的信息
get /brokers/ids/0
{"jmx_port":-1,"timestamp":"1516184048700","endpoints":["PLAINTEXT://hs01:9092"],"host":"hs01","version":2,"port":9092}
cZxid = 0x29000048b2
ctime = Wed Jan 17 18:14:08 CST 2018
mZxid = 0x29000048b2
mtime = Wed Jan 17 18:14:08 CST 2018
pZxid = 0x29000048b2
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x261033b8886032a
dataLength = 119
numChildren = 0
```
- #### rmr [path]
```
#删除消息
rmr /brokers/topics/test
rmr /admin/delete_topics/test
```