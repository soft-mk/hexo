---
title: 创建版本库
date: 2019-11-25 14:16:58
category: 
- git
tags: 
- git
---

## 创建版本库
新建一个文件夹 , 并在该文件夹内运行命令行 .
```
git init
```
可以在文件夹内看到自动生成的 .git 文件夹 , 自行修改此文件夹内容会破坏 git 仓库 .

## 把文件添加到版本库
新建 readme.txt 文件 . 写入文字介绍 .
```
git add readme.txt
```
git add 没有返回信息
```
git commit -m "commit text"
```
-m 参数是提交说明
返回改动的文件数量和改动行数 .
