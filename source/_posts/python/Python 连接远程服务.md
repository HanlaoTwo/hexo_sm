---
title: Python 连接远程服务
date: 2018-07-10 21:09:19
tags: python
---
## Python 连接远程服务器


#### 1.Python库：paramiko
  用来通过ssh协议连接远程服务器
  
 [ githuB文档](http://docs.paramiko.org/en/2.1/api/proxy.html)
  
  [使用示例](http://www.tuicool.com/articles/e2EFzy)
 
  [ssh详解](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)
  
```
import paramiko

#用户名和密码
USER = 'root'
PASSWORD = '000000'

#要更新的文件和路径
file_update = 'textchat.js'

cmd_mk = 'mkdir hq01'
cmd_rm = 'rm -r hq02'

IP = '192.168.207.132'

s = paramiko.SSHClient()
s.set_missing_host_key_policy(paramiko.AutoAddPolicy())
s.connect(hostname=IP, username=USER, password=PASSWORD)

out_rm = s.exec_command(cmd_rm)
out_mk = s.exec_command(cmd_mk)

s.close


REMORE_PATH = '/root/hq01/get.py'
LOCAL_PATH = 'get.py'


t = paramiko.Transport((IP,22))
t.connect(username=USER,password=PASSWORD)
s = paramiko.SFTPClient.from_transport(t)
s.put(LOCAL_PATH,REMORE_PATH)
t.close
```

#### 2.Python库：ConfigParser
用于读取配置文件（方便配置） 

[使用示例](http://www.pythontab.com/html/2014/pythonhexinbiancheng_1120/919.html)

#### 3.Python库 ftplib(自带)
用于实现ftp客户端

[使用示例](http://www.cnblogs.com/kaituorensheng/p/4480512.html)
  
  [ftp 详解](http://www.cnblogs.com/luoxn28/p/5585458.html)
  
  Linux中ftp的使用
  
  [链接](http://www.linuxidc.com/Linux/2015-12/126357.htm)