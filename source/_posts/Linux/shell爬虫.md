---
title: shell爬虫
date: 2018-07-10 21:09:19
tags: Linux
---
```
curl -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:47.0) Gecko/20100101 Firefox/47.0' https://www.oschina.net/tweets | grep data-emoji-render | grep -o '"true">.*' | sed 's/"true">//;s/<\/span>/\n/;s/<\/div>/\n/'
