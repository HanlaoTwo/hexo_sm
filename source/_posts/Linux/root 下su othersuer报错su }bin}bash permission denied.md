---
title: root 下su othersuer报错su }bin}bash permission denied
date: 2018-07-10 21:09:19
tags: Linux
---
原因是su这个命令在执行的时候会调用其他目录下的程序

如果修改了某个可能被调用的目录权限，比如

    chmod 750 /*
再调用su命令的时候就会报错了

因为不知道具体是哪个目录的权限问题所以最简单的解决的方法是

    chmod 755 /*