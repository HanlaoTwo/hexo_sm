---
title: conda操作
date: 2018-07-10 21:09:19
tags: 开发工具
---
#### 管理python
创建一个名为python34的环境，指定Python版本是3.4（不用管是3.4.x，conda会为我们自动寻找3.4.x中的最新版本）  

    condacreate--namepython34python=3.4  
  
安装好后，使用activate激活某个环境 

    activatepython34# for Windows  
    sourceactivatepython34# for Linux & Mac  
激活后，会发现terminal输入的地方多了python34的字样，实际上，此时系统做的事情就是把默认2.7环境从PATH中去除，再把3.4对应的命令加入PATH  
  
此时，再次输入  

    python--version  
可以得到`Python 3.4.5 :: Anaconda 4.1.1 (64-bit)`，即系统已经切换到了3.4的环境  
  
如果想返回默认的python 2.7环境，运行  

    deactivatepython34# for Windows  
    sourcedeactivatepython34# for Linux & Mac  
  
复制一个环境  

    conda create -n pyhon34 --clone python34clone  
删除一个已有的环境  

    condaremove--namepython34--all  
 为了确定这个环境已经被移除，输入以下命令  

    conda info -e  

#### 管理包
查看当前环境下已安装的包  

    condalist  
  
查看某个指定环境的已安装包  

    condalist-npython34  
  
查找package信息  

    condasearchnumpy  
  
安装package  

    condainstall-npython34numpy  
如果不用-n指定环境名称，则被安装在当前活跃环境   也可以通过-c指定通过某个channel安装  
  
更新package  

    condaupdate-npython34numpy  
  
删除package  
    
    condaremove-npython34numpy  