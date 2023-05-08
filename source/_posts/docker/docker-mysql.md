---
title: docker 之 mysql 安装部署 
date: 2022-08-29 11:49:00
category: 
- docker
tags: 
- docker
- mysql
---

## 搜索安装 mysql

- 搜索 mysql

  ```shell
  docker search mysql
  ```

  也可以访问 [https://hub.docker.com/_/mysql/tags](https://hub.docker.com/_/mysql/tags) Mysql 镜像库

- 拉取

  ```shell
  docker pull mysql:latest
  ```

- 查看镜像
  
  ```shell
  docker images
  ```

- 启动容器
  
  ```shell
  docker run --name mysql-name -p 3306:3306 -v /opt/docker/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=password -d mysql:5.7
  ```

  - `-p 3306:3306` 将容器的 3306 端口映射到主机的 3306 端口
  - `-v /opt/docker/mysql/conf:/etc/mysql/conf.d` 将主机 /opt/docker/mysql/conf 目录挂载到容器的 /etc/mysql/conf.d
  - `-e MYSQL_ROOT_PASSWORD=123456` 初始化 root 密码
  - `-d` 后台运行容器，并返回容器ID
  - `mysql:5.7` name:tag

## 配置文件

- 进入容器内部

  ```shell
  docker exec -i -t mysql-name bin/bash
  ```
