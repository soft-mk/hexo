---
title: docker 使用 Dockerfile 安装 php 
date: 2022-08-15 11:49:00
category: 
- docker
tags: 
- docker
- php
---

## 基本环境

系统 : ubuntu-20.04
docker 版本 : 20.10.21

## 编辑 Dockerfile

```sh
FROM php:8.2-fpm

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 更新安装依赖包和PHP核心拓展
RUN apt-get update && apt-get install -y \
            --no-install-recommends  libfreetype6-dev libjpeg62-turbo-dev libpng-dev curl libzip-dev \
            && rm -r /var/lib/apt/lists/* \
            && docker-php-ext-install -j$(nproc) gd bcmath opcache pdo_mysql \
            gettext sockets zip mysqli dba pcntl calendar \
            shmop exif sysvmsg sysvsem sysvshm



# 安装 PECL 拓展，安装Redis，mongodb，amqp

RUN pecl install redis && docker-php-ext-enable redis

RUN pecl install mongodb && docker-php-ext-enable mongodb


# 若在此处安装amqp失败（因为linux系统版本问题查不到包会报错：E: Unable to locate package librabbitmq-dev），可先将下面注释。
# 等安装好后 进入容器执行：
# 1.执行：apt-get update
# 2.再搜索一下： apt-cache search librabbitmq-dev
# 3.如果能查询到再执行 apt-get install librabbitmq-dev -y
# 4.同理，pecl查询下版本：pecl search amqp
# 5.执行：pecl install amqp 1.11.0 -y

#RUN apt-get install librabbitmq-dev -y \
#	&& pecl install amqp 1.11.0 -y \
#	&& docker-php-ext-enable amq

ENV COMPOSER_HOME /root/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

WORKDIR /data
```

## 安装

```sh
docker build -t php:v1 .
```

安装完成后可以进入容器查看

```sh
docker run -it php:v1 sh
php -v
php -m
```

## 打包镜像

[docker 打包 nginx 和 php 镜像](/2022/08/15/docker/docker-push-image)

## docker-composer 安装

[docker-compose 安装 nginx 和 PHP](/2022/08/15/docker/docker-compose)
