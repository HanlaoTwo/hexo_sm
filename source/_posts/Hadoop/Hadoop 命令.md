---
title: Hadoop 命令
date: 2018-07-10 21:09:19
tags: Hadoop
---

[官网](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)

credential
```
Usage: hadoop credential <subcommand> [options]
create alias [-provider provider-path] [-strict] [-value credential-value]
delete alias [-provider provider-path] [-strict] [-f]
list [-provider provider-path] [-strict]
```
例子

    hadoop credential list -provider jceks://file/tmp/test.jceks