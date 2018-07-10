---
title: 安装Hive，本地模式
date: 2018-07-10 21:09:19
tags: Linux
---
- #### 环境
> CentOS6.5

> jdk1.8

> MySQL5.6

> Hadoop2.7

mysql要用原生的若果是centOS会自带MariaDB，不要用。

[CentOS上MySQL安装]()
- #### 安装hive
下载hive压缩包

解压

然后放到一个单独的目录下（不放也行）

```
wget url
tar -zxvf   apache-hive-2.2-bin.tar.gz
mv apache-hive-2.2-bin hive
```
不用编译，然后配置就好了

- #### 配置hive
- ##### 环境变量
```
vim /etc/profile
#在最后加上下面内容，第一行是hive的绝对路径
export HIVE_HOME=/usr/hive
export PATH=$HIVE_HOME/bin:$HIVE_HOME/conf:$PATH
#编辑好后保存
：wq
#保存环境变量
source /etc/profile
```
- ##### MySQL
这里假装MySQL已经装好了

新建一个用户hive,密码为000000。然后新建库hive，这些配置在hive-site.xml中会用到。
```
mysql -u root -p #进入MySQL
#配置如下
CREATE USER 'hive'@'localhost' IDENTIFIED BY '000000';
grant all privileges on *.* to 'hive'@'localhost' identified by 'hive';
flush privileges;
```
- ##### 配置驱动程序
需要把MySQL驱动的jar包下载下来然后放到hive的lib目录下。
```
wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.39.tar.gz
tar -zxvf mysql-connector-java-5.1.39.tar.gz # 解压
cp mysql-connector-java-5.1.39/mysql-connector-java-5.1.39-bin.jar /usr/hive/lib
```
- ##### 配置hive-site.xml

到hive的安装目录。目录里是没有hive-site.xml的，但是有模板，把模板复制到hive-site.xml中。然后进行编辑。

模板中内容很多，但是需要改的地方只有几个。所以需要查找内容再修改。最好把文件下载到本地改好再放回。

在修改之前要先建一个临时文件目录，配置的时候会用到。这里是
> mkdir /usr/Hadoop/hive/iotmp

```
cd conf   #切换到配置目录下
cp hive-default.xml.template hive-site.xml    #复制一份
vim hive-site.xml     #修改
```
需要修改的地方如下（修改的内容在文件中不是连续的，要找全）：
```
 <!-- 数据库地址 -->
<property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://localhost:3306/hive</value>
    <description>JDBC connect string for a JDBC metastore</description>
</property>
 <!-- 数据库连接驱动 -->
<property>
   <name>javax.jdo.option.ConnectionDriverName</name>
   <value>com.mysql.jdbc.Driver</value>
   <description>Driver class name for a JDBC metastore</description>
</property>
 <!-- 数据库名字-->
<property>
   <name>javax.jdo.option.ConnectionUserName</name>
   <value>hive</value>
   <description>Username to use against metastore database</description>
</property>
 <!-- 数据库密码 -->
<property>
   <name>javax.jdo.option.ConnectionPassword</name>
   <value>000000</value>
   <description>password to use against metastore database</description>
</property>
 <!-- 下面--四个---的配置都是临时存储目录，自己新建然后填上绝对路径-->
<property>
    <name>hive.exec.local.scratchdir</name>
    <value>/usr/Hadoop/hive/iotmp</value>
    <description>Local scratch space for Hive jobs</description>
  </property>
<property>
    <name>hive.downloaded.resources.dir</name>
    <value>/usr/Hadoop/hive/iotmp</value>
    <description>Temporary local directory for added resources in the remote file system.</description>
</property>
<property>
    <name>hive.server2.logging.operation.log.location</name>
    <value>/usr/Hadoop/hive/iotmp</value>
    <description>Top level directory where operation logs are stored if logging functionality is enabled</description>
</property>
<property>
    <name>hive.querylog.location</name>
    <value>/usr/Hadoop/hive/iotmp</value>
    <description>Location of Hive run time structured log file</description>
</property>
```
- ##### 配置hive-env.sh
hive-env也要从模板复制过去然后修改。

赋值之后打开，要修改的内容被注释掉了可以打开注释修改也可以直接在末尾添加内容。
```
cp hive-env.sh.template hive-env.sh    #复制
vim hive-env  #打开
#在末尾添加下面内容

# Hadoop的目录
HADOOP_HOME=/usr/hadoop

# hive的配置文件目录
export HIVE_CONF_DIR=/usr/hive/conf

：wq #保存退出
```
- ##### 新建元数据sechme（这个单词还不知道怎么翻译）
切换到hive的bin目录下，然后新建元数据sechme.
这里名字要和mysql对应
```
cd /usr/hive/bin
#新建
./schematool -initSchema -dbType mysql
```
- #### 启动hive
启动Hadoop
启动MySQL
启动hive
在控制台输入hive
出现下面输出
```
Logging initialized using configuration in jar:file:/usr/Hadoop/hive/hive/lib/hive-common-2.0.1.jar!/hive-log4j2.properties
Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. tez, spark) or using Hive 1.X releases.
hive> 
```
然后输入show tables;不报错就是安装好了。
```
hive> show tables;
OK
Time taken: 2.42 seconds
hive>
```