---
title: 替换jar包中为文件
date: 2018-07-10 21:09:19
tags: Linux
---
```
jar tvf tag-1.5.3-release-jar-with-dependencies.jar | grep ProdacceptReduce

jar xvf tag-1.5.3-release-jar-with-dependencies.jar com/hs/tag/tag/accept/prodaccept/ProdacceptReduce.class

rm com/hs/tag/tag/accept/prodaccept/ProdacceptReduce.class

cp ProdMatchReduce.class com/hs/tag/tag/accept/prodaccept/

jar uvf tag-1.5.3-release-jar-with-dependencies.jarcom/hs/tag/tag/accept/prodaccept/ProdacceptReduce.class
```
组合
```
jar xvf tag-1.5.3-release-jar-with-dependencies.jar `jar tvf tag-1.5.3-release-jar-with-dependencies.jar | grep ProdacceptReduce | awk '{print $NF}'`