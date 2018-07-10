---
title: sqlite3报错
date: 2018-07-10 21:09:19
tags: python
---

我自己装了python3.5，但在导入sqlite3这个包的时候出现找不到包的错误。

下面给出解决方法

检查自己有没有安装sqlite-devel，没有的话yum -y install sqlite-devel

然后进入到Python目录，（cd python目录）

然后命令行输入./configure，然后make和make  install

这个时候可以输入python，进入python环境后，import sqlite3，

