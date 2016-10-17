---
title: tomcat 配置https
date: 2016-09-21 17:08:14
categories:   部署 
tags: [tomcat,https]
---
1. 首先是申请证书，可以用java自带的keytool生成证书
![keystore](/path/to/20161017135038.png)<br/><!--more-->
2. 找到tomcat目录/conf/server.xml文件
 
 更改这段代码：
 
    <--<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
                    maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
                    clientAuth="false" sslProtocol="TLS" />-->
  
  为：<br/>
  
    <Connector port="8443" protocol="HTTP/1.1"
                maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
                clientAuth="false" sslProtocol="TLS" 
                keystoreFile="/.keystore" （keystore文件地址）
                keystorePass="123456"/>(生成keystore输入的密码)
3. 验证
    访问https://localhost:8443 验证是否可行
 
注：如果希望能通过域名访问，则需要向相关机构申请https证书
 