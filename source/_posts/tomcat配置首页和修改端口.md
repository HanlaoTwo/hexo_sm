---
title: tomcat配置首页和修改端口
date: 2018-06-18 16:04:15
tags: note
---
#### 修改端口
sever.xml   
修改Connector port="端口号" 
```
<Connector port="80" 
protocol="HTTP/1.1"
connectionTimeout="20000"
redirectPort="8443" />
```
#### 修改首页
server.xml  
*<host></host>* 中间加入一行   
*<Context path="" docBase= =="hello"== debug="0" reloadable="true" />*     
hello是要配置的新首页目录

```
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
            
		<Context path="" docBase="hello" debug="0" reloadable="true" />

        <Valve className="org.apache.catalina.valves.AccessLogValve" 
        directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

      </Host>
```