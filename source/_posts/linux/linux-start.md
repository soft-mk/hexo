---
title: linux 系统下的启动和重启命令
date: 2019-02-15 11:12:52
categories:
- linux

tags:



---

## nginx

### 重启
```$xslt
/usr/local/nginx/sbin/nginx -s reload
```
### 查看状态
```$xslt
ps -ef | grep nginx
```

## php-fpm
### 启动
```$xslt
/usr/local/php/sbin/php-fpm
```
### 重启
查看 master 进程
```$xslt
ps aux|grep php-fpm
```
kill -USR2 master 进程
```$xslt
kill -USR2 42891
```
INT, TERM 立刻终止
QUIT 平滑终止

USR1 重新打开日志文件

USR2 平滑重载所有worker进程并重新载入配置和二进制模块

## redis
### 查看是否启动
```$xslt
ps -ef | grep redis
```
### 启动redis
```$xslt
/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
```
