---
title: kafka发布消息报错LEADER_NOT_AVAILABLE
date: 2018-07-10 21:09:19
tags: kafka
---
- #### 报错信息

```
$ bin/kafka-console-producer.sh --broker-list="192.168.1.100:32785" --topic test
ssss
[2016-05-11 11:21:42,527] WARN Error while fetching metadata with correlation id 0 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:42,625] WARN Error while fetching metadata with correlation id 1 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:42,727] WARN Error while fetching metadata with correlation id 2 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:42,829] WARN Error while fetching metadata with correlation id 3 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:42,931] WARN Error while fetching metadata with correlation id 4 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,033] WARN Error while fetching metadata with correlation id 5 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,135] WARN Error while fetching metadata with correlation id 6 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,237] WARN Error while fetching metadata with correlation id 7 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,339] WARN Error while fetching metadata with correlation id 8 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,441] WARN Error while fetching metadata with correlation id 9 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,543] WARN Error while fetching metadata with correlation id 10 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,645] WARN Error while fetching metadata with correlation id 11 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,747] WARN Error while fetching metadata with correlation id 12 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,849] WARN Error while fetching metadata with correlation id 13 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:43,951] WARN Error while fetching metadata with correlation id 14 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:44,053] WARN Error while fetching metadata with correlation id 15 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:44,155] WARN Error while fetching metadata with correlation id 16 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:44,257] WARN Error while fetching metadata with correlation id 17 : {test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2016-05-11 11:21:44,359] WARN Error while fetching metadata with correlation 
```

- #### 1.修改server.properties
```
vim config/server.properties 
#注释打开并把值修改成hsot

# Hostname the broker will advertise to producers and consumers. If not set, it uses the
# value for "host.name" if configured.  Otherwise, it will use the value returned from
# java.net.InetAddress.getCanonicalHostName().
advertised.host.name=hs03
```
- #### 2.查看集群是否有broker没有运行
```
#进入zookeeper客户端
zookeeper-shell.sh hs01:2181,hs02:2181,hs03:2181
#查看状态
ls /brokers/ids
[3, 2, 0]
```
如果少broker重新启动
