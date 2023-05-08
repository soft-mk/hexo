---
title: docker-compose 安装 nginx 和 PHP
date: 2022-08-15 20:30:00
category: 
- docker
tags: 
- docker
- php
---

## 基本环境

系统 : ubuntu-20.04
docker 版本 : 20.10.21

## 安装 docker-compose

```sh
sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## 编辑 docker-compose.yml 文件

```sh
version: '3'
services:
  nginx-1-20:
    container_name: nginx-1-20
    image: registry.cn-hangzhou.aliyuncs.com/xciot/nginx:v1
    ports:
    - 82:80
    #- 443:443
    # 文件映射
    volumes:
    - /www/wwwroot:/usr/share/nginx/html
    - ./nginx/nginx.conf:/etc/nginx/nginx.conf
    - ./nginx/conf.d:/etc/nginx/conf.d
    - ./nginx/logs:/var/log/nginx
    # 指定 PHP 版本的 container_name
    depends_on:
      - php74
      - php80
    restart: always

  #php74
  php74:
    container_name: php74
    image: registry.cn-hangzhou.aliyuncs.com/xciot/php74:v1
    # 文件映射
    volumes:
      - /www/wwwroot:/usr/share/nginx/html
      - ./php74/php.ini:/usr/local/etc/php/php.ini
      - ./php74/php-fpm.d:/usr/local/etc/php-fpm.d

    restart: always

  #php80
  php80:
    container_name: php80
    image: registry.cn-hangzhou.aliyuncs.com/xciot/php80:v1
    # 文件映射
    volumes:
      - /www/wwwroot:/usr/share/nginx/html
      - ./php80/php.ini:/usr/local/etc/php/php.ini
      - ./php80/php-fpm.d:/usr/local/etc/php-fpm.d

    restart: always
```

## 安装

```sh
docker-compose up -d
```
