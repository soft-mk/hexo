---
title: windows 使用密钥登录 linux 服务器 (putty)
date: 2019-11-11 19:51:00

categories:
- linux

tags:
- linux
- putty 实现密钥登录
---

#### 先用密码登录 linux 服务器 , 生成密钥
``` bash
ssh-keygen -t rsa
```

生成密钥的过程中会提示输入密码 , 可以直接 enter 跳过 . 如果输入密码的话 , 以后每次登录都需要输入密码 .

#### 部署密钥
``` bash
cd /root/.ssh
ssh-copy-id -i /root/.ssh/id_rsa.pub root@yourip
yes
```
.ssh 文件夹中的 id_rsa 是私钥文件 , 需要下载到本地电脑用来登录 .

#### 下载 id_rsa 文件到本地
打开 puttygen 
![](https://ws1.sinaimg.cn/large/0060vrlugy1g8uc5tt10nj30dp0da0tg.jpg)

1. load , 选择 id_rsa 文件
2. 保存私钥到本地 (.ppk 文件)
3. 复制私钥 , 并将私钥保存到服务器 /root/.ssh/authorized_keys 中

#### 使用 putty 登录
填入 IP 地址
![](https://ws1.sinaimg.cn/large/0060vrlugy1g8v8abmhk1j30cw0ch0t2.jpg)

填入用户名
![](https://ws1.sinaimg.cn/large/0060vrlugy1g8v8cckiooj30cy0ch74x.jpg)

选择之前保存的 .ppk 私钥文件
![](https://ws1.sinaimg.cn/large/0060vrlugy1g8v8e4cy3yj30cy0ch0t8.jpg)

返回 session 保存站点
![](https://ws1.sinaimg.cn/large/0060vrlugy1g8v8f4yi27j30cy0ch0t5.jpg)

尝试登录