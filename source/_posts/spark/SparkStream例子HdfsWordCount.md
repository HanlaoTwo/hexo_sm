---
title: SparkStream例子HdfsWordCount
date: 2018-07-10 21:09:19
tags: spark
---
#### spark github上的例子
#### 程序描述

 计算给定目录下的新文件的单词个数
 
 运行的时候在hdfs上设置一个目录
 
 然后实时的往目录里放文件
 
 程序可以文件中单词的个数
 #### 代码
```
package stream

import org.apache.spark.SparkConf
import org.apache.spark.streaming.{Seconds, StreamingContext}

object HdfsWordCount {

  def main(args: Array[String]) {
    //val args = Array("D:\\workspace\\idea\\spark-test\\data")//z这里是目录不是文件
    if (args.length < 1) {
      System.err.println("Usage: HdfsWordCount <directory>")
      System.exit(1)
    }

    StreamingExamples.setStreamingLogLevels()
    val sparkConf = new SparkConf().setAppName("sadsadas").setMaster("local")
    
    // 初始化
    val ssc = new StreamingContext(sparkConf, Seconds(10))
    
    // 创建输入流，然后计算新文件的单词个数
    val lines = ssc.textFileStream(args(0))
    val words = lines.flatMap(_.split(" "))
    val wordCounts = words.map(x => (x, 1)).reduceByKey(_ + _)
    
    //输出计算结果
    wordCounts.print()
    
    ssc.start()
    ssc.awaitTermination()
  }
}
// scalastyle:on println
```
#### 打包运行
mvn install 

程序包：
test-1.0.jar

程序主类：
stream.HdfsWordCount

参数:
hdfs上的目录

input

命令：

    spark-submit --class stream.HdfsWordCount --master yarn --deploy-mode cluster  test-1.0.jar input

#### 运行结果
 向hdfs的目录中放入新文件,文件hello.txt
 
    hadoop fs -put hello.text input
 运行结果
 
 ```
 -------------------------------------------
Time: 1513337720000 ms
-------------------------------------------
(input/pretreatment,1)
(Found,1)
(drwxr-xr-x,3)
(0,3)
(input/tables,1)
(11:16,2)
(,33)
(3,1)
(2017-12-04,2)
(-,3)
...

 ```
 