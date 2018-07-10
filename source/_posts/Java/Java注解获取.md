---
title: Java注解获取
date: 2018-07-10 21:09:19
tags: Java
---
### java 注解
[注解见另一篇笔记](http://blog.csdn.net/boomhankers/article/details/70768349)

##### 注解按保存范围阶段分类
先看一个栗子,下面是一个自定义的注解:

```
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface myAnnotation {
    String[] value();
```
@Retention()注解，表示这个自定义注解的保存范围

@Retention(RetentionPolicy.SOURCE)表示保存在源文件中

分类：
- ==*SOURCE*==:   此注解只会保存在源文件中，也就是.java文件，编译之后不会存在编译好的.class文件中
- *==CLASS==*:  默认范围 此注解会保留在源文件和编译后的文件中，但不会被加载到虚拟机中
- *==RUNTIME==*: 会保留在源文件和编译之后的文件中，运行时会被加载到JVM虚拟机中


### 获取注解

##### 某一个类中的注解
先通过反射机制获取类，然后获取指定的方法和方法的注解.

*这种方法要获取的注解一定要是运行时注解*
```
package com.learn.controller;

import java.lang.annotation.Annotation;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.reflect.Method;

import static java.lang.annotation.ElementType.*;

@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.RUNTIME)
public @interface Myanno {
    String value();
}

class Myanotaion {
    @Myanno("a method")
    @Override
    public String toString(){
        return "llalal";
    }
}
class GetAnno{
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException {
        Class<?> c = Class.forName("com.learn.controller.Myanotaion");
        Method methods = c.getMethod("toString");
        Annotation annos[] = methods.getAnnotations();
        Annotation myanno = methods.getAnnotation(Myanno.class);
        System.out.println(myanno);
        System.out.println(annos[0]);
    }
}
```
>   methods.getAnnotations();是获取所有注解
>
>   methods.getAnnotation(Myanno.class);是获取指定注解



###### 获取编译阶段的注解
编译时注解指的是@Retention的值为CLASS的注解

自定义类继承 AbstractProcessor类；

重写其中的 process 函数。

编译器在编译时会自动查找所有继承自 AbstractProcessor 的类，然后调用他们的 process 方法。

[注解获取方式](http://www.open-open.com/lib/view/open1423471786764.html)

###### 获取运行时注解