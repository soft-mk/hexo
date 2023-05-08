---
title: linux 常用命令
date: 2019-07-08 11:12:52
categories:
- linux

tags:



---

## 文件操作
```shell
df -h #显示文件系统磁盘块的使用情况  -h human read
du -h --max-depth=1 #显示文件夹占用的存储空间  --max-depth 文件深度
ls -al #list 列出当前工作目录的内容 -a 列出所有(包含 . ..  -A 不包含) -l 列出所有者 组 以及权限 -t 时间排序 
ll #相当与 ls -l
mkdir #创建目录 
rmdir #删除目录
pwd #print working directory
cp FILE PATH #复制文件
mv FILE PATH #移动文件
```

## 查询
- more
```shell
more +100 -10 +/pattern xx.log
+100 从第 100 行开始显示
-10 每页显示 10 行
+/pattern 搜索 pattern 字符串, 从该字符串前两行开始显示

按页查看文件内容, 空格键切换下一页, b 返回上一页, q 退出 , = 输出当前行号
```
- cat
```shell
cat -n xx.log # -n 显示行数
cat -n a.log > b.log # 对 a.log 显示行数并写入 b.log, 覆盖 b.log 的内容
cat -n a.log >> b.log # 对 a.log 显示行数并追加写入 b.log
```
- grep
```shell
cat a.log | grep pattern -A 5 -B 10 -C 3
pattern 查找 a.log 中的 pattern 字符串
-A 5 显示匹配行的后 5 行数据
-B 10 显示匹配行的前 10 行数据
-C 3 显示匹配行的前后 3 行数据

cat a.log | grep pattern -c -i
-c 显示匹配的行数
-i 忽略字符大小写

cat a.log | grep pattern -H -n
-H 显示所属的文件名称
-n 显示行数
```

- awk
```shell

```






## 网络连接