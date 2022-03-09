---
layout: post
title: 建立 Github 博客站点
date: '2022-02-25 17:25:16 +0800'
categories: 工
published: true
---

# 参考来源

[Github Pages 创建 Jekyll 站点手册](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

[Jekyll 安装](https://jekyllrb.com/docs/installation/)

# Jekyll

[Jekyll](https://jekyllrb.com/) 是一个 Ruby 编写的轻量建站工具，它使用文件系统保存所有内容，避免了使用数据库，所以提供的是纯静态数据展示，优点是简单。

Jekyll 基本是开箱即用的，默认的 `minima` 主题已经很好，但是大部分时候仍然需要自定义，例如添加 $\LaTeX$ 支持。首先需要拷贝当前主题的 layout 和 include 文件到本地，如果已经安装了主题，可以使用 `bundle info --path` 命令获取主题所在目录，例如 `bundle info --path minima`。应该尽可能少的拷贝主题文件，以便后续升级或修改主题。

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

Jekyll 支持大部分 markdown 语法，可以使用本地 markdown 编辑器来编辑博客。也可以使用在线编辑器，[这里](https://github.com/planetjekyll/awesome-jekyll-editors) 有一个 Jekyll 编辑器列表。实践来看，仍然推荐本地编辑，通过执行以下命令来本地预览。

```
bundle exec jekyll serve
```

