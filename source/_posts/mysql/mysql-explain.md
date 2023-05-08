---
title: mysql EXPLAIN 详解
date: 2021-02-18 15:26:01

categories: 
- mysql

tags: 
- mysql
---
### EXPLAIN 命令
- 使用 
	直接在 SQL 语句前加入 EXPALIN 
- 参数
| id | columns | JSON Name | Meaning |
| :---: | :---: | :---: | :--- |
| 1 | id | select_id | 执行编号，标识select所属的行。如果在语句中没子查询或关联查询，只有唯一的select，每行都将显示1。否则，内层的select语句一般会顺序编号，对应于其在原始语句中的位置 |
| 2 | select_type | None | 显示本行是简单或复杂select。如果查询有任何复杂的子查询，则最外层标记为PRIMARY（DERIVED、UNION、UNION RESUlT） |
| 3 | table | Table Name | 当前表名 |
| 4 | partitions | Partitions | 匹配的分区 |
| 5 | type | Access Type | 数据访问/读取操作类型（ALL、index、range、ref、eq_ref、const/system、NULL） |
| 6 | possible_keys | Possible Keys | 可能用到的索引 |
| 7 | key | key | 经过优化器评估最终使用的索引 |
| 8 | key_len | Key Lenth | 使用到的索引长度 |
| 9 | ref | ref | 显示了之前的表在key列记录的索引中查找值所用的列或常量 |
| 10 | rows | rows | 为了找到所需的行而需要读取的行数，估算值，不精确。通过把所有rows列值相乘，可粗略估算整个查询会检查的行数 |
| 11 | filtered | filtered | 按表条件过滤行的百分比 |
| 12 | Extra | Extra | 额外信息说明 |
- 详解
	- id
	- select_type
	- table
	- type
	- possible_keys
	- key
	- key_len
	- ref
	- rows
	- Extra