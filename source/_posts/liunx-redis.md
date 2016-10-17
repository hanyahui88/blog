---
title: liunx 安装redis(centos)  
date: 2016-08-05 16:26:29
categories:   部署 
tags: [redis,centos]
---

1. 安装gcc
2. 下载redis，并解压
3. 进去目录，make && make install
4. 把${redis_home}/redis.conf 的daemonize no 改成 daemonize yes 后台运行
5. 进入${redis_home}/src  启动redis   ./redis-server  ../redis.conf 使用配置文件启动
6. 验证是否已经启动  ps -ef |grep redis 