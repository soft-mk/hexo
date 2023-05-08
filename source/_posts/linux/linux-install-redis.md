---
title: linux 下安装 redis

date: 2019-02-15 09:27:49

categories:
- linux

tags:
- redis
- 开发
- 安装

---
## 下载 redis
进入  /usr/local/src 目录 , 下载 redis , 解压安装. 
```bash
wget http://download.redis.io/releases/redis-4.0.0.tar.gz
tar zxvf redis-4.0.0.tar.gz 
cd redis-4.0.0
make
cd src
make install
```

## 创建 redis 管理目录
```$xslt
mkdir -p /usr/local/redis/bin 
mkdir -p /usr/local/redis/etc
mv /usr/local/src/redis-4.0.0/redis.conf /usr/local/redis/etc
cd /usr/local/src/redis-4.0.0/src
cp mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-dump redis-cli redis-server /usr/local/redis/bin
```

## 修改 redis.conf , 让 redis 后台运行
找到 daemonize , 将值设置为 yes

## 启动与连接
```$xslt
/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
/usr/local/redis/bin/redis-cli
```

## 常用
查看是否启动
```$xslt
ps -ef | grep redis
```
端口占用
```$xslt
netstat -tunpl | grep 6379
```
停止 redis
```$xslt
/usr/local/redis/bin/redis-cli shutdown
```

