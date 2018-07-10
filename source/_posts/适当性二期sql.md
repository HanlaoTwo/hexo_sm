---
title: 适当性二期sql
date: 2018-06-18 16:04:15
tags: note
---
```

-- 测评日期，测评到期日
SELECT
  client_id,
  corp_begin_date,
  corp_end_date
FROM hs_asset.clientprefer; --where client_id = @client_id;

--2.
--开户天数,organ_flag--> select organ_flag from client where client_id = @client_id
SELECT
  organ_flag,
  open_days
FROM hs_asset.eligpaper
WHERE paper_type = '1' AND prodta_no = ' ';

-- 试卷获取
SELECT
  a.*,
  b.question_type,
  b.question_kind,
  b.question_content,
  b.open_date

FROM hs_asset.eligpaperquestrel a, hs_asset.eligquestion b

WHERE a.paper_type = '1' AND a.prodta_no = ' ' AND a.question_no = b.question_no

ORDER BY a.order_no, a.paper_type, a.organ_flag ASC;



SELECT STOCK_CODE from HS_DATA.HIS_PRICE;

-- 3.答案获取 client_id = @client_id paper_answer like '%*'
SELECT
  paper_answer,
  CLIENT_ID
FROM hs_his.his_eligtestjour
WHERE paper_type = '1' AND prodta_no = ' ';

select init_date, client_id,paper_answer,position_str from hs_his.his_eligtestjour where  paper_type = '1' and prodta_no = ' '