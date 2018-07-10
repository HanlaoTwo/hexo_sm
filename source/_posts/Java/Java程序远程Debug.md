---
title: Java程序远程Debug
date: 2018-07-10 21:09:19
tags: Java
---
#### 0.环境
远程服务器（本地也可以应该）

远程服务器JDK环境

本地IDE（这里是idea）
#### 1.准备程序
先准备一个要远程debug的程序，这里新建一个test工程，并导出jar包。比如一个名叫Test的jar文件
#### 2.远程启动
把包放到远程服务器的目录下


终端输入命令
```
 java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address="8000" -jar 
 ```
 终端返回下面结果说明卡伊开始debug了
 ```
 Listening for transport dt_socket at address: 8000
 ```
 如图：
 ![image](C:\Users\hanqian18790\Desktop\youdaoIMG\QQ截图20170523195051.png)
#### 3.本地启动
ide上配置远程，

点击Eidt Cnfigration

idea配置如下：
![image](C:\Users\hanqian18790\Desktop\youdaoIMG\remotedebug_local.png)

#### 4.参数说明
远程调试时的一些VM参数说明如下：
header 1 | header 2
---|---
-XDebug             |  启用调试。 
-Xnoagent            |禁用默认sun.tools.debug调试器。 
-Djava.compiler=NONE| 禁止 JIT 编译器的加载。 
-Xrunjdwp           | 加载JDWP的JPDA参考执行实例。 
transport            | 用于在调试程序和 VM 使用的进程之间通讯。 
dt_socket            | 套接字传输。 
dt_shmem             | 共享内存传输，仅限于 Windows。
server=y/n           | VM是否需要作为调试服务器执行。
address        | 调试服务器的端口号，客户端用来连接服务器的端口号。 
suspend=y/n          | 是否在调试客户端建立连接之后启动 VM 。 


