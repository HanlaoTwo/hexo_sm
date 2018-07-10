---
title: find
date: 2018-07-10 21:09:19
tags: Linux
---

列出当前目录及子目录下所有文件和文件夹 

    find . 

在/home目录下查找以.txt结尾的文件名 

    find /home -name "*.txt" 

同上，但忽略大小写 

    find /home -iname "*.txt"

当前目录及子目录下查找所有以.txt和.pdf结尾的文件 

    find . \( -name "*.txt" -o -name "*.pdf" \) 或 find . -name "*.txt" -o -name "*.pdf" 

匹配文件路径或者文件 

    find /usr/ -path "*local*" 

基于正则表达式匹配文件路径 

    find . -regex ".*\(\.txt\|\.pdf\)$" 

同上，但忽略大小写 

    find . -iregex ".*\(\.txt\|\.pdf\)$" 

否定参数 

找出/home下不是以.txt结尾的文件 

    find /home ! -name "*.txt" 

根据文件类型进行搜索 

    find . -type 类型参数 

类型参数列表： 

f 普通文件 

l 符号连接 

d 目录 

c 字符设备 

b 块设备 

s 套接字 

p Fifo 基于目录深度搜索 

向下最大深度限制为

    3 find . -maxdepth 3 -type f 

搜索出深度距离当前目录至少2个子目录的所有文件 

    find . -mindepth 2 -type f 

根据文件时间戳进行搜索 

    find . -type f 时间戳 

UNIX/Linux文件系统每个文件都有三种时间戳：

访问时间（-atime/天，-amin/分钟）：用户最近一次访问时间。

修改时间（-mtime/天，-mmin/分钟）：文件最后一次修改时间。

变化时间（-ctime/天，-cmin/分钟）：文件数据元（例如权限等）最后一次修改时间。

搜索最近七天内被访问过的所有文件 

    find . -type f -atime -7 

搜索恰好在七天前被访问过的所有文件 

    find . -type f -atime 7 

搜索超过七天内被访问过的所有文件

    ...
    
来自: http://man.linuxde.net/find