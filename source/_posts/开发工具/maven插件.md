---
title: maven插件
date: 2018-07-10 21:09:19
tags: 开发工具
---
- maven-surefire-plugin

Maven通过Maven Surefire Plugin插件执行单元测试。（通过Maven Failsafe Plugin插件执行集成测试）

 

在pom.xml中配置JUnit,TestNG测试框架的依赖，即可自动识别和运行src/test目录下利用该框架编写的测试用例。surefire也能识别和执行符合一定命名约定的普通类中的测试方法（POJO测试）。

生命周期中test阶段默认绑定的插件目标就是surefire中的test目标，无需额外配置，直接运行mvn test就可以。

 

基本配置如下，下文中的配置项如无特殊说明，都位于pom文件的<configuration>节点中。
```
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.18.1</version>
        <configuration>
          ......
　　　　　　配置内容
　　　　　　......
        </configuration>
      </plugin>
```
```
 

//常用通用配置
// 跳过测试阶段
<skipTests>true</skipTests>
或者 

mvn install -DskipTests
或者 （Compliler插件也会根据该参数跳过编译测试类） 

mvn install -Dmaven.test.skip=true
 
```
忽略测试失败 
Maven在测试阶段出现失败的用例时，默认的行为是停止当前构建，构建过程也会以失败结束。有时候（如测试驱动开发模式）即使测试出现失败用例，仍然希望能继续构建项目。
```
<testFailureIgnore>true</testFailureIgnore> 
或者

mvn test -Dmaven.test.failure.ignore=true
 
```
- maven-jar-plugin

默认的mvn install生成的jar是不带主类入口的，需要在maven-compile-plugin中设置主类
```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <classpathPrefix>lib/</classpathPrefix>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
```
- maven-compiler-plugin

设置编译器的版本

```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
            </plugin>
```
- maven-dependency-plugin
把依赖的jar包单独放到一个目录下
```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>copy-dependencies</id>
                        <phase>prepare-package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${project.build.directory}/lib</outputDirectory>
                            <overWriteReleases>false</overWriteReleases>
                            <overWriteSnapshots>false</overWriteSnapshots>
                            <overWriteIfNewer>true</overWriteIfNewer>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```