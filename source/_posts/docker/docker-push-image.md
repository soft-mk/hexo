---
title: docker 打包 nginx 和 php 镜像
date: 2022-08-15 19:29:20
category: 
- docker
tags: 
- docker
- php
- nginx
---

## 创建阿里云镜像仓库

- 登录阿里云 , 找到产品中的容器镜像服务并创建个人或企业实例 [https://cr.console.aliyun.com/cn-hangzhou/instances](https://cr.console.aliyun.com/cn-hangzhou/instances)
- 创建命名空间
- 创建镜像仓库

## 在本地拉取 php 镜像

- 通过 Dockerfile 拉取安装指定扩展的 php 版本 , 参考 [docker 使用 Dockerfile 安装 php](/2022/08/15/docker/php)

## 将镜像推送到阿里云镜像仓库

- 将镜像推送到Registry
  
  ```shell
  #登录
  docker login --username=[username] registry.cn-hangzhou.aliyuncs.com
  #打标签
  docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/[命名空间]/[镜像仓库]:[镜像版本号]
  #推送
  docker push registry.cn-hangzhou.aliyuncs.com/[命名空间]/[镜像仓库]:[镜像版本号]
  ```
