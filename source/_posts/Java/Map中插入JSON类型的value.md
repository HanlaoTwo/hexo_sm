---
title: Map中插入JSON类型的value
date: 2018-07-10 21:09:19
tags: Java
---
### 向一个map中插入JSON格式的value

如果直接用字符串拼接成json需要转译字符“\”,

比如：
```
 map.put("hello","{\"he\",\"llo\"}");
```

如果不加入转译字符就会报错，但是这样根据key取value的时候就会输出转译字符，如下：
```
{\"wor\":\"ld\"}"
```
为了能正常的输出JSON字符串需要把字符串转正json格式。

使用fastjson
```
JSON.toJSONString("{\"wor\":\"ld\"}")
```
代码：

```
package com.aha

import com.alibaba.fastjson.JSON;

import java.util.HashMap;
import java.util.Map;

/**
 * Created by han
 */
public class testJSON {
    public static void main(String[] args){
        Map<String,String> map = new HashMap<>();
        map.put("hello","{\"he\",\"llo\"}");
        map.put("world", JSON.toJSONString("{\"wor\":\"ld\"}"));
        for (String key : map.keySet()) {
            System.out.println(">>>>>>>>>>>>>"+map.get(key));
        }
    }
}

```
输出如下：
```
"{\"wor\":\"ld\"}"

{"he","llo"}
```