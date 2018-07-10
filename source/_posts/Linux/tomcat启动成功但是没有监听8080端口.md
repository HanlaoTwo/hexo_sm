---
title: tomcat启动成功但是没有监听8080端口
date: 2018-07-10 21:09:19
tags: Linux
---
查看tomcat日志
```
cd tomcat/logs
cat catlina.out
```
错误如下：
```
/usr/lib/jvm/java-1.7.0-openjdk-1.7.0.75.x86_64/jre/bin/java: No such file or directory
```
原因：

Java虚拟机没有找到

控制台输入java有输出

直接安装jdk不配置环境变量输入java也会有输出

解决：

按照路径去找发现确实没有文件

重新设置环境变量，配置正确的jre路径，然后重启
