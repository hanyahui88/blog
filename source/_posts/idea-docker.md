---
title: idea 调试发布到docker中的web项目(centos)  
date: 2016-08-26 17:38:40
categories:   部署 
tags: [docker,web,idea]
---
1. 下载docker pull hanyahui88/tomcat  镜像，因为这个镜像开启了5005的调试端口(或者自己下载个tomcat的官方镜像，然后自己开启5005端口，在用这个生成一个镜像)
2. 打开Run/Debug Configurations，点击 +，添加remote，添加docker中访问tomcat的ip<!--more-->
![setting](/path/to/6631541655212221615.png)<br/>
3. docker中启动tomcat后，idea中启动remote就可以了，在本地打个断点，访问tomcat，可以验证
注：代码一定要同步，不然会有出入
想看怎么在idea中集成docker请点击：[这里](https://hanyahui88.github.io/2016/10/17/idea-integrate-docker/ "idea-docker")