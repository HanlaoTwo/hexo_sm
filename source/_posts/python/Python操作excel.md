---
title: Python操作excel
date: 2018-07-10 21:09:19
tags: python
---
#### 1.使用的库
> xlrd  库 ==读文件==

> xlwt  库 ==写文件==

[官网地址](http://pypi.python.org/pypi/xlrd)

可以操作的文件：.xls or .xlsx 文件

#### 2.用法
安装：
> pip install 模块

###### xlrd使用：

0. 打开文件
```
data = xlrd.open_workbook('文件.xlsx')
```

1. 获取excel的sheet,返回一个数组，每个元素都是一个sheet
```
sheet = data.sheets()
```
2. 获取表单
```
table = sheet[0]
```
3. 获取行的数量和列的数量
```
rowcount = table.nrows
colcount = table.ncols
```
4. 获取一行或一列的内容，返回一个数组。每个元素为一个单元格内容
```
row_values = table.row_values(i)  # i 为行数 
col_value = table.col_values(i)   # i 为列数
```
###### xlwd使用

[官网链接](https://github.com/python-excel/xlwt/tree/master/examples)

1. 使用 ==待更新==
#### 3.栗子
把一个excel里的数据导出成MySQL的insert语句
```
import xlrd

data = xlrd.open_workbook('data.xlsx')
table = data.sheets()[0]

table_name = "HSDATA.ASSET"
rowcount = table.nrows
cloum_names = table.row_values(1)

names_str = "INIT_DATE, FUND_ACCOUNT, MONEY_TYPE, TOTAL_ASSET, FUND_ASSET, SECU_MARKET_VALUE, OPFUND_MARKET_VALUE"
values_str = ""

for i in range(2,rowcount):
    cloum_values = table.row_values(i)
    index = 0
    for value in cloum_values:
        if(index == 0):
            values_str = values_str+str(int(value))+","
        if(index == 1):
            values_str = values_str+"\'hq\',"
        if(index == 2):
            values_str = values_str+"\'"+str(value)+"\',"
        if(index == 3):
            values_str = values_str+str(value)+","
        if(index == 4):
            values_str = values_str+str(value)+","
        if(index == 5):
            values_str = values_str+str(int(value))+","
        if(index == 6):
            values_str = values_str+str(value)
        index = index + 1

    sql = "INSERT INTO "+table_name+"("+names_str+")VALUES("+values_str+");"
    values_str = ""
    print (sql)
```