---
title: redis增删改查----Spring+redis
date: 2018-07-10 21:09:20
tags: redis
---
https://www.ibm.com/developerworks/cn/java/os-springredis/index.html

https://docs.spring.io/spring-data/data-redis/docs/current/reference/html/#get-started

https://docs.spring.io/spring-data/redis/docs/2.0.1.RELEASE/api/

java 文件
```
ackage com.hundsun.account.hs_rt_account.redis;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.data.redis.core.ListOperations;
import org.springframework.data.redis.core.RedisTemplate;

/**
 * Created by asdas 2017/11/9.
 * for test
 */
public class TestRedis {


    private static RedisTemplate redisTemplate;
    private static ListOperations hellolistops;

    public static void main(String[] args) {
        ApplicationContext ac = new ClassPathXmlApplicationContext(new String[]{"applicationContext-redis.xml"});
        //从Spring容器中根据bean的id取出我们要使用的userService对象
        redisTemplate = (RedisTemplate) ac.getBean("redisTemplate");
        hellolistops = redisTemplate.opsForList();
        TestRedis tr = new TestRedis();

        tr.addHello("test1", "first");
        tr.addHello("test2", "second");
        tr.addHello("test3", "third");

        tr.delHello("test3");

        tr.modHello("test2", "di er ge");

        System.out.println(tr.getHello("test1"));
        System.out.println(tr.getHello("test2"));
        System.out.println(tr.getHello("test3"));
    }

    public void addHello(String id, String hello) {
         hellolistops.leftPush(id, hello);
        //System.out.println(l);
    }

    public void delHello(String id) {
        redisTemplate.delete(id);
    }

    public void modHello(String id, String hello_mod) {
        redisTemplate.delete(id);
        hellolistops.leftPush(id, hello_mod);
    }

    public String getHello(String id) {
        return hellolistops.range(id, 0, -1).toString();
    }
}

```
pom文件
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.hundsun.account</groupId>
	<artifactId>hs-rt-account</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>hs-rt-account</name>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.compile.ver>1.7</project.compile.ver>
	</properties>

	<dependencies>

		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.8.1</version>
		</dependency>


	
		<!-- redis -->
		<dependency>
			<groupId>org.springframework.data</groupId>
			<artifactId>spring-data-redis</artifactId>
			<version>1.8.8.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>redis.clients</groupId>
			<artifactId>jedis</artifactId>
			<version>2.9.0</version>
		</dependency>
		<dependency>
			<groupId>commons-pool</groupId>
			<artifactId>commons-pool</artifactId>
			<version>1.6</version>
		</dependency>

	</dependencies>
	
</project>

```
spring配置文件
applicationContext-redis.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xmlns:p="http://www.springframework.org/schema/p"
		xmlns:context="http://www.springframework.org/schema/context" 
		xsi:schemaLocation="
			http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
			http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

	<bean id="jedisConnectionFactory"
		class="org.springframework.data.redis.connection.jedis.JedisConnectionFactory"
		p:host-name="${redis.host}" p:port="${redis.port}" p:password="${redis.pass}">
	</bean>
	<!-- Configurer that replaces ${...} placeholders with values from a properties 
		file -->
	<context:property-placeholder location="classpath:redis.properties" />

	<context:annotation-config />

	<bean id="redisTemplate" class="org.springframework.data.redis.core.RedisTemplate"
		p:connection-factory-ref="jedisConnectionFactory">
		<property name="keySerializer">
			<bean class="org.springframework.data.redis.serializer.StringRedisSerializer" />
		</property>
		<property name="valueSerializer">
			<bean class="org.springframework.data.redis.serializer.StringRedisSerializer" />
		</property>
		<property name="hashKeySerializer">
			<bean class="org.springframework.data.redis.serializer.StringRedisSerializer" />
		</property>
		<property name="hashValueSerializer">
			<bean class="org.springframework.data.redis.serializer.StringRedisSerializer" />
		</property>
	</bean>

</beans>

```