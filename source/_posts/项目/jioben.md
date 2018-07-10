---
title: jioben
date: 2018-07-10 21:09:19
tags: 项目
---
```
drop table accept;
CREATE TABLE `accept` (
  `CLIENT_ID` varchar(18) NOT NULL,
  `ORGAN_FLAG` char(2) DEFAULT '',
  `BRANCH_NO` decimal(10,0) NOT NULL DEFAULT '0',
  `ACPT_CATEGORY_NO` varchar(4) NOT NULL DEFAULT '',
  `ACPT_CATEGORY_NAME` varchar(64) NOT NULL,
  `PASS_FLAG` char(10) DEFAULT NULL,
  `PARAM_VALUE` varchar(2000) DEFAULT NULL,
  `INIT_DATE` decimal(10,0) DEFAULT NULL,
  `SEQ_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  UNIQUE KEY `accept_SEQ_ID_uindex` (`SEQ_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=2578 DEFAULT CHARSET=utf8;