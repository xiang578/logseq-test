---
public: true
title: Alfred
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

提高使用率的第一步，整理默认搜索支持常见的（谷歌、百度、知乎、微博、淘宝、b站）等等

多站点搜索，同时打开多个搜索页面

Force keyboard 强制默认输入法

Features

Default Results

  + Applications

    + 「Match Application’s keywords in default results」可以匹配应用的元数据。

    + Extras 添加额外搜索

Advanced-Syncing 终于发现如何在不太的 mac 之间同步配置，现在在大白中完成配置，让小灰同步即可。

其他

Snippets

Search 拓展

  + 搜索自己的推特 `https://twitter.com/search?q={query}%20(from%3Axiang578)&src=typed_query`

使用 iTerm 2 做为终端：https://gist.github.com/xiang578/c8b504bdf9a34cd14e3acd95695ad773

调出时所在屏幕，激活窗口：Appearance > Options

快捷键 ![](https://media.xiang578.com/15715605464295.jpg)

文件处理

  + ' 文件搜索~

  + ~ / 文件浏览器 ⌘+下键

  + 对文件点击向右方向键，查看对文件的操作

  + previous 上一次浏览的路径

  + shift 预览文件

  + open 打开项目，选中项目后按 ⇧Shift 键预览项目

除了空格键外，你还可以在前面加上 open 以打开文件，f 在 Finder 中查看，in 搜索文档内文字，tags 搜索指定标签文件。![](https://media.xiang578.com/15715606181389.jpg)

在回车打开文件前，不妨先按下 ⌥Option + ⌘Command + \，你会发现 Alfred 已经为你准备了解压、复制、分享、查重等数项常用操作![](https://media.xiang578.com/15715607337375.jpg)

Clipboard 粘贴板历史

Snippets 快捷短语

[一站式文件处理中心：Alfred 文件搜索 & 处理详解 - 少数派](https://sspai.com/post/56175)

![](https://media.xiang578.com/15715591872216.jpg)

⌘Command-C 复制路径

⌘Command-Y 预览

搜索结果可以直接拖拽到其他软件中，按⌘Command移动，按 ⌥Option 是复制

搜索后的文件可以通过右方向键打开 action 窗口。

Workflow

  + Debug 难免会遇到问题

    + 打开 Workflow 对应的 Debug 窗口之后，再运行指令，会将错误信息输出在窗口中。

  + [BlackwinMin/alfred-gallery: Original macOS Alfred actions by Minja.](https://github.com/BlackwinMin/alfred-gallery) 集合

    + 

  + [mpco/AlfredWorkflow-Recent-Documents: Quickly open recent documents and apps / 快捷打开最近访问的文档或应用](https://github.com/mpco/AlfredWorkflow-Recent-Documents)

    + `rr` 当前激活应用打开的文档

    + `rf` 最近访问文件夹

    + `rd` 全局最近文档

    + `ra` 最近程序

    + 环境变量 `ExcludedFolders` 忽视文件

    + 需要 `open macOS Full Disk Access preference` 权限，否则使用 ra 可能会有问题

  + [mpco/AlfredWorkflow-DEVONthink-Search: Powerful Tool for Searching in DEVONthink.](https://github.com/mpco/AlfredWorkflow-DEVONthink-Search)

## See Also

  + [[Alfred/Debug]]

  + Text Tools for Alfred http://matthewhealy.net/blog/category/text-tools-for-alfred

  + [Alfred Workflow 从使用到创造 - 少数派](https://sspai.com/post/57648)
