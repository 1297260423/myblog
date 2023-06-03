---
title: "hugo安装"
date: 2023-02-12T13:09:47+08:00
tags: []
categories: [""]
toc:
  enable: true
description: 
draft: true

---

<!--more-->

# hugo

> hugo 是一个快速建站工具，尤其方便制作个人博客

## 1.安装

```bash
go install github.com/gohugoio/hugo@latest
```

[Releases · gohugoio/hugo (github.com)](https://github.com/gohugoio/hugo/releases)

[hugo_extended_0.110.0_windows-amd64.zip](https://github.com/gohugoio/hugo/releases/download/v0.110.0/hugo_extended_0.110.0_windows-amd64.zip)

> 前提：已经有golang环境

```
#查看版本，确定是否安装完成
hugo version
```

# 2.新建hugo站点

> hugo new site {名称}

```
hugo new site myblog
```

## 3.添加LoveIt主题

> 初始化你的项目目录为 git 仓库, 并且把主题仓库作为你的网站目录的子模块
> https://hugoloveit.com/zh-cn

```
git init
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

可能出现的错误[warning: in the working copy of '.gitmodules', LF will be replaced by CRLF the next time Git touches it](https://blog.csdn.net/Babylonxun/article/details/126598477)

> 更新主题

```
git submodule update --rebase --remote
```

## 4.运行

```
hugo serve -D -e production --bind="0.0.0.0" --port="1313"
```

