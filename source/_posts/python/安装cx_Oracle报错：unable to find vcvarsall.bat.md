---
title: 安装cx_Oracle报错：unable to find vcvarsall.bat
date: 2018-07-10 21:09:19
tags: python
---
#### 环境：
> Python3.5
>
> vs 2008

#### 报错：
> unable to find vcvarsall.bat

#### 原因：

*python的distutils模块中的msvc9compiler.py并不从环境变量指定的路径中寻找’vcvarsall.bat’，而是通过注册表来寻找…，然而，不知为什么编译器安装过程没有配置注册表。*

#### 解决办法：

网上有很多，但是都不能很快解决。

## **终极牛逼方案：*安装最新版***
> python -m pip install cx_Oracle --pre