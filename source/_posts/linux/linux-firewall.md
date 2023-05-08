---
title: centOs7+ 版本防火墙设置
date: 2020-01-19 14:51:00

categories:
- linux

tags:
- linux
- 防火墙
---

#### 服务管理
安装 firewall
``` php
yum -y install firewalld firewall-config 
```
开机启动 | 关闭开机启动
```
systemctl enable|disable firewalld
```
启动 | 关闭 | 重启 | 查看状态
```
systemctl start|stop|restart|status firewalld
```

#### firewalld-cmd 命令管理端口
查看防火墙是否正在运行
```
firewall-cmd --state
```
查看所有开启的端口
```
firewall-cmd --zone=public --list-ports
```
开启关闭端口 以 80 端口为例 (--permanent 为永久生效 , 否则重启后失效)
```
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --remove-port=80/tcp --permanent
```
修改端口后需要重载
```
firewall-cmd --reload
```