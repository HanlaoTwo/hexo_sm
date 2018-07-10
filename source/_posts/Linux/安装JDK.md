---
title: 安装JDK
date: 2018-07-10 21:09:19
tags: Linux
---
```
yum search java|grep jdk

ava-1.6.0-openjdk.x86_64 : OpenJDK Runtime Environment 
java-1.6.0-openjdk-demo.x86_64 : OpenJDK Demos 
java-1.6.0-openjdk-devel.x86_64 : OpenJDK Development Environment 
java-1.6.0-openjdk-javadoc.x86_64 : OpenJDK API Documentation 
java-1.6.0-openjdk-src.x86_64 : OpenJDK Source Bundle 
java-1.7.0-openjdk.x86_64 : OpenJDK Runtime Environment 
java-1.7.0-openjdk-demo.x86_64 : OpenJDK Demos 
java-1.7.0-openjdk-devel.x86_64 : OpenJDK Development Environment 
java-1.7.0-openjdk-javadoc.noarch : OpenJDK API Documentation 
java-1.7.0-openjdk-src.x86_64 : OpenJDK Source Bundle 
java-1.8.0-openjdk.x86_64 : OpenJDK Runtime Environme
...

yum install java-1.7.0-openjdk
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.metrocast.net
 * epel: epel.mirror.constant.com
 * extras: mirror.metrocast.net
 * updates: mirror.metrocast.net
Resolving Dependencies
--> Running transaction check
---> Package java-1.7.0-openjdk.x86_64 1:1.7.0.141-2.6.10.1.el7_3 will be installed
--> Processing Dependency: java-1.7.0-openjdk-headless = 1:1.7.0.141-2.6.10.1.el7_3 for package: 1:java-1.7.0-openjdk-1.7.0.141-2.6.10.1.el7_3.x86_64
--> Processing Dependency: xorg-x11-fonts-Type1 for package: 1:java-1.7.0-openjdk-1.7.0.141-2.6.10.1.el7_3.x86_64
--> Processing Dependency: libpulse.so.0(PULSE_0)(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.141-2.6.10.1.el7_3.x86_64
--> Processing Dependency: libpng15.so.15(PNG15_0)(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.141-2.6.10.1.el7_3.x86_64
```
安装完之后，默认的安装目录是在: /usr/lib/jvm/java-1.7.0-openjdk-1.7.0.75.x86_64 
```
vi /etc/profile 

#set java environment
JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-1.7.0.75.x86_64
JRE_HOME=$JAVA_HOME/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 

source /etc/profile 

java -versiob
```