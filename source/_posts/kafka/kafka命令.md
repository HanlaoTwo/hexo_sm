---
title: kafka命令
date: 2018-07-10 21:09:19
tags: kafka
---
查看topic

    kafka-topics.sh --list --zookeeper localhost:2181

查看某一topic下的消息

    kafka-console-consumer.sh --zookeeper localhost:2181 --topic account --from-beginning
    
删除topic
```
./zookeeper-shell.sh hs03:2181

rmr /brokers/topics/{topic_name}
rmr /admin/delete_topics/{topic_name}
```
创建消息

    kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
    
发送消息

    kafka-console-producer.sh --broker-list hs03:9092 --topic hh
    
查看topic信息
```
    kafka-topics.sh --describe  --zookeeper hs03:2181
    
    Topic:T1	PartitionCount:1	ReplicationFactor:1	Configs:
	Topic: T1	Partition: 0	Leader: 3	Replicas: 3	Isr: 3
    Topic:T2	PartitionCount:1	ReplicationFactor:1	Configs:
	Topic: T2	Partition: 0	Leader: 3	Replicas: 3	Isr: 3
    Topic:T3	PartitionCount:1	ReplicationFactor:1	Configs:
	Topic: T3	Partition: 0	Leader: 3	Replicas: 3	Isr: 3
```