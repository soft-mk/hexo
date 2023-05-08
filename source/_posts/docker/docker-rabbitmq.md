---
title: docker 之 rabbitmq 安装部署 
date: 2022-07-26 11:49:00
category: 
- docker
tags: 
- docker
- rabbitmq
---

## 常用操作

| 操作 | 命令 | 示例 | 说明 |
| ---- | ---- | ---- | ---- |
| 检索 | docker search keyword | docker search rabbitmq:management | 搜索 docker 镜像 |
| 拉取 | docker pull keyword:tag | docker pull rabbitmq:management | 拉取镜像 , 不指定 tag , 则默认拉取最新版 |
| 列表 | docker images | -- | 查看本地仓库的所有镜像 |
| 查看 | docker ps | -- | 查看运行中的容器 |
| 启动 | docker start/stop/rm containerID | -- | 启动容器 |
| 删除 | docker rmi imageId | docker rmi 640s2d2w8hx5sw | 删除 docker 镜像 |

## 搜索安装 rabbitmq

- 搜索 rabbitmq

    ```shell
    docker search rabbitmq:management
    ```

- 拉取

    ```shell
    docker pull rabbitmq:management
    ```

- 查看镜像

    ```shell
    docker images
    ```

- 启动容器

  - 简单版

    ```shell
    docker run -d -p 5672:5672 -p 15672:15672 --name rabbitmq rabbitmq:management
    ```
  
  - 复杂版 (设置账户密码，hostname)

    ```shell
    docker run -d -p 15672:15672  -p  5672:5672  -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin --name rabbitmq --hostname=rabbitmqhostone  rabbitmq:management
    ```

  - 通过 image ID 启动 , 其中 `13fa` 是 image ID 的前四位

    ```shell
    docker run -d -p 15672:15672 -p 5672:5672 --name rabbitmq 13fa
    ```

## 初始化设置

rabbitmq 默认用户名和密码都是 `guest` , 该账户远程网络访问受限 , 所以我们一般都会新增一个账户用来连接 .

- 进入容器内部

    ```shell
    docker exec -i -t 91a0 bin/bash
    ```

其中 `91a0` 是容器ID 的前四位 , 容器ID 太长 , 无需全部写上

- 添加用户 , `admin` 是账号 , `25s14q` 是密码

    ```shell
    rabbitmqctl add_user admin 25s14q
    ```

- 设置用户权限 , 赋予 `admin` 用户所有权限

    ```shell
    rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"
    ```

- 设置用户角色 , 赋予 `admin` 用户 `administrator` 角色

    ```shell
    rabbitmqctl set_user_tags admin administrator
    ```

- 查看用户设置

    ```shell
    rabbitmqctl list_users
    ```
