---
title: linux 系统下备份 mysql 数据库
date: 2019-02-25 11:26:01

categories: 
- mysql

tags: 
- mysql
- linux
---
### mysql-backup
创建 shell script 备份脚本
```php
vim mysql-backup.sh
```
```php
#!/bin/sh
# This is a mysql datbase backup shell script.

# set mysql info
hostname="localhost"
user="root"
password="my password"

# set database info
database="bak database name"
bakpath="path to backup"
date=$(date +%Y%m%d_%H%M%S)

# backup
mkdir -p $bakpath
mysqldump -h$hostname -u$user -p$password $database | gzip \ 
> $bakpath/$database_$date_sql.gz
```

### shell 脚本完整版
```
#!/bin/bash

source /etc/profile #加载系统环境变量
source ~/.bash_profile #加载用户环境变量
user="root"
password="ZGL7t5RhTHhkJHaC"
host="localhost"
port="3306"
db=("gift")

lock="--single-transaction"
mysql_path="/www/server"
backup_path="${mysql_path}/backup"
date=$(date +%Y-%m-%d_%H-%M-%S)
day=7
backup_log="${mysql_path}/backup.log"

#建立备份目录
if [ ! -e $backup_path ];then
  mkdir -p $backup_path
fi

#删除 $day 之前的备份
find $backup_path -type f -mtime +$day -exec rm -rf {} \; > /dev/null 2>&1
echo "备份数据库:${db[*]}"

#备份
backup_sql(){
  dbname=$1
  backup_name="${dbname}_${date}.sql.gz"
  mysqldump -h$host -u$user -p$password $lock --flush-logs $dbname | gzip > $backup_path/$backup_name
  echo $dbname
  echo $backup_name
  if [[ $? == 0 ]];then
    cd $backup_path
    size=$(du $backup_name -sh | awk '{print $1}')
    echo "$datee 备份 $dbname($size) 成功"
  else
    cd $backup_path
    rm -rf $backup_name
    echo "$date 备份失败"
  fi
}

backup_sql ${db[*]}

```

### 创建定时任务执行 shell script

### 手动备份
备份一个数据库
```shell
mysqldump -hhostname -uusername -pmypwd databasename > /path to backup/bakname.sql
```
备份并压缩
```shell
mysqldump -hhostname -uusername -pmypwd databasename ｜ gzip > /path to backup/bakname.sql.gz
```
备份数据库一些表
```shell
mysqldump -hhostname -uusername -pmypwd databasename table1 table2 table3 > /path to backup/bakname.sql
```
仅备份数据库结构
```shell
mysqldump -no-data -databases databasename1 databasename2 databasename3 > /path to backup/bakname.sql
```
备份所有数据库
```shell
mysqldump -all-databases > /path to backup/bakname.sql
```

### 还原数据库
还原无压缩数据库
```shell
mysql －hhostname -uuser -pmypwd databasename < /path to backup/bakname.sql
```
还原压缩数据库
```shell
gunzip < /path to backup/bakname.sql.gz | mysql -hhostname -uusername -pmypwd databasename
```

### 迁移到新的服务器
```shell
mysqldump -hhostname -uuser -pmypwd databasename | mysql -hnew_hostname -C databasename
```
[链接https://www.jianshu.com/p/b77dfd6d998b](https://www.jianshu.com/p/b77dfd6d998b)


