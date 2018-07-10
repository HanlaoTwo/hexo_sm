---
title: JAVA语法
date: 2018-07-10 21:09:19
tags: Java
---
#### 1. if 和 else if

```
else if(){}
```
如果有满足条件的就会跳出，不执行其他的else if
```
if(){}
```
会连续判断，直到结束
#### 2. if else 和 switch
> if else(){} 的空间效率高

> switch的时间效率高
==空间换时间==

#### 3.param = new Object()和param = null
> param = new Object() 会初始化，真实存在

> param = null 参数为空，不存在

#### 4.Variable expected
[Variable expected error](http://stackoverflow.com/questions/31797631/variable-expected-error)

map.get(key) = new Value();

#### 5.assert
[assertion(断言)](http://www.cnblogs.com/wardensky/p/4307848.html)
assertion就是在程序中的一条语句，它对一个boolean表达式进行检查，一个正确程序必须保证这个boolean表达式的值为true；如果该值为false，说明程序已经处于不正确的状态下，系统将给出警告并且退出。

用法：
```
1. assert expression1;
2. assert expression1: expression2;
```
expression1表示一个boolean表达式，expression2表示一个基本类型、表达式或者是一个Object，用于在失败时输出错误信息。

#### 6.Java修饰符
public/private/protected

#### 7.Java 集合类

#### 8. Object o = new Object()
o.toString()和（String）o的区别
#### 9.Java枚举类
[lianjie](http://www.cnblogs.com/zhaoyanjun/p/5659811.html)

#### 10.@SuppressWarnings
J2SE 提供的最后一个批注是 @SuppressWarnings。该批注的作用是给编译器一条指令，告诉它对被批注的代码元素内部的某些警告保持静默。 
@SuppressWarnings 批注允许你选择性地取消特定代码段（即，类或方法）中的警告。其中的想法是当您看到警告时，您将调查它，如果你确定它不是问题，就可以添加一个 @SuppressWarnings 批注，以使您不会再看到警告。虽然它听起来似乎会屏蔽潜在的错误，但实际上它将提高代码安全性，因为它将防止对警告无动于衷 — 看到的每一个警告都将值得注意。
[来自百度知道](https://zhidao.baidu.com/question/297231941.html)

[可屏蔽内容](http://blog.csdn.net/mddy2001/article/details/8291484)