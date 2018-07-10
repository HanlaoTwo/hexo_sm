---
title: shadowsocks
date: 2018-07-10 21:09:19
tags: python
---
[连接](https://github.com/ziggear/shadowsocks)

systemctl stop firewalld.service #停止firewall

systemctl disable firewalld.service
#禁止firewall开机启动
```
yum install python-setuptools && easy_install pip

pip install shadowsocks

ssserver -c /etc/shadowsocks.json -d start

/etc/shadowsocks.json
```

```
{
    "server":"my_server_ip",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"mypassword",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```