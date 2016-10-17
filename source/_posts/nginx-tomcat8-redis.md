---
title: nginx-tomcat8-redis 做集群      
date: 2015-12-11 11:54:31
categories:   部署 
tags: [redis,tomcat,nginx,集群,session共享  ]
---
1. nginx 配置

        upstream localhost {
            server localhost:8080 weight=1 max_fails=2 fail_timeout=30s;
            server localhost:8081 weight=1 max_fails=2 fail_timeout=30s;
        }
        server {
                listen       80;
                server_name  localhost;
            
            location / {
                    proxy_connect_timeout   3;  
                    proxy_send_timeout      30;  
                    proxy_read_timeout      30; 
                    proxy_pass http://localhost;
                }          
        }
<!--more-->
2. tomcat 配置
每个tomcat 的context.xml  配置文件 <Context> 节点下 添加下面代码
        
        <Manager className="com.radiadesign.catalina.session.RedisSessionManager" 
        host="localhost" 
        port="6379" 
        database="0"  
        maxInactiveInterval="60" />
3. 添加 tomcat-redis-session.jar包，jedis-2.7.2.jar   commons-pool2-2.4.1.jar；将这3个包放入tomcat\lib目录下；
也可以网上下载 tomcat-redis-session 项目把jedis-2.7.2.jar  和commons-pool2-2.4.1.jar 都编译进去
然后把编译后的包放在toomcat\lib中<br/>
4. 给每个tomcat首页加上sessionid,访问网页验证，看看sessionId是不是一样的<br/>
5. 遇到的错误:
错误1：com/radiadesign/catalina/session/RedisSessionHandlerValve : Unsupported major.minor version 52.0。原因:编译的时候jdk版本过高
错误2：java.lang.IllegalStateException: Race condition encountered: attempted to load session[23D87414FA0F9520F84869F39B545CDB] which has been created but not yet serialized.原因：客户端请求时传了多个JSESSIONID的原因，手动清除cookie，再次请求，问题解决。