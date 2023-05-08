---
title: centOs 安装 php 7.3
date: 2019-06-18 21:27:04

categories:
- linux

tags:
- PHP
- 开发
- 安装
---

### 下载依赖
```
yum -y install libxml2 libxml2-devel
yum -y install openssl openssl-devel
yum -y install curl curl-devel
yum -y install libjpeg libjpeg-devel
yum -y install libpng libpng-devel
yum -y install freetype freetype-devel
yum -y install pcre pcre-devel
yum -y install libxslt libxslt-devel
yum -y install bzip2 bzip2-devel
```

安装最新版 libzip
```
#删除旧版
yum remove libzip

#下载 libzip-1.5.2
cd /usr/local/src
wget https://nih.at/libzip/libzip-1.5.2.tar.gz

#新版 libzip 需要 cmake 编译 , 下载 cmake
wget https://github.com/Kitware/CMake/releases/download/v3.15.0-rc1/cmake-3.15.0-rc1-Linux-x86_64.tar.gz
tar -zxvf cmake-3.15.0-rc1-Linux-x86_64.tar.gz
mv cmake-3.15.0-rc1-Linux-x86_64.tar.gz /usr/local/cmake
export PATH=$PATH:/usr/local/cmake/bin

#解压安装 libzip
tar -zxvf libzip-1.5.2.tar.gz
cd libzip-1.5.2
mkdir build
cd build
cmake ..
make & make install
```

### 下载编译 php7.3.0
```
cd /usr/local/src
wget "https://downloads.php.net/~cmb/php-7.3.0.tar.gz"
tar -zxvf php-7.3.0.tar.gz
cd php-7.3.0
#编译 参数自行添加
./configure --prefix=/usr/local/php \
 --with-curl=/usr/local/curl\
 --with-gd \
 --with-freetype-dir=/usr/include/freetype2\
 --with-gettext \
 --with-iconv-dir \
 --with-kerberos \
 --with-libdir=lib64 \
 --with-libxml-dir \
 --with-mysqli \
 --with-openssl \
 --with-pcre-regex \
 --with-pdo-mysql \
 --with-pdo-sqlite \
 --with-pear \
 --with-png-dir \
 --with-xmlrpc \
 --with-xsl \
 --with-zlib \
 --enable-fpm \
 --enable-bcmath \
 --enable-libxml \
 --enable-inline-optimization \
 --enable-mbregex \
 --enable-mbstring \
 --enable-opcache \
 --enable-pcntl \
 --enable-shmop \
 --enable-soap \
 --enable-sockets \
 --enable-sysvsem \
 --enable-xml \
 --enable-zip

make
make install

#成功输出
Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20180731/
Installing PHP CLI binary:        /usr/local/php/bin/
Installing PHP CLI man page:      /usr/local/php/php/man/man1/
Installing PHP FPM binary:        /usr/local/php/sbin/
Installing PHP FPM defconfig:     /usr/local/php/etc/
Installing PHP FPM man page:      /usr/local/php/php/man/man8/
Installing PHP FPM status page:   /usr/local/php/php/php/fpm/
Installing phpdbg binary:         /usr/local/php/bin/
Installing phpdbg man page:       /usr/local/php/php/man/man1/
Installing PHP CGI binary:        /usr/local/php/bin/
Installing PHP CGI man page:      /usr/local/php/php/man/man1/
Installing build environment:     /usr/local/php/lib/php/build/
Installing header files:          /usr/local/php/include/php/
Installing helper programs:       /usr/local/php/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php/php/man/man1/
  page: phpize.1
  page: php-config.1
Installing PEAR environment:      /usr/local/php/lib/php/

Warning: "continue" targeting switch is equivalent to "break". Did you mean to use "continue 2"? in phar:///usr/local/src/php-7.3.0/pear/install-pear-nozlib.phar/PEAR/PackageFile/v2/Validator.php on line 1933
[PEAR] Archive_Tar    - installed: 1.4.3
[PEAR] Console_Getopt - installed: 1.4.1
[PEAR] Structures_Graph- installed: 1.1.1
[PEAR] XML_Util       - installed: 1.4.2
[PEAR] PEAR           - installed: 1.10.5
Wrote PEAR system config file at: /usr/local/php/etc/pear.conf
You may want to add: /usr/local/php/lib/php to your php.ini include_path
/usr/local/src/php-7.3.0/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin
ln -s -f phar.phar /usr/local/php/bin/phar
Installing PDO headers:           /usr/local/php/include/php/ext/pdo/
```

配置信息
```
# 复制 php.ini php-fpm.conf www.conf 配置文件
cp php.ini-production /usr/local/php/lib/php.ini
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
ln -s /usr/local/php/sbin/php-fpm /usr/local/bin

#加入服务
cp /usr/local/src/sapi/fpm/php-fpm.service /usr/lib/systemd/system/

#php 命令
export PATH=$PATH:/usr/local/php/bin/
#测试
php -v
php -m
```
