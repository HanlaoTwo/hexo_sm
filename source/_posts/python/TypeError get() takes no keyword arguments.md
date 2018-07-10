---
title: TypeError get() takes no keyword arguments
date: 2018-07-10 21:09:19
tags: python
---
```
converted_comments.get(submission.id, default=0)
#改成
converted_comments.get(submission.id, 0)