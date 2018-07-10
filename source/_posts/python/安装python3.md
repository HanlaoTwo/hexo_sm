---
title: 安装python3
date: 2018-07-10 21:09:19
tags: python
---
wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz

 tar -zxvf Python-3.6.3.tgz
 
 yum install gcc
 
 ```
 Installed:
  gcc.x86_64 0:4.8.5-16.el7                                                                                                                                                                                       

Dependency Installed:
  cpp.x86_64 0:4.8.5-16.el7   glibc-devel.x86_64 0:2.17-196.el7   glibc-headers.x86_64 0:2.17-196.el7   kernel-headers.x86_64 0:3.10.0-693.2.2.el7   libmpc.x86_64 0:1.0.1-3.el7   mpfr.x86_64 0:3.1.1-4.el7  

Dependency Updated:
  glibc.x86_64 0:2.17-196.el7                      glibc-common.x86_64 0:2.17-196.el7                      libgcc.x86_64 0:4.8.5-16.el7                      libgomp.x86_64 0:4.8.5-16.el7                     

Complete!
 ```

yum install zlib zlib-devel

yum install openssl openssl-devel

vim Modules/Setup.dist
 ```
 
# Andrew Kuchling's zlib module.
# This require zlib 1.1.3 (or later).
# See http://www.gzip.org/zlib/
zlib zlibmodule.c -I$(prefix)/include -L$(exec_prefix)/lib -lz

# Interface to the Expat XML parser
#
# Expat was written by James Clark and is now maintained by a group of
 ```
 ./configure 
 
make && make install
 
ln -s /[path]/python3 python3
 