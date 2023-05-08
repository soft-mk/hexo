---
title: 阿里云 SLB 配置
date: 2021-02-25 15:07:00

categories:
- 阿里云

tags:
- SLB
---

## 创建资源组

[https://resourcemanager.console.aliyun.com/resource-groups](https://resourcemanager.console.aliyun.com/resource-groups)

把需要加入负载均衡的 ecs 实例添加到新建的资源组中

转入或新购资源

![image](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/ACF50D1A-8799-4ff8-8A7B-24F2719EF22C.png)

## 创建负载均衡(应用型负载均衡(按量付费))

[https://slb.console.aliyun.com/alb/cn-beijing/albs](https://slb.console.aliyun.com/alb/cn-beijing/albs)

选择地域/实例网络类型/VPC/可用区/IP模式 , 建议选项如图

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_14-56-28.png)

选择功能版本/计费方式和资源组

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_14-57-24.png)

## 配置域名

添加域名解析记录

记录类型选择 CNAME

记录值是负载均衡的 DNS 名称

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-25-35.png)

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-21-12.png)

申请该域名的 SSL 证书

## 创建后端服务器组

[https://slb.console.aliyun.com/alb/cn-beijing/server-groups](https://slb.console.aliyun.com/alb/cn-beijing/server-groups)

服务器组类型直接选择服务器类型

后端协议选择 http

调度算法按需选择 , 如无特殊需求可直接选择加权轮询

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-02-32.png)

后端服务器组创建完成后开始编辑后端服务器

配置后端服务器的端口和权重 , 权重越大转发的请求越多 , 端口可选 81/89 , 需要配置安全组允许访问 , 如果有防火墙也需要开放端口 , 可以直接在浏览器访问该端口号测试能否正常访问 .

## 创建监听

负载均衡协议选择 https

监听端口 443

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-18-15.png)

选择 SSL 证书

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-30-01.png)

选择服务器组

![img](https://xc-saas.oss-cn-hangzhou.aliyuncs.com/ali/20230306/2023-03-06_15-31-47.png)
