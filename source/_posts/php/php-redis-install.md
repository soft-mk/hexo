---
title: linux 安装 php-redis 扩展
date: 2019-02-15 10:20:28

categories:
- PHP

tags:
- redis
- 开发
- 安装
---
## 下载 redis 扩展
下载地址 [http://pecl.php.net/package/redis](http://pecl.php.net/package/redis) 选择对应版本 , 也可以直接执行 
```$xslt
wget http://pecl.php.net/get/redis-4.0.0.tgz
```

## 解压
```$xslt
tar zxvf redis-4.0.0.tgz
cd redis-4.0.0
```

## 在解压的 redis 文件夹下生成 configure 配置文件
```$xslt
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```

## 编译完成后配置 php.ini
```$xslt
extension=redis.so
```
如果找不到 php.ini , 可以在 phpinfo() 中查看 Loaded Configuration File . 
如果值为 none , 可以在编译目录下把 php.ini-development 复制一份到 /usr/local/php/lib 下

## 重启 nginx 或者 apache 
