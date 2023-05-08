---
title: git 使用 ssh 连接
date: 2022-09-05 17:27:58
category: 
- git
tags: 
- git
---

### 创建密钥文件

进入 git bash 输入
`ssh-keygen -t rsa -f /d/server/mk2920 -C dev@mk2920.com`

-t 指定生成的密钥类型
-f 文件保存路径
-C 注释(邮箱)

### 添加查看密钥

- 启动密钥管理器 `ssh-agent bash`

    ```shell
    SSH_AUTH_SOCK=/tmp/ssh-OttEIgSeih2Y/agent.496; export SSH_AUTH_SOCK;
    SSH_AGENT_PID=497; export SSH_AGENT_PID;
    echo Agent pid 497;
    ```

- 查看 `ssh-add -l`

    ```shell
    3072 SHA256:*************** dev@mk2920.com (RSA)
    ```

- 添加 `ssh-add /d/server/mk2920`
  
    ```shell
    Identity added: /d/server/mk2920 (dev@mk2920.com)
    ```

### 不同项目使用不同密钥

- 编辑配置文件 '~/.ssh/config'

    ```shell
    Host mk
    HostName gitee.com
    IdentityFIle D:/server/mk2920
    User MK

    Host mk
    HostName github.com
    IdentityFIle D:/server/mk2920
    User MK

    Host yangwl
    HostName 192.168.8.100
    IdentityFIle D:/server/login_key/git_login
    User MK
    ```

- 测试 `ssh -T git@github.com`

    ```shell
    Hi MK2920! You've successfully authenticated, but GitHub does not provide shell access.
    ```
