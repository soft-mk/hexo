---
title: shadowsocks & finalspeed 服务端搭建
date: 2019-06-4 09:51:00

categories:
- linux

tags:
- linux
- 搭建 shadowsocks
---

#### shadowsocks 服务端
使用 root 用户登陆 , 安装 shadowsocks .
``` php
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-go.sh
chmod +x shadowsocks-go.sh
./shadowsocks-go.sh 2>&1 | tee shadowsocks-go.log
```
脚本安装完成后，已将 shadowsocks-go 加入开机自启动
配置文件
``` bash
vim /etc/shadowsocks/config.json
```
单用户 和 多用户 配置
``` bash
{
 "server":"0.0.0.0",
 "server_port": 13839,
 "local_port":1080,
 "password":"jkdf7nd33eUj",
 "method":"aes-256-cfb",
 "timeout":600
}
{
 "port_password":{
      "13839":"jkdf7nd33eUj",
      "12179":"Ka7KGb4gqwtF",
      "16713":"fJArFv1gQ8Ve",
      "18711":"4aZtRq4frGf5",
      "17739":"e1PDAM35rYG9"
 },
 "method":"aes-256-cfb",
 "timeout":600
 }
```
管理
启动/停止/重启/状态
``` bash
/etc/init.d/shadowsocks start/stop/restart/status
```

#### FinalSpeed 服务端
安装
``` bash
rm -f install_fs.sh
wget  https://github.com/ucoker/finalspeed/raw/master/install_fs.sh
chmod +x install_fs.sh
./install_fs.sh 2>&1 | tee install.log
```
开机启动
``` bash
vim /etc/rc.local
```
加入
``` bash
sh /fs/start.sh
```
确保端口开放
管理 执行一键安装会自动更新
卸载
``` bash
sh /fs/stop.sh ; rm -rf /fs
```
启动
``` bash
sh /fs/start.sh
```
停止
``` bash
sh /fs/stop.sh
```
重新启动
``` bash
sh /fs/restart.sh
```
运行日志
``` bash
tail -f /fs/server.log
```

#### windows 客户端
[下载地址](https://pan.baidu.com/s/1TRcXDzhw9w9DqrgR5Iem-w)
提取码：xe8o

解压安装 Shadowsocks-4.1.6 , 服务器配置如下 , 端口可以自定义 , 密码为 shadowsocks 服务端设置的密码 .
![](https://ws1.sinaimg.cn/large/0060vrlugy1g3oxgz9aj1j30cw0cv0t2.jpg)

执行 finalspeed.exe 文件
配置如下
![](https://ws1.sinaimg.cn/large/0060vrlugy1g3oxpjaly5j30kx09gweu.jpg)