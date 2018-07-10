---
title: work
date: 2018-07-10 21:09:19
tags: python
---
```
# -*- coding:utf-8 -*-
import requests
import re
import random

header_login = {
    'Host': 'hs-cas.hundsun.com',
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.157 Safari/537.36',
    'Upgrade-Insecure-Requests': '1',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
    'Accept-Language': 'en-US,en;q=0.5',
    'Accept-Encoding': 'gzip, deflate, sdch',
    'Connection': 'keep-alive',
    'Cache-Control': 'max-age=0'
}

header_info = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.157 Safari/537.36',
    'Upgrade-Insecure-Requests': '1',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
    'Accept-Language': 'en-US,en;q=0.5',
    'Accept-Encoding': 'gzip, deflate, sdch',
    'Referer': '127.0.0.1:8888',
    'Connection': 'keep-alive',
    'Cache-Control': 'max-age=0'
}

login_url = 'https://hs-cas.hundsun.com/cas/login?service=http%3A%2F%2Fpm.hundsun.com%3A80%2Fj_acegi_cas_security_check'
s = requests.Session()
# html = s.get(login_url, headers=header)

html = s.get(login_url, headers=header_login, verify=False)
# print(html)
print('结果：', html.status_code)
print('原因：', html.reason)

rule1 = '<input type=\"hidden\" name=\"lt\" value=\"(.*?)\" \/>'
rule2 = '<input type="hidden" name="execution" value="(.*?)" \/>'
rule3 = '<input type=\"hidden\" name=\"_eventId\" value=\"(.*?)\" \/>'

patten1 = re.compile(rule1, re.S)
patten2 = re.compile(rule2, re.S)
patten3 = re.compile(rule3, re.S)

array1 = re.findall(patten1, html.text)
array2 = re.findall(patten2, html.text)
array3 = re.findall(patten3, html.text)
loginParams = {
    'username': 'hanqian18790',
    'password': 'hanQIAN1993',
    'lt': array1[0],
    'execution': array2[0],
    '_eventId': array3[0]
}
sessionHtml = s.post(login_url, data=loginParams, verify=False)

print("the session rsult is: ", sessionHtml.status_code)
print("the reason is: ", sessionHtml.reason)

indexhtml = s.get('http://pm.hundsun.com/main.do', headers=header_login, verify=False)


r = random.random()
content = s.get(
    'http://pm.hundsun.com/pages/task/entityTab.jsf?taskId=423c943d-85d7-4cf8-9ce0-7020ad064bc4&action=0&keepOperate=N&r='+str(r)
    , headers=header_info, verify=False)
print('------->', content.status_code)
print('------->', content.text)
