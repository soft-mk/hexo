---
title: hexo 写作
date: 2019-01-25 17:16:58
category: 
- hexo
tags: 
- hexo 写作
---

### 新增分类页面
进入项目根目录下 , 生成 page
```$xslt
hexo new page categories
```
在 /source/categories/index.md 的 front-matter 中加入
```$xslt
type: 'categories'
```

### 新增标签页面

```$xslt
hexo new page tags
```
在 /source/tags/index.md 的 front-matter 中加入
```$xslt
type: 'tags'
```

### 使用标签和分类
```$xslt
hexo new post 'filename'
```
直接在 md 文件的 front-matter 中加入 分类和标签
```$xslt
category: 
- hexo #分类
tags: 
- 安装hexo #标签
- 主题 #标签
```

next 主题下使用超链接 
```$xslt
[Hexo themes](https://hexo.io/themes/)
```