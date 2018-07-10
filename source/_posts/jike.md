---
title: jike
date: 2018-06-18 16:04:15
tags: note
---
```
# -*- coding:utf-8 -*-

import requests
import re
import os

header = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:47.0) Gecko/20100101 Firefox/47.0',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8',
    'Accept-Language': 'zh-CN,zh;q=0.9,en;q=0.8',
    'Accept-Encoding': 'gzip, deflate',
    #'Referer':'http://www.jikexueyuan.com/course/1888.html?ss=1',
    'Cookie':'td_cookie=1156121737; _ga=GA1.2.380983170.1517797102; jkxyid_v2=574de074-6b6b-4475-a7f2-f01a14c4dd21; gr_user_id=93987888-4f04-4dc8-a2d8-b01212db5f21; _uab_collina=151779718059576220008262; MEIQIA_EXTRA_TRACK_ID=0vxp6LiOs5F6RZmZFpn0fdzGX1W; _umdata=C234BF9D3AFA6FE71EA6E4CE48D9BD53DB0208CB20D959012232396F043CC94EAD06E375B71FBF5DCD43AD3E795C914CAF4E29E6B21796B4E2F1E1803717844A; td_cookie=1583310513; _gid=GA1.2.25731033.1520306022; otherlogin=qq; uname=qq_9e3o2asf; uid=4627872; code=JYEUNA; authcode=135fwTzluWIwAbg4QQgj48oRfZkTbGiov3CgE5kvOkHaekzFmCYrdmcB8F3CED6V8GIp4eDkwxmpTKUyk9DsQBTJ1QvVOl8Xpwj5BXlhE81KtNQSlGsSOZYwc17WawQ; avatar=https%3A%2F%2Fassets.jikexueyuan.com%2Fuser%2Favtar%2Fdefault.gif; ca_status=1; vip_status=1; level_id=1; is_expire=0; domain=0iqWVUPUV; svip_status=0; svip_is_expire=1; QINGCLOUDELB=84b10773c6746376c2c7ad1fac354ddfd562b81daa2a899c46d3a1e304c7eb2b|Wp5di|Wp5di; gr_session_id_aacd01fff9535e79=73501102-bee7-4b50-a563-9f0cd3bd3a29; gr_cs1_73501102-bee7-4b50-a563-9f0cd3bd3a29=uid%3A4627872'
}

referParam = {'course_id': '1888'}


bigdata = 'http://ke.jikexueyuan.com/zhiye/bigdata/'
html = requests.get(bigdata,headers=header)
chapterRule = '<a jktag=".*" target="_blank" href="(.*?)" title=".*" class="inner">'
chapterUrl = re.findall(re.compile(chapterRule),html.text)
i=0

for chapter in chapterUrl:
    html = requests.get('http:'+chapter,headers=header)
    #referData = requests.get('http://www.jikexueyuan.com/course/1888.html',headers=header,params=referParam)
    #print(referData.text)
    #print(html.text)

    chapterTitleRule = '<a class="active" href="javascript:;">(.*?)</a>'
    chapterTile = re.findall(re.compile(chapterTitleRule,re.S),str(html.content,'utf-8'))[0]
    dir = str(i)+chapterTile
    os.mkdir( dir, 7777 )
    i = i+1

    contentsRule = '<span class="sm-icon "></span>\n\s*<a href="\/\/(.*?)" jktag=".*">.*?<\/a>'
    contentsPattern = re.compile(contentsRule)
    contentsUrls = re.findall(contentsPattern,html.text)
    print(contentsUrls)
    for courseUrl in contentsUrls:
        courseHtml = requests.get('http://'+courseUrl,headers=header)

        vedioRule = '<source src="(.*?)".* type="video/mp4"'
        titleRule = '<span class="tit">(.*?)</span>'

        vedioPattern = re.compile(vedioRule,re.S)
        titlePattern = re.compile(titleRule,re.S)

        vedioUrl = re.findall(vedioPattern,courseHtml.text)[0]
        title = re.findall(titlePattern,str(courseHtml.content,'utf-8'))[0]

        vedioUrl = vedioUrl.replace('amp;','')

        print(vedioUrl)
        print(title)

        vedio = requests.get(url=vedioUrl)
        with open(dir+'/'+title+'.mp4', 'wb') as f:
            f.write(vedio.content)
            f.flush()

