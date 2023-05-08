---
title: 远程仓库
date: 2019-11-25 17:16:58
category: 
- git
tags: 
- git
---

## 添加远程库
#### 先有本地库 , 后创建远程库
```
git remote add origin git@server_name:php/community.git
```

首次推送
```
git push -u origin master
```
后续推送
```
git push origin master
```

#### 先创建远程库
```
git clone git@server_name:php/community.git
```