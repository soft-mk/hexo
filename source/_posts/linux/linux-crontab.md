---
title: linux crontab 计划任务
date: 2019-07-09 16:10:52
categories:
- linux

tags:



---

## crontab 参数

```shell
crontab -e #编辑计划任务
crontab -l #查看
```

crontab 格式 "M H D m d cmd" , 其中 M 为分钟(0-59) , H 为小时(0-23) , D 为天(1-31) , m 为月(1-12) , d 为每周天数(0-6) 0 是周日 , cmd 表示要运行的程序或者 sh 文件
```shell
*/10 * * * * command #每 10 分钟执行
0 * * * * command #每小时执行
0 0 * * * command #每天执行
0 0 1 * * command #每月执行
0 0 1 1 * command #每年执行
0 0 * * 0 command #每周执行一次
0 2 * * * command #每天 2 点执行
```

特殊符号
 , (逗号) 代表分隔时段
 ```shell
 0 2,5,8 * * * command #代表每天 2 点 5 点 8 点各执行一次
 ```
  - (中划线) 代表时间区间
 ```shell
 0 10-20 * * * command #代表每天 10 点到 20 点各执行一次
 ```
  /n (n为合理数值)
```shell
*/5 * * * * command #代表每 5 分钟执行一次
```