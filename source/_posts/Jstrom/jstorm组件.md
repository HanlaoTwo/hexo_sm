---
title: jstorm组件
date: 2018-07-10 21:09:19
tags: Jstrom
---
- #### topology    
一个JStorm任务

- #### spout   
spout代表输入的数据源，这个数据源可以是任意的，比如说kafka，DB，HBase，甚至是HDFS等，JStorm从这个数据源中不断地读取数据，然后发送到下游的bolt中进行处理。

- #### bolt    
bolt代表处理逻辑，bolt收到消息之后，对消息做处理（即执行用户的业务逻辑），处理完以后，既可以将处理后的消息继续发送到下游的bolt，这样会形成一个处理流水线（pipeline，不过更精确的应该是个有向图）；也可以直接结束。

- #### component   
spout 或者 bolt

- #### worker  
一个承载JStorm任务的进程。即为一个真正的操作系统执行进程，分布到一个集群的一台或者多台机器上并行执行。

- #### task    
执行pout和bolt的线程
每个spout和bolt都可以单独指定一个并行度(parallelism)，代表同时有多少个线程(task)来执行这个spout或bolt。

- #### 窗口    
在流式计算中我们经常需要以时间或者数据量将无界的数据划分成一份份有限的集合，然后以这个集合为维度进行操作。比如我们会计算过去1个小时交易额TOP 10的天猫卖家，这时我会按照交易事件发生的时间将交易事件划分成到某个事件集合当中去，每个集合的大小是1个小时，然后计算每一个集合的TOP10。在流式计算中，这类的集合通常我们称之为Window。

- #### [ack机制](http://120.25.204.125/ProgrammingGuide_cn/AdvancedUsage/Theory/Acker.html)     
JStorm的acker机制，能够保证消息至少被处理一次（at least once）。也就是说，能够保证不丢消息。这里就详细解析一下acker的实现原理。