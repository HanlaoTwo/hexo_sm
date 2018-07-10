---
title: sql
date: 2018-07-10 21:09:19
tags: work
---
```

SELECT
  a.acpt_category_no,
  a.acpt_category_name,
  c.param_id,
  c.param_name,
  b.need_flag,
  b.organ_flag,
  b.prof_flag,
  b.prof_type,
  b.data_type,
  b.int_config,
  b.str_config
FROM hs_acpt.bopcategory a, hs_acpt.bopbusintypequaliarg b, hs_acpt.bopqualiarg c
WHERE a.acpt_category_no = b.acpt_busin_type AND b.param_id = c.param_id AND a.acpt_category_level = 2 AND
      b.need_flag = 1  AND a.acpt_category_no = '0044'--= '0252' AND c.param_id
                                              IN
                          ('0116', '0018', '0019', '0027', '0028', '0041', '0044', '0045', '0046', '0053', '0065',
                            '0066', '0116', '0119', '0122', '0134', '0168', '0169', '0172', '0174', '0177', '0179',
                           '0189', '1002', '1003', '1004','0252');


select * from hs_acpt.bopbusintypequaliarg  WHERE acpt_busin_type  = 0018;


INSERT INTO hs_acpt.bopbusintypequaliarg
(ACPT_BUSIN_TYPE, ORGAN_FLAG, PARAM_ID, DATA_TYPE, INT_CONFIG, STR_CONFIG, MODIFY_ABLE, NEED_FLAG, SHOW_TITLE, ORDER_NO, PROF_FLAG, PROF_TYPE)
VALUES ('0018', '0', 24, '1', 50, '1111111111111,20', '1', '1', ' ', 7, '0', '!');
-- 用户参数
SELECT t.ORGAN_FLAG,p.prof_flag,p.prof_type FROM CLIENTPREFER p,CLIENT t WHERE p.CLIENT_ID = t.CLIENT_ID AND t.CLIENT_ID = 'IO20170101011';

select a.client_id,a.fund_account,a.asset_prop,t.init_date,t.money_type,
  d.fin_close_balance + d.slo_close_balance + d.fare_close_debit + d.fin_close_interest+ d.slo_close_interest + d.fin_close_fine_interest + d.slo_close_fine_interest+ d.other_close_interest + d.other_close_debit + d.other_close_fine_interest + d.refcost_close_fare as total_debit,
                                   t.fund_asset
                                   +t.secu_market_value
                                   +t.opfund_market_value
                                   +t.opt_market_value
                                   --+t.total_debit
                                   +t.prod_market_value
                                   +t.hkfund_market_value
                                   +t.ofcash_market_value
                                  +t.pfund_market_value
                                   +t.secum_market_value
                                as totalasset
from hs_his.his_asset t, hs_asset.fundaccount a,hs_data.assetdebit d
where a.fund_account=t.fund_account
  and a.fund_account = d.fund_account
  and t.init_date = d.init_date
  and t.money_type = d.money_type
  --and t.init_date = '20170104'
  and a.client_id like 'IT20170101004%';

SELECT CLIENT_ID,ORGAN_FLAG,PROF_FLAG,PROF_TYPE from CLIENTPREFER WHERE CLIENT_ID = 'IT20170101001';
UPDATE  client set ORGAN_FLAG='0'  WHERE CLIENT_ID = 'IO20170101005'

select * from  hs_acpt.bopbusintypequaliarg
UPDATE hs_acpt.bopbusintypequaliarg SET prof_flag = '1' WHERE acpt_busin_type='0044' and param_id = 53
select ORGAN_FLAG from client where client_id='IT20170101001'
select prof_flag from CLIENTPREFER where client_id='IT20170101001'
-- 业务
SELECT a.acpt_category_no,a.acpt_category_name,c.param_id,c.param_name,b.need_flag,b.organ_flag,b.prof_flag,b.prof_type,b.data_type,b.int_config,b.str_config
FROM hs_acpt.bopcategory a, hs_acpt.bopbusintypequaliarg b, hs_acpt.bopqualiarg c,CLIENTPREFER p,CLIENT t
WHERE a.acpt_category_no = b.acpt_busin_type AND b.param_id = c.param_id AND a.acpt_category_level = 2 AND b.need_flag = 1
     AND t.ORGAN_FLAG = b.organ_flag and p.prof_flag= b.prof_flag
      AND a.acpt_category_no = '0044' --AND c.param_id in (50,51,52,53,54,55,56,57,58,60)
      and p.CLIENT_ID = t.CLIENT_ID
      AND t.CLIENT_ID = 'IT20170101004'
ORDER BY param_id;
-- 负债
SELECT fin_close_balance ,slo_close_balance , fare_close_debit , fin_close_interest, slo_close_interest , fin_close_fine_interest , slo_close_fine_interest, other_close_interest , other_close_debit , other_close_fine_interest, refcost_close_fare from hs_data.ASSETDEBIT WHERE CLIENT_ID = 'IO20170101026' AND INIT_DATE = '20170105';

SELECT * from BUSINESSACCEPT WHERE ACPT_CATEGORY_NO = '0252';
  --CLIENT_ID LIKE 'IT20170101001%' and
  --PARAM_VALUE like '%#58#%';

-- p50 p51 p52
SELECT CLIENT_ID,CLIENT_INCOME_TYPE as p50,THREE_YEARS_AVG_INCOM as p51,LAST_YEAR_NET_ASSET as p52 from CLIENTPREFER WHERE CLIENT_ID = 'IT20170101004';
-- p53
SELECT c.CLIENT_ID from CLIENT c,hs_crdt.riskacctlist r WHERE r.id_kind = c.id_kind and r.id_no = c.id_no AND r.client_name = c.FULL_NAME and r.riskaccount_type = '0';
-- p54
SELECT o.CLIENT_ID from FUNDACCOUNT f ,OPTBLACKACCT o ,CLIENT c WHERE c.CLIENT_ID = o.CLIENT_ID AND f.ASSET_PROP = 'B' AND f.FUND_ACCOUNT= o.FUND_ACCOUNT;
-- 55,56,57,58,60
SELECT CLIENT_ID,CORP_RISK_LEVEL as p55,EN_INVEST_TERM as p56,EN_INVEST_KIND as p57,CLIENT_INCOME_TYPE as p58,EN_MAXDEFICIT_RATE as p60 from CLIENTPREFER WHERE CLIENT_ID = 'IT20170101004';

SELECT h.fund_account,h.init_date,SECU_MARKET_VALUE from hs_his.his_asset h,FUNDACCOUNT f WHERE f.FUND_ACCOUNT=h.fund_account and f.CLIENT_ID = 'IT20170101024';



SELECT * from FUNDACCOUNT WHERE FUND_ACCOUNT = 'IT20170101004';
UPDATE FUNDACCOUNT SET ASSET_PROP = 'B' WHERE FUND_ACCOUNT = 'IT20170101004';
UPDATE FUNDACCOUNT SET ASSET_PROP = 'B' WHERE FUND_ACCOUNT = 'IT20170101006';
UPDATE FUNDACCOUNT SET ASSET_PROP = 'B' WHERE FUND_ACCOUNT = 'IO20170101004';
UPDATE CLIENTPREFER SET CLIENT_INCOME_TYPE = '2' WHERE CLIENT_ID = 'IT20170101001';
SELECT * from CLIENT WHERE id_no = '510212196801081335';
SELECT client_name,CLIENT_id,id_no,id_kind,riskaccount_type from hs_crdt.riskacctlist;
UPDATE CLIENT SET FULL_NAME = '王斌' WHERE CLIENT_ID = 'IT20170101001';
UPDATE hs_crdt.riskacctlist set riskaccount_type = '0';
UPDATE CLIENTPREFER SET CLIENT_INCOME_TYPE = '2' WHERE CLIENT_ID LIKE 'IO%';
SELECT CLIENT_INCOME_TYPE,CLIENT_ID from CLIENTPREFER WHERE CLIENT_ID LIKE 'IO%';
COMMIT;

select st.client_id,ss.stock_account from hs_asset.sstrestradeacct ss ,HS_ASSET.STOCKHOLDER st WHERE ss.STOCK_ACCOUNT =st.STOCK_ACCOUNT ;
UPDATE CLIENTPREFER SET PROF_FLAG = '0',PROF_TYPE='!'WHERE CLIENT_ID = 'IO20170101005';

select a.client_id,t.init_date,t.secum_market_value
from hs_his.his_asset t
join hs_asset.fundaccount a on a.fund_account=t.fund_account where t.init_date='20170105' and a.client_id ='IT20170101024';

SELECT h.fund_account,h.init_date,SECU_MARKET_VALUE from hs_his.his_asset h,FUNDACCOUNT f
WHERE f.FUND_ACCOUNT=h.fund_account and f.CLIENT_ID = 'IT20170101024';

SELECT * from BUSINESSACCEPT WHERE PRE_ANALYSIS_TYPE = 2;--WHERE CLIENT_ID like 'IT%' AND ACPT_CATEGORY_NO = 0053;

SELECT * from hs_user.SYSDICTIONARY WHERE DICT_ENTRY = 2505;

SELECT * from FUNDACCOUNT WHERE asset_prop = 7;

SELECT * from BUSINESSACCEPT WHERE ACPT_CATEGORY_NO = '0018'
select a.en_prodrisk_level,ORGAN_FLAG  from  eligriskmatch a
where a.finance_type = 1

      and a.corp_risk_level = 2;

select a.en_prodrisk_level  from  eligriskmatch a
where a.finance_type = 1
and a.organ_flag = 1
and a.corp_risk_level = 2;

