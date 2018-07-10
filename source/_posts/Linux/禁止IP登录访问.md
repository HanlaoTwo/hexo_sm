---
title: 禁止IP登录访问
date: 2018-07-10 21:09:19
tags: Linux
---
对于能过xinetd程序启动的网络服务，比如ftp telnet，我们就可以修改/etc/hosts.allow和/etc/hosts.deny的配制，来许可或者拒绝哪些IP、主机、用户可以访问。

比如我们在 /etc/hosts.allow中加入

    all:218.24.129.

这样就会允许来自218.24.129.*域的所有的客户来访问。这只是举个例子，实际上，系统默认状态 下，都是能用这些网络服的

如果我们在 /etc/hosts.deny中加入，就限制了来自218.24.129.*域的所有的所有的IP。

    all:218.24.129.

如果我们在 /etc/hosts.deny中加入

    all:218.24.129.134

这样就限制了所有在218.24.129.134中的所有的用户的访问。

当hosts.allow和 host.deny相冲突时，以hosts.allow设置优化。

设置好后，要重新启动
```
/etc/rc.d/init.d/xinetd restart
/etc/rc.d/init.d/network restart
```
 

不是任何服务程序都能使用TCP_wrappers的，例如使用命令ldd /usr/sbin/sshd，如果输出中有libwrap，则说明可以使用TCP_wrappers, 即该服务可以使用/etc/hosts.allow和/etc/hosts.deny,如果输出没有libwrap则不可使用

```
vi /etc/hosts.deny
#
# hosts.deny    This file contains access rules which are used to
#               deny connections to network services that either use
#               the tcp_wrappers library or that have been
#               started through a tcp_wrappers-enabled xinetd.
#
#               The rules in this file can also be set up in
#               /etc/hosts.allow with a 'deny' option instead.
#
#               See 'man 5 hosts_options' and 'man 5 hosts_access'
#               for information on rule syntax.
#               See 'man tcpd' for information on tcp_wrappers
#
all:218.24.129.134
all:59.63.166.81
#all:114.67.147.214
```