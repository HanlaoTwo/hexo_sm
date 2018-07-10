---
title: git把本地项目push到远程仓库
date: 2018-07-10 21:09:19
tags: 开发工具
---

#### 环境

系统：windows

目录：D:/workspace/idea/spark-test

远程仓库：https://github.com/HanlaoTwo/SparkStudy.git

协议：https

#### 创建版本库

```
#初始化
git init

Reinitialized existing Git repository in D:/workspace/idea/spark-test/.git/

#用命令git add告诉Git，把文件添加到仓库：
git add *
warning: LF will be replaced by CRLF in src/main/scala/sql/SparkSQLExample.scala.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/compiler.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/encodings.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/misc.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/modules.xml.
...

#提交
git commit -m "all is new"
[master (root-commit) 521cf14] all is new
warning: LF will be replaced by CRLF in .idea/compiler.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/encodings.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/misc.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/modules.xml.
```
#### 提交到远程仓库
```
#添加
git remote add origin https://github.com/HanlaoTwo/SparkStudy.git
#报错，已存在
fatal: remote origin already exists.

#删除
git remote rm origin
#再添加
git remote add origin https://github.com/HanlaoTwo/SparkStudy.git

#提交
git push -u origin master
Username for 'https://github.com': hanlaotwo
Password for 'https://hanlaotwo@github.com':
Counting objects: 294, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (279/279), done.
Writing objects:  99% (292/294), 1.10 MiB | 68.00 KiB/s

```