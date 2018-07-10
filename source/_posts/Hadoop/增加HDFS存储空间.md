---
title: 增加HDFS存储空间
date: 2018-07-10 21:09:19
tags: Hadoop
---
- ### 查看存储空间
```
hadoop  fs -du -h /# 查看hdfs根目录下使用量
    
[root@hs03 yfzx]# hadoop fs -du -h /
759      2.2 K    /abc
7.3 K    21.8 K   /bigdata
549.3 M  1.6 G    /cdh
281.6 K  844.8 K  /data
0        0        /input
84       252      /position
25.2 M   75.7 M   /table
4.2 G    24.8 G   /tmp
50.3 G   153.9 G  /user
```
- ### 设置存储空间大小
Use dfs.datanode.du.reserved configuration value in

$HADOOP_HOME/conf/hdfs-site.xml 

for limiting disk usage.

```
  <property>
    <name>dfs.datanode.du.reserved</name>
    <!-- cluster variant -->
    <value>182400</value>
    <description>Reserved space in bytes per volume. Always leave this much space free for non dfs use.
    </description>
  </property>
```