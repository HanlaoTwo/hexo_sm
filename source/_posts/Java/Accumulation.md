---
title: Accumulation
date: 2018-07-10 21:09:19
tags: Java
---
#### 读property文件
[链接](http://shmilyaw-hotmail-com.iteye.com/blog/1899242)

代码：
```
public class IOExample {
    public static void main(String[] args) {
        Properties prop = new Properties();

        try {
            prop.load(new FileInputStream("input/config/database.properties"));

            System.out.println(prop.getProperty("oracle.output.url"));
        } catch(IOException e) {
            e.printStackTrace();
        }
    }

----------------------------------------------
public class NewApp {  
    public static void main(String[] args) {  
        Properties prop = new Properties();  
          
        try {  
            prop.load(NewApp.class.getClassLoader().getResourceAsStream("config.properties"));  
              
            System.out.println(prop.getProperty("database"));  
            System.out.println(prop.getProperty("dbuser"));  
            System.out.println(prop.getProperty("dbpassword"));  
        } catch(IOException e) {  
            e.printStackTrace();  
        }  
    }  
}  
```