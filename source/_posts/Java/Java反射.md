---
title: Java反射
date: 2018-07-10 21:09:19
tags: Java
---
### 1. 反射
正常情况下都是通过一个类去实例化一个对象，通过一个对象找到一个类的名称，地址，方法等类信息时用到的机制就是反射
#### 一个简单的栗子：
```
package com.learn.controller;

public class Fanshe {

    public static void main(String[] args){
        testFanshe ts = new testFanshe();
        System.out.println(
                ts.getClass().getName()
        );
    }

}
class testFanshe{}
```     
运行结果如下：
> com.learn.controller.testFanshe

### 2. 反射原理
- ##### Object类
   object类是Java中所有类的父类。
> 一切操作都是用Object类完成，类、数组的引用都可以使用Object类接收

Object类的方法如下

![image](C:\Users\hanqian18790\Desktop\object.png)
- ##### Class类
所有对象都是Class类的实例
使用反射机制就要先获取Class类的实例

实例化Class类的方法：

1.对象.class

2.对象.getClass()

3.Class.forName(包名.类名)  ---------//更具灵活性，不用使用一个对象的实例只要知道类名和路径

实例化Class类后就可以使用Class类中的方法进行反射操作了

一些方法如下:

![imge](C:\Users\hanqian18790\Desktop\getClass.png)

### 3. 反射的应用

#### 1).实例化Class后可以通过具体类的构造方法实例化一个具体对象
```
package com.learn.controller;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class Fanshe {
    public static void main(String[] args) throws 
            NoSuchMethodException, 
            IllegalAccessException, 
            InstantiationException, 
            InvocationTargetException {

        Class<?> c = null;
        try {
            c = Class.forName("com.learn.controller.testFanshe");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        testFanshe TS0 = (testFanshe) c.newInstance();          //需要有无惨构造方法
        Constructor<?>[] cons = c.getConstructors();            //返回所有构造方法
        testFanshe TS1 = (testFanshe) cons[0].newInstance();    //newInstance()可以传入参数，如果有需要参数的构造方法的话

    }

}

class testFanshe {
}
```



#### 2). 反射还可以：
```
Class<?>[] interfaces = c.getInterfaces();              //取得所有接口
Class<?> superclass = c.getSuperclass();                //取得父类
Method[] methods = c.getMethods();                      //取得方法
Field[] fields = c.getFields();                         //取得全部属性
```
#### 3). 还可以获取类，接口，属性，方法的修饰符，入参，入参类型。。。