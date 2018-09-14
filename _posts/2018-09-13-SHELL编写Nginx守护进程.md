---
title: SHELL编写Nginx守护进程
date: 2018-09-13 09:50:00
categories:
- shell
tags:
- shell
---

### 实现目录
监控nginx进程，当发现nginx进程down掉，可以自动启动nginx服务。
```
#/bin/bash
#description: this is a deamon about nginx.
#version: v0.0.1
#author: biezz
#date: 2018-09-10

d=`date "+%Y%m%d"`
echo $d
echo ^[[32mDeamon\'s pid is:$$^[[37m
n=1
while :; do
    sn=`ps -ef |grep nginx|grep -v grep|awk '{print $2}'`
    echo $sn
    if [ "${sn}" == "" ];then
        let n++
        echo $n
        cp /root/deamon/nginx.log /root/deamon/nginx_$d.log
        rm /root/deamon/nginx.log
        nohup /usr/local/nginx/sbin/nginx > /root/deamon/nginx.log
        echo Starting ok!
    else
        echo Nginx is running.
    fi
    sleep 5
done
```  
如果是需要开机启动，这里拿nginx作为例子，针对源码安装的服务，因为某些服务是可以直接设置开机自动启动。  
```
vim /etc/init.d/deamon.sh
#!/bin/bash
#chkconfig:2345 80 90
#description: This is a Daemon
#author: biezz
#date: 2018-08-03

/root/deamon/deamon.sh >>/root/deamon/deamon.log 2>&1 &
```
