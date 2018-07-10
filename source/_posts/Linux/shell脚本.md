---
title: shell脚本
date: 2018-07-10 21:09:19
tags: Linux
---
```
#!/usr/bin/env bash
cd /root/software/tag
#删除文件
echo "开始删除文件"
hadoop fs -rm -R input/basic

echo "可运行的程序有: "
for program in Adapter Adpaterfour hello hhaha lallal;
do
    echo "${program}"
done

echo "输入要运行的程序,默认为Adapter"
while read var
do
if [ "$var" == "" ]
then
    nohup hadoop jar tag-0.0.1-jar-with-dependencies.jar com.hs.tag.jobflow.Adapter  --start_date=20170109 --end_date=20170109>adapterlog.log 2>&1 &
    echo "开始运行adapter程序，可以看日志了"
    break
else
    nohup hadoop jar tag-0.0.1-jar-with-dependencies.jar com.hs.tag.jobflow.${var}  --start_date=20170515 --end_date=20170515>adapterlog.log 2>&1 &
    echo "开始运行${var}程序，可以看日志了"
    break
fi
done


```