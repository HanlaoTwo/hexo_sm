---
title: Python上传本地文件到Linux指定目录
date: 2018-06-18 16:04:15
tags: note
---
```
import paramiko

#服务器信息
IP = '10.0.0.1'
USER = 'root'
PASSWORD = '000000'

#文件信息
file_update = 'hello.js'
REMORE_PATH = '/usr/test/'
LOCAL_PATH = 'textchat.js'
cmd_rm = 'rm '+REMORE_PATH+file_update

#删除
s = paramiko.SSHClient()
s.set_missing_host_key_policy(paramiko.AutoAddPolicy())
s.connect(hostname=IP, username=USER, password=PASSWORD)
out_rm = s.exec_command(cmd_rm)
s.close

#上传
t = paramiko.Transport((IP,22))
t.connect(username=USER,password=PASSWORD)
s = paramiko.SFTPClient.from_transport(t)
s.put(LOCAL_PATH,REMORE_PATH+file_update)
t.close
```