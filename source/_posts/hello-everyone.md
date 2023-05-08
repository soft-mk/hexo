---
title: 安装 hexo
date: 2019-01-25 15:16:58
category: 
- hexo
tags: 
- 安装hexo
- 主题
---

## 开始使用 HEXO 写 BLOG

hexo 搭建 , 依赖 node.js 和 git , 需要先安装以上两个环境 .

安装完成之后进入目录 , 直接运行命令

``` bash
npm install -g hexo-cli
```

等到安装完成后 , 开始创建项目

``` bash
hexo init <folder>
cd <folder>
npm install
```

出现错误的话自行谷歌 , 接下来开始更换主题 , 可以在 [Hexo themes](https://hexo.io/themes/) 中查找新的主题 . 选用当下比较流行的 [next](https://github.com/theme-next/hexo-theme-next) 主题 , 从 git 上 clone 下来 .

``` bash
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改语言和主题 , 在项目根目录下打开 _config.yml 文件 , 

```$xslt
language: zh-CN
theme: next
```

查看效果
```$xslt
hexo clean
hexo g
hexo s
```

访问浏览器 [http://localhost:4000](http://localhost:4000)