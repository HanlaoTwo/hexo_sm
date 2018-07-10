---
title: mysql存储过程
date: 2018-07-10 21:09:19
tags: mysql
---
- ### 直接修改
```
DROP PROCEDURE IF EXISTS modrow;
CREATE PROCEDURE modrow()
  BEGIN

    #DECLARE mod_row_count INT;

    SELECT count(COLUMN_NAME)
    as mod_row_count
    FROM information_schema.columns
    WHERE table_name = 'bopbusitypeinfo'
          AND column_name IN ('acpt_category_no','acpt_category_name','param_id','param_name','need_flag','organ_flag','data_type','int_config','str_config');

    IF mod_row_count = 9
    THEN
      ALTER TABLE hselite.bopbusitypeinfo MODIFY acpt_category_no VARCHAR(4);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY acpt_category_name VARCHAR(64);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY param_id DECIMAL(10);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY param_name VARCHAR(2000);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY need_flag CHAR(1);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY organ_flag CHAR(1);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY data_type CHAR(1);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY int_config DECIMAL(10);
      ALTER TABLE hselite.bopbusitypeinfo MODIFY str_config VARCHAR(255);
    END IF;

  END;
CALL modrow();
```
- ### 定义分隔符
```
delimiter //
DROP PROCEDURE IF EXISTS modrow;
CREATE PROCEDURE modrow()
  BEGIN
  select 1+1 from dual;
  END;
CALL modrow();
//

```
- ### 带参数的
```
DROP PROCEDURE IF EXISTS modrow;
CREATE PROCEDURE modrow(IN dbname VARCHAR(255),IN tablename VARCHAR(255),IN cloumname VARCHAR(255),IN descripe VARCHAR(1000))
  BEGIN
    DECLARE mod_row_count INT;
    SET @dbname = dbname;
    SET @tablename = tablename;
    SET @cloumname = cloumname;
    SET @descripe = descripe;

    SELECT count(COLUMN_NAME)
    INTO mod_row_count
    FROM information_schema.columns
    WHERE table_name = @tablename
          AND column_name = @cloumname;

    IF mod_row_count = 1
    THEN
      SET @insertSql = @descripe;
      PREPARE stmtinsert FROM @insertSql;
      EXECUTE stmtinsert;
      DEALLOCATE PREPARE stmtinsert;
    END IF;
  END;
CALL modrow('hselite','accept','prof_flag','ALTER TABLE hselite.accept MODIFY prof_flag VARCHAR(4)');
```
- ### 动态sql
```
DROP PROCEDURE IF EXISTS hselite.pro_mod_tab_col;
CREATE DEFINER=`root`@`%` PROCEDURE `pro_mod_tab_col`(IN ddname varchar(64),IN talname varchar(64),IN colname varchar(64),IN typename varchar(64),IN commt varchar(64),IN def_var varchar(64))
  BEGIN
    DECLARE num VARCHAR(100);
    declare l_tab_name varchar(100); #表名
    declare l_dd_name varchar(100);  #库名
    declare l_col_name varchar(100); #字段名
    declare l_type_name varchar(100); #字段类型
    declare l_commt varchar(100);  #注释
    declare l_def_var varchar(100);  #默认值
    declare SQL_FOR_alter varchar(500);  ##动态sql

    set @l_dd_name=ddname ;
    set @l_tab_name=talname;
    set @l_col_name=colname;
    set @l_type_name=typename;
    set @l_commt=commt;
    set @l_def_var=def_var;

    set @SQL_FOR_alter=CONCAT("ALTER TABLE " ,@l_dd_name,'.',@l_tab_name, " MODIFY ",@l_col_name,' ',@l_type_name ," DEFAULT '" ,@l_def_var,"' not null COMMENT '", @l_commt," ';");
    #select  @SQL_FOR_alter;
    select count(1) into num from information_schema.columns WHERE table_schema=@l_dd_name and table_name = @l_tab_name AND column_name =@l_col_name;
    #select num;
    IF (num=1) THEN
      PREPARE stmt1 FROM @SQL_FOR_alter;
      EXECUTE stmt1;
      DEALLOCATE PREPARE stmt1 ;
    end if;
  END;

```

