---
title: maven自动部署项目到tomcat中    
date: 2016-08-04 14:49:13
categories:   部署 
tags: [maven,tomcat,自动部署]
---

1. 项目pom文件配置:

        <build>
           <finalName>test</finalName>
           <outputDirectory>${project.basedir}/target/test</outputDirectory>
           <defaultGoal>deploy</defaultGoal>
           <plugins>
               <plugin>
                   <groupId>org.apache.tomcat.maven</groupId>
                   <artifactId>tomcat7-maven-plugin</artifactId>
                   <version>2.2</version>
                   <configuration>
                       <finalName>test</finalName>
                       <path>/test</path>
                       <port>8080</port>
                       <uriEncoding>UTF-8</uriEncoding>
                       <url>http://localhost:8080/manager/text</url>
                       <server>tomcat7</server>
                       <username>tomcat</username>
                       <password>tomcat</password>
                   </configuration>
               </plugin>
           </plugins>
       </build>
<!--more-->
2. maven %MAVEN_HOME%/conf/setting.xml文件配置
   
       <servers>
            <server>
                <id>tomcat7</id>
                <username>tomcat</username>
                <password>tomcat</password>
            </server>
        </servers>
3. tomcat  %TOMCAT_HOME%/conf/tomcat-users.xml文件配置

        <tomcat-users xmlns="http://tomcat.apache.org/xml"
                       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                       xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
                       version="1.0">
             <role rolename="manager-gui"/>
             <role rolename="manager-script"/>
             <user username="tomcat" password="tomcat" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
        </tomcat-users>
注：         
1、pom文件中的server名称和setting文件中的id名称相同
2、setting 文件、pom文件和tomcat-users文件的username和password都相同
启动tomcat，打开控制台，切换到项目目录下，输入 mvn tomcat7:deploy;
打开 http://localhost:8080/manager/html 看看项目是否存在了，存在说明成功了。