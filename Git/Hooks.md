---
title: Git/Hooks
public: true
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

Hooks 可以实现在 git 命令后，触发额外的脚本。初始化 git 项目时，会在 `.git/Hooks`  目录中生成一些 sample 文件。
举个例子，这个站点的 md 源文件放在 `writing/notes` 目录中，站点对应的项目是 [xiang578/gru](https://github.com/xiang578/gru)。每一次更新笔记后，需要手动将文件从 `writing/notes` 复制到 `gru/docs`，然后再 push 到 github 中部署。
新建脚本  `gru/.git/post-commit`，`post-commit` 代表这个脚本会在 commit 时触发，脚本代码如下：
```shell
#!/bin/sh
#
# An example hook script to prepare a packed repository for use over
# dumb transports.

tmp=../gru/
cd $tmp
cp -rf ../writing/notes/* docs/.
```
## Ref
[Git - Book](https://git-scm.com/book/zh/v2)
