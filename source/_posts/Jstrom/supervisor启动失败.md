---
title: supervisor启动失败
date: 2018-07-10 21:09:19
tags: Jstrom
---
在jstorm的安装目录下
```
cat conf/storm.yaml
 
jstorm.log.dir: /opt/rt/data/jstorm/logs
nimbus.host: 10.20.28.67
storm.local.dir: /opt/rt/data/jstorm/data
storm.zookeeper.root: /hs_jstorm
storm.zookeeper.servers: [hs01]
nimbus.childopts: -Xms2g -Xmx2g -Xmn768m -XX:SurvivorRatio=4 -XX:MaxTenuringThreshold=15 -XX:+UseConcMarkSweepGC -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=70 -XX:+HeapDumpOnOutOfMemoryError -XX:CMSMaxAbortablePrecleanTime=5000
```
备份，删除storm.local.dir下的文件，然后重启