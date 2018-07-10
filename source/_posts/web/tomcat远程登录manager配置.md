---
title: tomcat远程登录manager配置
date: 2018-07-10 21:09:19
tags: web
---
- #### 增加用户    
    
    vim vim conf/tomcat-users.xml

修改文件
```
<role rolename="tomcat"/>
<role rolename="role1"/>
<user username="tomcat" password="000000" roles="tomcat"/>
<user username="both" password="000000" roles="tomcat,role1"/>
<user username="role1" password="000000" roles="role1"/>
<!-- 上边是原来的，取消注释要修改password，也可以不取消注释 -->
<role rolename="manager"/>　
<role rolename="manager-gui"/>　
<role rolename="admin"/>　
<role rolename="admin-gui"/>　
<role rolename="manager-script"/>
<user username="hello" password="000000" roles="admin-gui,admin,manager-gui,manager,manager-script"/>
```
- #### 增加权限
在
```
conf/Catalina/localhost
```
目录下新建
```
manager.xml
```
文件
    
    vim manager.xml

文件内容
```
    <Context privileged="true" antiResourceLocking="false" docBase="${catalina.home}/webapps/manager">
        <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```

重启tomcat

然后打开ip/manager/html

输入

```
hello
000000
```

登录