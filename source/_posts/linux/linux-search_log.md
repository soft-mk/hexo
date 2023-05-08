---
title: linux 系统 查询并筛选日志返回结果
date: 2022-02-24
categories:
- linux

tags:
- awk

---
#### 搜索 THINKPHP 的 SQL 耗时范围
- thinkphp 的 SQL 日志记录格式为
```
[2022-02-14T10:00:35+08:00][sql] SELECT * FROM `eb_system_config` WHERE  `menu_name` = 'site_logo' LIMIT 1 [ RunTime:0.002698s ]
[2022-02-14T10:00:35+08:00][sql] SELECT * FROM `eb_system_menus` WHERE  `is_show` = 1  AND `access` = 1 ORDER BY `sort` DESC [ RunTime:0.001589s ]
[2022-02-14T10:00:35+08:00][sql] SELECT `menu_name`,`value` FROM `eb_system_config` [ RunTime:0.000803s ]
[2022-02-14T10:00:35+08:00][sql] SELECT * FROM `eb_system_config` WHERE  `menu_name` = 'cache_config' LIMIT 1 [ RunTime:0.000413s ]
[2022-02-14T10:00:35+08:00][sql] SHOW FULL COLUMNS FROM `eb_system_role` [ RunTime:0.001837s ]
[2022-02-14T10:00:35+08:00][sql] SELECT `role_name` FROM `eb_system_role` WHERE  `id` = 1 LIMIT 1 [ RunTime:0.002040s ]
```

- 查询命令
```
cat /log/*.log | awk -F 'RunTime:' '{print $2}' | awk -F 's' '{print $1}' | awk '$NF>0.002{print $NF}' | wc -l
```
- 详解
	- cat /log/*.log
	输出 /log 目录下的所有 .log 文件
	- | awk -F 'RunTime:' '{print $2}'
	输出内容后 , 以 `Runtime:` 为关键字进行切割 , 得到两部分内容 , `Runtime:` 之前是 `$1` , 我们需要的是 Runtime 之后的执行时间 , 所以取 `$2` , 如 `0.002040s ]` .
	- | awk -F 's' '{print $1}'
	以 `s` 为关键字进行切割 , 并取切割后的第一部分内容 , 即每条记录的执行时间 , 如 `0.002040`
	- | awk '$NF>0.002{print $NF}'
	拿到执行时间 `$NF` 后和 `0.002` 对比 , 如果条件成立 , 则输出 `$NF`
	- | wc -l
	统计符合条件的数量
	
