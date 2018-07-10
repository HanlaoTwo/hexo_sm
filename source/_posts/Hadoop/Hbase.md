---
title: Hbase
date: 2018-07-10 21:09:19
tags: Hadoop
---
Hbase介绍[链接](http://blog.csdn.net/frankiewang008/article/details/41965543)

白话MySQL(RDBMS)与HBase之间

![image](C:\Users\hanqian18790\Desktop\clipboard.png)


原来系统中有2张表blogtable和comment表，采用HBase后只有一张blogtable表，如果按照传统的RDBMS的话，blogtable表中的列是固定的，比如schema 定义了Author,Title,URL,text等属性，上线后表字段是不能动态增加的。但是如果采用列存储系统，比如Hbase，那么我们可以定义blogtable表，然后定义info 列族，User的数据可以分为：info:title ,info:author ,info:url 等，如果后来你又想增加另外的属性，这样很方便只需要 info:xxx 就可以了。

对于Row key你可以理解row key为传统RDBMS中的某一个行的主键，Hbase是不支持条件查询以及Order by等查询，因此Row key的设计就要根据你系统的查询需求来设计了额。 Hbase中的记录是按照rowkey来排序的，这样就使得查询变得非常快。

具体操作过程如下：

创建blogtable表

 create 'blogtable', 'info','text','comment_title','comment_author','comment_text'
  
插入概要信息

 put 'blogtable', '1', 'info:title', 'this is doc title'
 put 'blogtable', '1', 'info:author', 'javabloger'
 put 'blogtable', '1', 'info:url', 'http://www.javabloger.com/index.php'
 
 put 'blogtable', '2', 'info:title', 'this is doc title2'
 put 'blogtable', '2', 'info:author', 'H.E.'
 put 'blogtable', '2', 'info:url', 'http://www.javabloger.com/index.html'
 
插入正文信息

 put 'blogtable', '1', 'text:', 'what is this doc context ?'
 put 'blogtable', '2', 'text:', 'what is this doc context2?'
 
插入评论信息

 put 'blogtable', '1', 'comment_title:', 'this is doc comment_title '
 put 'blogtable', '1', 'comment_author:', 'javabloger'
 put 'blogtable', '1', 'comment_text:', 'this is nice doc'
 
 put 'blogtable', '2', 'comment_title:', 'this is blog comment_title '
 put 'blogtable', '2', 'comment_author:', 'H.E.'
 put 'blogtable', '2', 'comment_text:', 'this is nice blog' 

HBase的数据查询\读取，可以通过单个row key访问，row key的range和全表扫描,大致如下：
注意：HBase不能支持where条件、Order by 查询，只支持按照Row key来查询，但是可以通过HBase提供的API进行条件过滤。
例如：http://hbase.apache.org/apidocs/org/apache/hadoop/hbase/filter/ColumnPrefixFilter.html

scan 'blogtable' ,{COLUMNS => ['text:','info:title'] } —> 列出 文章的内容和标题

scan 'blogtable' , {COLUMNS => 'info:url' , STARTROW => '2'} —> 根据范围列出 文章的内容和标题

get 'blogtable','1' —> 列出 文章id 等于1的数据

get 'blogtable','1', {COLUMN => 'info'} —> 列出 文章id 等于1 的 info 的头(Head)内容

get 'blogtable','1', {COLUMN => 'text'} —> 列出 文章id 等于1 的 text 的具体(Body)内容

get 'blogtable','1', {COLUMN => ['text','info:author']} —> 列出 文章id 等于1 的内容和作者(Body/Author)内容