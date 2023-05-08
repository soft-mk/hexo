---
title: 同步代码
date: 2019-11-26 15:12:04
category: 
- git
tags: 
- git
---

## 同步代码
服务器上的仓库位置 `/www/server/project.git` , 服务器上项目代码位置 `/www/wwwroot/project` .

进入 `/www/server/project.git` 的 `hooks` 目录下 , 复制一份 post-update.sample
```
cp post-update.sample post-update
vim post-update
```
post-update 内容如下
```bash
#!/bin/sh

unset GIT_DIR

NowPath=`pwd`
DeployPath="/www/wwwroot/project"

cd $DeployPath

git pull origin master

cd $NowPath

exit 0

```

如果出现 error , 大部分是权限错误 .
