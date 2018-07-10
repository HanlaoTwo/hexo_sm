---
title: hadoop 增加存储目录
date: 2018-07-10 21:09:19
tags: Hadoop
---
直接在cdh上配置

HDFS -> 配置 -> datanode ->DataNode 数据目录dfs.data.dir,dfs.datanode.data.dir

增加一个目录，不用提前创建


```
[root@hs03 dn]# hadoop fs -df -h
Filesystem           Size     Used  Available  Use%
hdfs://hs03:8020  854.0 G  291.8 G    337.7 G   34%

[root@hs03 dn]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/vg_dev023053-lv_root    295G  229G   52G  82% /
tmpfs                               16G     0   16G   0% /dev/shm
/dev/sda1                           477M   33M  419M   8% /boot
cm_processes                        16G   89M   16G   1% /opt/cm-5.7.1/run/cloudera-scm-agent/process

[root@hs03 dn]# hadoop fs -df -h
Filesystem           Size     Used  Available  Use%
hdfs://hs03:8020  859.7 G  291.8 G    343.5 G   34%
[root@hs03 dn]# 
```