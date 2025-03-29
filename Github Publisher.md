---
public: true
title: Github Publisher
date:
- 2024/04/04
tags:
- Obsidian
categories: 随手记
toc: "true"
permalink: note/github-publisher.html
lastMod: 2025-03-29
toc: "true"
---
原来一直用 Logseq 写笔记，等了好久也没有等到一个可以把笔记导出成 md 文章的插件。昨天晚上看其他人博客的时，发现 Obsidian 插件 [Gihub Publisher](https://github.com/ObsidianPublisher/obsidian-github-publisher)，可以通过内建的命令把笔记上传到指定的 github 仓库，从而实现使用 Obsidian 管理 blog 文章。

<!-- more -->
`Share key` 把 share 改成 public，实现和 logseq 兼容
`Contents - Internals links` 将 wiki link 转换成内部链接，但是 hexo 好像不支持解析内部链接。
一些问题：
笔记改名后 publish，会新增加一篇文章，但是不会删除旧的笔记。
## Ref
[ObsidianPublisher/obsidian-github-publisher: Github Publisher helps you to publish your notes on a preconfigured GitHub repository from your Obsidian Vault, for free, and more!]()
[最近折腾Obsidian及hexo - 天一生水 (jiangyu.org)](https://www.jiangyu.org/obsidian-plugin-and-hexo/)
用 dataview 生成读书页面