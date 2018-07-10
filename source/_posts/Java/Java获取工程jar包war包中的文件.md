---
title: Java获取工程jar包war包中的文件
date: 2018-07-10 21:09:19
tags: Java
---
#### 1.相对路径有问题
工程目录如图：

--
用相对路径的方法可以获取跟src同一目录下的js文件
```
//scripts前不要加   “/”
        FileReader file = 
        new FileReader("scripts/textchat.js");
        

```
但是这样打包之后会找不到文件
#### 2.使用反射
把文件放在resource目录下

用反射获取类文件编译后所在目录

然后用获取到的路径+相对路径获取文件

测试类
```
public class paths {

    public static void main(String args[]) throws FileNotFoundException {
    
        //下面三种方法都可以获取相对路径
        System.out.println(paths.class.
        getResource("/").
        getPath());
        
        System.out.println(paths.class.
        getResource("").
        getPath());
        
        System.out.println(paths.class.
        getClassLoader().getResource("").
        getPath());
        
        //获取文件
        FileReader file = 
        new FileReader(paths.class.
        getResource("/").
        getPath()+"scripts/textchat.js");
    }
}
```
这样在打包之后就可以访问想要的文件了。