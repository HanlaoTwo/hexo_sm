---
title: Python 执行shell命令， 获取时间，切割字符串
date: 2018-07-10 21:09:19
tags: python
---
```
#import subprocess
#import commands
import time
import datetime

startdate = '20160101'
enddate = '20160101'


closefile = open('close', 'r+')


def next_day(date):
    i = date[0:3]
    m = int(i)
    date = datetime.datetime(int(date[0:4]), int(date[4:6]), int(date[6:8])) + datetime.timedelta(days=1)
    time_format = date.strftime('%Y%m%d')
    return time_format


def copy_data(date, next_date):
    print('hahahah',date,'lallala',next_date)
    command = 'perl -p -i'+date+'.bak -e "s/' + date + '/' + next_date + '/g" t'
    print(command)
    #subprocess.call(command)
    #commands.getoutput(command)


while 1:
    closedate = closefile.readline().replace('\n','')
    closedate = closedate.replace('\r','')
    if (closedate):
        copy_data(startdate, next_day(startdate))
        startdate = next_day(startdate)
    else:
        break

closefile.close()
```