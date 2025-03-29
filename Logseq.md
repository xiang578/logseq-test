---
tags:
  - Logseq
  - Workflow
public: true
categories: 随手记
toc: true
date:
  - 2024/06/16
permalink: note/logseq
title: Logseq
updated: 2024-10-05
mathjax: true
---

从 2019 年开始使用 [[Roam]]，2022 年底迁移到 Logseq，自己可以算得上一名资深双链笔记软件爱好者。得益于这几年日常高强度使用，已经积累超过 7k+ 笔记。本文记录我的 Logseq 最佳实践。

<!--more-->

## 基础功能

  + [[logseq/task]] 任务管理相关内容整理

  + [[logseq/query]] 查询功能，期待官方数据库版本能提升查询体验。

## 同步

  + 官方提供 [[Logseq Sync]] (需要赞助 5 刀成为 backer 用户)，自己从这个功能上线开始使用，快要一年时间内，也没有遇到过什么大的问题，还是比较省心的。

  + 由于之前还使用 [[logseq-publish]] 将笔记[发布出来](https://notes.xiang578.com/#/page/%E7%AE%97%E6%B3%95%E8%8A%B1%E5%9B%AD)，所以家中主力 mac 上的 logseq 数据目录也会使用 git 管理。

## 笔记在线发布

  + 最早使用 pengx17 的 Github Action 插件 [[logseq-publish]]，将 `public:: true` 的笔记打包成一个 PWA，然后利用 Gihub 托管。

  + 但是打包出来的 PWA 其实功能很弱，比如不支持访问量统计，评论。所幸自己写了一个 python 脚本，通过 [[Logseq API]] 将笔记转成 md 文件，然后通过 hexo 渲染成静态网页。比如你现在看到的这篇文章就是通过这种方式导出的，具体见 [[logseq 笔记发布到 hexo 博客]]。

## 插件

  + 插件是提升用户体验必不可少的一环，但是和 Obsidian 相比，Loseq 的插件生态要弱上不少。[[Logseq plugin]]
