---
title: oracle
date: 2018-07-10 21:09:20
tags: oracle
---
- #### 查看表结构
```
 describe nchar_tst
```
- #### 查操作记录
    
    select t.SQL_TEXT, t.FIRST_LOAD_TIME
    from v$sqlarea t
    where t.SQL_TEXT like 'delete%' and t.FIRST_LOAD_TIME like '2017%'
    order by t.FIRST_LOAD_TIME desc;
    
- #### 锁表
```
select b.OBJECT_NAME,a.ORACLE_USERNAME,a.OS_USER_NAME,a.PROCESS, c.program,c.terminal,c.sid,c.serial#
from V$LOCKED_OBJECT a,DBA_OBJECTS b,v$session c where   (a.OBJECT_ID=b.OBJECT_ID and c.sid=a.session_id)
order by a.ORACLE_USERNAME,b.OBJECT_NAME;

alter system kill session '198,240';
```

- #### 会话数太多
> ORA-12516: TNS: 监听程序无法找到匹配协议栈的可用句柄.
TNS-12516 TNS:listener could not find available handler with matching protocol stack

查看会话数：
```
select count(*) from v$session;
```

[解决办法](http://www.open-open.com/lib/view/open1338520588261.html)

[Oracle中会话的状态](http://blog.csdn.net/haiross/article/details/43447353)

- #### java.sql.SQLException: ORA-00911: 无效字符
sql多了一个";" 去掉就可以了

- #### 查看建表语句

select dbms_metadata.get_ddl('TABLE','ELIGRISKMATCH') from dual;

- #### 恢复数据

[恢复数据](http://www.cnblogs.com/chaizp/p/5192522.html)
```
select * from hs_his.his_clientinfojour AS OF TIMESTAMP  (SYSTIMESTAMP - INTERVAL '100' MINUTE);

select * from hs_his.his_clientinfojour as of timestamp to_timestamp('2017-11-01 01:00:00','YYYY-MM-DD HH24:MI:SS');

select timestamp_to_scn(to_timestamp('2017-11-01 01:00:00','YYYY-MM-DD HH:MI:SS')) from dual;
```

- #### 查操作记录

```
select t.SQL_TEXT, t.FIRST_LOAD_TIME
from v$sqlarea t
 where t.FIRST_LOAD_TIME like '2010-06-30%'
 order by t.FIRST_LOAD_TIME desc
```



























