---
title: Apache 自带 ab 测试工具使用
date: 2019-06-10 21:27:04

categories:
- apache

tags:
- PHP
- 开发
- apache
---

#### 打开方式
ab 测试工具在 apache 目录下的 bin 文件夹中 , 进入 bin 目录之后可以直接执行 ab .
#### 常用请求参数
```
-n #总请求次数默认为 1
-c #并发次数 , 不能大于总请求次数
-p #post 参数路径 , 与 -T 参数配合使用
-T #请求头设置 
```
#### 无参数请求
```
ab -n 10 -c 10 http://test.com/index.php
```
#### GET 方式请求
```
ab -n 10 -c 10 "http://test.com/index.php?a=1&b=2"
```
url 必须用双引号括起来
#### POST 请求
```
ab -n 10 -c 10 -p D:\params.txt -T application/x-www-form-urlencoded http://test.com/index.php
```
D:/params.txt 的内容如下
```
gid=14659&user_id=1&token=f870b28e-5c04-4a90-9838-654172607287
```

#### 测试结果
![](https://ws1.sinaimg.cn/large/0060vrlugy1g3w3oysk9yj30m20esgn1.jpg)