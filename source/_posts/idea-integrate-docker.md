---
title: idea 部署项目到docker中(centos)  
date: 2016-08-26 17:38:40
categories:   部署 
tags: [idea,docker,部署,centos]
---

1. 开启docker的remote api
    修改配置文件
    vim /etc/sysconfig/docker
    修改 OPTIONS='--selinux-enabled --log-driver=journald'
    为 OPTIONS='--selinux-enabled --log-driver=journald -H tcp://0.0.0.0:4243 -H unix:///run/docker.sock'<!--more-->
2. 项目中添加docker-dir文件夹，在文件件中创建Dockerfile文件
    Dockerfile: 

        FROM docker.io/hanyahui88/tomcat:latest
        
        ADD grass-1.0.war /usr/local/tomcat/webapps
        WORKDIR /usr/local/tomcat/webapps
        RUN mv grass-1.0.war grass.war
3. 最终的目录结构
    ![project](/path/to/20161017140753.png)<br/>
4. 打开idea的setting->clouds 点击 ，添加docker
    ![project](/path/to/6631544953747099030.png)<br/>
5. 打开project Structure ,将output directory 设置成docker-dir
    ![project](/path/to/6631663701002913845.png)<br/>
6. 打开Run/Debug Configurations，点击 ，添加Docker Deployment
    ![project](/path/to/6631588934212220439.png)<br/>
7. 添加项目（添加output-directory为docker-dir的war）
    ![project](/path/to/6631760458026152942.png)<br/>
8. 设置对外的端口
    ![project](/path/to/6631590033723848213.png)<br/>
9. 点击运行就ok了
    ![project](/path/to/6631715378049415715.png)<br/>