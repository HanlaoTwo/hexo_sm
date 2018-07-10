---
title: 设计模式--MVVM
date: 2018-06-18 16:04:15
tags: note
---
### 1.关联模式
> #### MVC

- 视图（View）：用户界面。 
- 控制器（Controller）：业务逻辑
- 模型（Model）：数据保存

View 传送指令到 Controller

Controller 完成业务逻辑后，要求 Model 改变状态

Model 将新的数据发送到 View，用户得到反馈




> #### MVP

- Model 提供数据
- View 负责显示
- Presenter 负责逻辑的处理

各部分之间的通信，都是双向的。

View 与 Model 不发生联系，都通过 Presenter 传递。

View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而Presenter非常厚，所有逻辑都部署在那里。

---
### 2.MVVM
- Model 提供数据
- View 负责显示
- ViewModel 处理用户输入，反馈数据变化

[比如AngualrJS](http://baidu.com/)

MVVM与MVP最大的不同就在于View与ViewModel交互的时候使用了松耦合的双向绑定，而不是像View与Presenter那样直接交互。ViewModel作为View的数据映射，通常View上有什么属性，ViewModel上也会存在相应的一个属性，这两个属性通过事件实现了双向的绑定，常见的MVVM框架都替我们完成了这样的绑定过程。 