---
title: 使用jenkins+maven+svn持续部署  
date: 2016-08-04 16:07:50
categories:   部署 
tags: [jenkins,maven,svn]
---
1. 下载jenkins.war 包，放入tomcat中，浏览器中输入localhost:8080/jenkins
2. 根据提示找到密码，并输入
3. 安装插件，svn和maven插件<br/>
    a.在线安装
    ![setting](/path/to/6631783547769735330.png)<br/><!--more-->
    b. 离线下载，可选网址：
    [http://mirror.xmission.com/jenkins/plugins](http://mirror.xmission.com/jenkins/plugins)
    [http://updates.jenkins-ci.org/download/plugins](http://updates.jenkins-ci.org/download/plugins)
    [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)
    下载完成后点击选择文件，上传<br/> 
    ![setting](/path/to/6631550451304639277.png)<br/>
    c.还可以修改update site http://mirror.xmission.com/jenkins/updates/current/update-center.json
4. 创建项目
    a.输入项目名称，选择maven项目，点击ok
    ![setting](/path/to/6631505371327906980.png)<br/>
    b.输入svn地址，帐号和密码
    ![setting](/path/to/6631806637513918234.png)<br/>
    c.build的时候选择invoke top_level maven targer  
    ![setting](/path/to/6631830826769745627.png)<br/>
    d:最后点击save 就可以了
    项目中pom文件和maven的配置请看:[MAVEN自动部署项目到tomcat中](https://hanyahui88.github.io/2016/08/04/maven-deploy-tomcat/ "idea-docker")
5. 点击项目名称进入详情
    ![setting](/path/to/6631639511746493121.png)<br/>
    点击1 去构建
    点击2 去看日志，构建完后，如果项目前面显示的蓝色的球球就是成功了，红的球球就是失败了，可以点击2查看异常