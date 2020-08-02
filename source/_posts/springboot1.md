---
title: SpringBoot入门教程————环境搭建
date: 2018-12-5 22:21:38
categories: java
tags: 
 - 教程 
 - springboot
 - java
---
## springboot简介

## 开发环境
1、jdk1.8
2、IntelliJ IDEA
3、springboot2.x
4、maven

## 新建项目
首先打开IntelliJ IDEA，点击创建Create New Project
{% asset_image github1.png %}
然后选择Spring Initializr,点击next
{% asset_image github2.png %}
配置Group和Artifact，点击next
{% asset_image github3.png %}
可以在Dependencies处搜索所需的依赖包，这里我们添加了一些常用的依赖包，点击next
{% asset_image github4.png %}
接着配置项目名，项目路径，点击finish
{% asset_image github5.png %}
稍等一下，IntelliJ IDEA会构建项目，并创建目录结构，下载添加的依赖包，创建完的项目是这样的
{% asset_image github6.png %}
## 运行项目
项目现在已经创建好了，我们先看一下里面都有什么内容
主要的文件只有三个
1、XXXXApplication
2、appliction.properties
3、pom.xml
### XXXXApplication
springboot启动类（入口函数、main函数）
因为我们第一次只是想要启动它，不添加什么其他的配置所以我们要加上(exclude = DataSourceAutoConfiguration.class)在@SpringBoot注解后面，它的意思是，禁用springboot的自动配置数据源
{% asset_image github8.png %}
### application.properties
这个文件是springboot的配置文件，大多数springboot的相关配置都可以在这里实现，因为当前我们什么也没配置所以他是空的
{% asset_image github9.png %}
### pom.xml
这个文件是maven的配置文件，maven项目引入的所有的jar包都是在这里面导入的
``` base
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.langxy</groupId>
    <artifactId>template</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>template</name>
    <description>Template project for Spring Boot</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.1.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.3.2</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```
### 运行
点击debug运行，这样这个springboot项目就运行起来了
{% asset_image github7.png %}
