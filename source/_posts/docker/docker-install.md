---
title: 安装 docker 
date: 2022-07-26 11:49:00
category: 
- docker
tags: 
- docker
---

## CentOS

### 系统要求

Docker 支持 64 位版本 CentOS 7/8，并且要求内核版本不低于 3.10。 CentOS 7 满足最低内核的要求，但由于内核版本比较低，部分功能（如 overlay2 存储层驱动）无法使用，并且部分功能可能不太稳定。

### CentOS 使用 yum 安装

- 安装依赖

```shell
sudo yum install -y yum-utils
```

- 使用国内源

```shell
# 阿里源
sudo yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sudo sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

# 官方源
sudo yum-config-manager \
     --add-repo \
     https://download.docker.com/linux/centos/docker-ce.repo
```

- 安装 docker

```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

- 启动 docker

```shell
sudo systemctl enable docker
sudo systemctl start docker
```

### 防火墙

CentOS8 防火墙使用了 `nftables`，但 `Docker` 尚未支持 `nftables`， 我们可以使用如下设置使用 `iptables`：

```shell
firewall-cmd --permanent --zone=trusted --add-interface=docker0
firewall-cmd --reload
```

## Ubuntu 20.04

- 更新现有的软件包列表

```sh
sudo apt update
```

- 安装一些必备软件包，让 apt 通过 HTTPS 使用软件包

```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

- 将官方 Docker 版本库的 GPG 密钥添加到系统中

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

- 将 Docker 版本库添加到APT源

```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

- 用新添加的 Docker 软件包来进行升级更新

```sh
sudo apt update
apt-cache policy docker-ce
```

- 安装 Docker

```sh
sudo apt install docker-ce
```
