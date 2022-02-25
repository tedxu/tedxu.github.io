---
layout: post
title: 建立 Github 博客站点
date: '2022-02-25 17:25:16 +0800'
categories: jekyll github
published: true
---

# 参考来源

[Github Pages 创建 Jekyll 站点手册](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

[Jekyll 安装](https://jekyllrb.com/docs/installation/)

# Jekyll

[Jekyll](https://jekyllrb.com/) 是一个 Ruby 编写的轻量建站工具，它使用文件系统保存所有内容，避免了使用数据库，所以提供的是纯静态数据展示，优点是简单。

# Github Pages

[Github Pages](https://docs.github.com/en/pages) 是 Github 的功能，可以使用一个 github repo 作为静态站点的后台存储。

[在 Github Pages 上创建 Jekyll 站点](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

# 开始发布博客

博客文章放置在 Jekyll 的 `_posts` 目录下，必须是以下列格式作为文件名

```
YYYY-MM-DD-title.<type>
```

其中 type 标识文件格式，至少有以下可选的文件格式：

- markdown
- markup

# Jekyll 编辑器

[这里](https://github.com/planetjekyll/awesome-jekyll-editors) 有一个 Jekyll 编辑器列表。[prose.io](https://prose.io/) 是一个好用的在线编辑器。