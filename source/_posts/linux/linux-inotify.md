---
title: rsync + inotify 实时同步
date: 2019-11-26 16:02:00

categories:
- linux

tags:
- linux
---

### inotify-tool

Inotify可以监控文件系统中添加、删除，修改、移动等各种事件

##### 检查环境
`uname -r` 检查内核版本 , 2.6.13 之后的版本才能支持 inotify
```
[root@localhost /]# uname -r
3.10.0-957.el7.x86_64
[root@localhost /]# cat /etc/redhat-release
CentOS Linux release 7.6.1810 (Core)
```
2.6.13 之后的版本可以查到这三个文件
```
[root@localhost /]# ll /proc/sys/fs/inotify/
总用量 0
-rw-r--r-- 1 root root 0 11月 26 12:35 max_queued_events
-rw-r--r-- 1 root root 0 11月 26 12:35 max_user_instances
-rw-r--r-- 1 root root 0 11月 26 12:35 max_user_watches

```
文件说明
`max_user_watches` 设置inotifywait或inotifywatch命令可以监视的文件数量（单进程）
`max_user_instances` 设置每个用户可以运行的inotifywait或inotifywatch命令的进程数
`max_queued_events` 设置inotify实例事件（event）队列可容纳的事件数量

##### yum 安装
```
yum install -y inotify-tools
```
##### 参数
```
/usr/bin/inotifywait -mrq --fromfile /www/server/scripts/inotify_exclude.list --format '%w%f' -e create,close_write,delete $Path

--fromfile 忽略监听文件 , 当需要忽略多个文件或文件夹的时候使用 , inotify_exclude.list 中使用 @/www/www/test_back/data 来忽略 data 文件夹 , 每个一行 .
```

### 文件同步工具 rsync(remote sync)
```
rsync -aze 'ssh -i ~/.ssh/id_rsa_dev' $LocalPath --delete $remoteUser@$RemoteServer:$RemotePath
```
##### 参数说明
```
$LocalPath 本地需要同步的文件路径
$remoteUser 远程服务器用户 与 ssh 密钥指定的用户相同
$RemoteServer 远程服务器 IP 地址
$RemotePath 远程服务器的文件路径
-a 包含-rtplgoD选项
-r 同步目录时要加上，类似 cp 命令的 -r 选项
-v 同步时显示一些信息，让我们知道同步的过程
-l 保留软链接
-L 同步软链接时会把源文件一起同步
-p 保持文件的权限属性
-o 保持文件的属主
-g 保持文件的属组
-D 保持设备文件信息
-t 保持文件的时间属性
--delete 删除 RemotePath 中 LocalPath 没有的文件
--exclude 过滤指定文件 , 如 --exclude "logs" 会把文件名包含 logs 的文件或者目录过滤掉
-u 如果 RemotePath 中的文件比 LocalPath 新，就不会同步
-z 传输时压缩
-e 使用 ssh 连接 remote 服务器
```

##### 脚本示例
`vim /www/server/scripts/inotify.sh`
```
#!/bin/bash
#id_rsa path
#IdRsaPath=/root/.ssh/id_rsa_dev
Path=/var/test_back
BackPath=/var/test_back
BackupServer=192.168.9.122

/usr/bin/inotifywait -mrq --fromfile /www/server/scripts/inotify_exclude.list --format '%w%f' -e create,close_write,delete $Path  | while read line  
do
    if [ -f $line ];then
		BackPathLine=${line%/*}/
        rsync -aze 'ssh -i ~/.ssh/id_rsa_dev' $line --delete root@$BackupServer:$BackPathLine
    else
        echo $line
    fi
done

```

###### 启动脚本
启动前先在 bash 同级目录下新建 inotify.log 文件 , 用来记录监听事件 .
```
nohup ./inotify.sh >> inotify.log &
```

###### 权限问题
使用 git hooks 自动部署的时候 , 部署文件夹的用户和用户组都是 git . 如果使用脚本同步该部署文件夹的话 , 会把文件权限和属主属组一起传输过去 . 所以在目标服务器中使用 inotify 监听文件夹 , 发现文件改动就将整个文件夹的权限改成 web 用户 www .
```
#!/bin/bash
#id_rsa path
#IdRsaPath=/root/.ssh/id_rsa_dev
Path=/var/test_back

/usr/bin/inotifywait -mrq --fromfile /www/server/scripts/exclude_inotify.list --format '%w%f' -e create,close_write,delete $Path  | while read line  
do
    echo $line
    if [ -f $line ];then
		chmod -R 777 /var/test_back && chown -R www:www /var/test_back
    else
        echo 'no line'
    fi
done

```


###### 不使用 inotify 实现文件传输
修改 git hooks , 在 post-recieve 中使用 rsync 传输文件 , 并在传输完成后调用远程服务器的脚本改变文件夹权限 .
```
#exec git update-server-info
homeDir=/var/www/html/diary/
testDir=/var/www/test/diary/
unset GIT_DIR

while read oldrev newrev refname
do
    branch=$(git rev-parse --symbolic --abbrev-ref $refname)
    echo $branch
    if [ "develop" == $branch ];
    then
        cd $homeDir
        echo ' ----------- git checkout ---------- '
        #git checkout $branch
        echo ' ----------- git pull and rsync files ---------- '
        git pull && rsync -aze 'ssh -i ~/.ssh/id_rsa_dev' $homeDir --delete root@$BackupServer:$testDir && ssh -i ~/.ssh/id_rsa_dev root@$BackupServer /www/script/change_mod_own.sh
    else
        echo "nothing to do with this branch"
    fi

done

```