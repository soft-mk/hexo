---
title: 版本回退与撤销修改
date: 2019-11-25 14:16:58
category: 
- git
tags: 
- 版本回退
---

## 查看版本
```
git log
```
![](https://ws1.sinaimg.cn/large/0060vrlugy1g9a9zo0fsrj30eq08cglm.jpg)

commit 之后的字符串代表版本号(commit id) , HEAD => 当前版本 , Author => 作者 , Date => 上传时间
git log 可以加上 --pretty=oneline 参数 , 只显示单行 . 

![](https://ws1.sinaimg.cn/large/0060vrlugy1g9aa4il22uj30g202eq2s.jpg)


## 回退到上一版本
```
git reset --hard HEAD^
```
HEAD^ => 上个版本 , HEAD^^ => 上上个版本 , 以此类推 .
HEAD~10 回退到之前第 10 个版本 . 
```
git reset --hard bb2998
```
回退到指定版本 , 版本号不需要写全 , 一般 5 位即可 , 太少可能会无法正确回退


## 查看执行过的命令
```
git reflog
```
可以看到执行过的命令 , 回退版本之后 , 如果想切换回最新版本 , 可以用这个命令查看最新版本的版本号 . 

## 撤销修改
#### git checkout -- filename
文件还在工作区 , 未添加到暂存区 . 可以用 ` git checkout -- filename ` 来丢弃工作区的修改 .
`git checkout -- filename` 让文件恢复到最近一次 `git add` 或者 `git commit` 的状态 .
#### `git reset`
```
git reset HEAD filename
```
撤销所有更改 , 回到最新版本
