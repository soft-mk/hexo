---
title: ubuntu20.04.4
date: 2022-04-24 12:38:00
categories:
- linux

tags:
- linux
- init
---

### 安装 nginx
- 创建新的虚拟机
- vmware设置
	- 配置类型选择 典型
	- 稍后安装系统
	- 操作系统选择 Linux , 版本选择 Ubuntu 64位
	- 命名
	![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_044627.png)
	- 指定磁盘容量
	- 自定义硬件
		* 设置 网络适配器 为桥接模式
		* 设置 CD/DVD 为指定的 ISO 映像文件 [下载地址](https://mirrors.aliyun.com/ubuntu-releases/)
	![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_045045.png)
	- 完成

### 安装 ubuntu
- 开启此虚拟机
- 按回车键选择语言
- 由于不可描述的原因 , 修改阿里云安装源
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_045727.png)
- 如果没有特殊需求 , 无需修改硬盘配置 , 使用默认配置
- 创建用户 , 输入用户名和密码
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_050044.png)
- 等待安装完成重启

### 安装完成后配置
- 查看 IP 地址
`ip addr`
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_051240.png)

- 修改默认设置 , 绑定静态 IP
`ls /etc/netplan/`
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_051610.png)
使用编辑工具编辑该配置文件
`sudo vi /etc/netplan/00-installer-config.yaml`
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_053035.png)
- 应用
`sudo netplan apply`
- 查看是否配置成功
`ip addr`
![image](https://kimiadai-1253350770.cos.ap-chengdu.myqcloud.com/202204/clipboard_20220420_053253.png)