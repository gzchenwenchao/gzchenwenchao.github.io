---
layout: post
title:  "JAVA SE 项目获取环境变量加载不同的环境变量文件"
date:   2017-10-18 00:26:00 +0800
categories: code
---

JAVA SE 项目获取环境变量加载不同的环境变量文件

properties-context.xml
```
    <bean id="application.properties" class="org.springframework.beans.factory.config.PropertiesFactoryBean">
        <property name="ignoreResourceNotFound" value="true" />
        <property name="locations">
            <list>
                <value>file:APP-INF/properties/${Runtime-Env}.properties</value>
                <value>classpath*:META-INF/config/properties/**/${Runtime-Env}.properties</value>
                <value>classpath*:META-INF/config/properties/**/*-${Runtime-Env}.properties</value>
            </list>
        </property>
    </bean>
```

pom.xml
```
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <configuration>
            <archive>
                <manifest>
                    <addClasspath>true</addClasspath>
                    <classpathPrefix>lib/</classpathPrefix>
                    <mainClass>MainClass</mainClass>
                </manifest>
                <manifestEntries>
                    <Runtime-Env>${runtime.env}</Runtime-Env>
                </manifestEntries>
            </archive>
        </configuration>
    </plugin>
```

打包的时候会打到文件 META-INFO/MANIFEST.MF 里，demo：
Manifest-Version: 1.0
Runtime-Env: release
Archiver-Version: Plexus Archiver


java 

```java
    JarFile jarFile = new JarFile(JAR_FILE);
    Manifest mf = jarFile.getManifest();
    Attributes ma = mf.getMainAttributes();
    String env = ma.getValue(ENV);
    System.setProperty(ENV, env);
```