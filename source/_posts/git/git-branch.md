---
title: 分支管理
date: 2019-11-25 17:16:58
category: 
- git
tags: 
- git
---

## 创建与合并
#### 创建分支并切换
```
git checkout -b dev
```
相当于 创建分支 `git branch dev` 切换分支 `git checkout dev` 两条命令

查看当前分支 , `git branch` 会列出所有分支 , 分支前带 * 号的是当前分支 .
```
git branch
```

切换完分支之后 , 可以在该分支下正常的修改提交 .

#### 合并分支
在 dev 分支上开发完毕后 , 切换回 master 分支 .
```
git checkout master
```
合并 dev 分支到主分支 master 上 , `git merge` 用于合并指定分支到当前分支 .
```
git merge dev
```

#### 切换分支
创建并切换分支 git switch 部分版本不可用 . 
```
git switch -c dev
```
切换分支
```
git switch master
```

#### 删除分支
删除 dev 分支
```
git branch -d dev
```

## 冲突解决
两个分支在同一行进行修改的时候 , 会在 `git merge` 的时候出现冲突 .
可以在 `git status` 查看冲突文件 .

```
<<<<<<< HEAD
这是 dev-yang 分支修改的东西 改 MASTER 里面的东西
=======
这是 dev-yang 分支修改的东西 
>>>>>>> dev-y
```
git 用 `<<<<<<<` `=======` `>>>>>>>` 标记出不同的分支
修改完冲突文件后 , `git add` `git commit` .

使用带参数的 `git log` 查看分支的合并情况
```
git log --graph --pretty=oneline --abbrev-commit
```
![](https://ws1.sinaimg.cn/large/0060vrlugy1g9agdqecsyj30b604cwef.jpg)