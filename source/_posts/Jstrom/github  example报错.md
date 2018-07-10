---
title: github  example报错
date: 2018-07-10 21:09:19
tags: Jstrom
---
注释掉 ==com.esotericsoftware.kryo.Kryo== 然后重新导入新包
```
import com.alibaba.jstorm.esotericsoftware.kryo.Kryo;
import com.alibaba.jstorm.esotericsoftware.kryo.Serializer;
import com.alibaba.jstorm.esotericsoftware.kryo.io.Input;
import com.alibaba.jstorm.esotericsoftware.kryo.io.Output;
import com.alipay.dw.jstorm.example.sequence.bean.Pair;

//import com.esotericsoftware.kryo.Kryo;
//import com.esotericsoftware.kryo.Serializer;
//import com.esotericsoftware.kryo.io.Input;
//import com.esotericsoftware.kryo.io.Output;

```

