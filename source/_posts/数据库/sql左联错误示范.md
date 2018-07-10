---
title: sql左联错误示范
date: 2018-07-10 21:09:19
tags: 数据库
---
```
SELECT
  a.first_ratio,
  a.second_ratio,
  a.organ_flag,
  a.question_score,
  a.prodta_no,
  a.paper_type,
  a.question_no,
  d.base_score,
  a.delete_flag AS myflag,
  d.delete_flag
FROM
  hs_asset.eligpaperquestrel a LEFT JOIN hs_asset.eligpaper d
    ON a.paper_type = d.paper_type
       AND a.prodta_no = d.prodta_no
       AND a.organ_flag = d.organ_flag
       AND d.delete_flag = '0' -- ORDER BY a.question_no
--AND a.delete_flag = '0'
WHERE A.QUESTION_NO = '53' AND a.paper_type = '-' AND a.prodta_no = ' ';
```