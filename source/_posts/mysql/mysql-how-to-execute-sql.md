---
title: MySQL 日志系统
date: 2019-05-31 18:30:01

categories: 
- mysql

tags: 
- mysql
---

### redo log (重做日志)
InnoDB 引擎独有 , 其他引擎没有次日志 .
当有一条记录需要更新时 , InnoDB 引擎会先把记录写到 redo log 里面 , 并更新内存 , 这个时候更新就算完成了 . 同时 InnoDB 引擎会在适当的时候将这个操作记录更新到磁盘里 , 而这个更新往往是在系统比较空闲的时候 .
redo log 的文件是固定大小的 , 循环写入 , 一旦可用空间不足就会停止写入 , 先将记录更新到数据文件 .
该日志可以保证数据库发生异常的情况下 , 之前提交的记录不会丢失 --- crash-safe .


### binlog (归档日志)







### 区别
redo log 是 InnoDB 引擎特有的 , binlog 是所有引擎都可以使用的 , 在 server 层实现 .
redo log 是物理日志 , 记录的是 "在某个数据页上做了什么修改"; binlog 是逻辑日志 , 记录的事这个语句的原始逻辑 .
redo log 是循环写的 , 空间固定 ; binlog 是可以追加写入的(归档) .