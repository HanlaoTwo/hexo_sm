---
title: kafka删除消息
date: 2018-07-10 21:09:19
tags: kafka
---
- #### 如果设置了可删除直接命令删除
配置

server.properties

delete.topic.enable=true
```
#删除test
kafka-topics  --delete --zookeeper hs01:2181  --topic test
```
- #### zookeeper客户端删除
```
#进入客户端
./zookeeper-shell.sh hs01:2181

#删除
rmr /brokers/topics/test
rmr /admin/delete_topics/test
```

- #### kafka日志删除
找到日志目录
```
kafka
############################# Log Basics #############################

# A comma seperated list of directories under which to store log files
log.dirs=/opt/rt/kafka/kafka-logs

#删除
rm -rf /opt/rt/kafka/kafka-logs/test-0
```