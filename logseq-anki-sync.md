---
public: true
tags:
  - Logseq plugin
title: logseq-anki-sync
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

挖空卡片

  + 使用 `{{` 和 `}}` 包围需要挖空的内容

  + `{{`  之前需要有一个空格，适合英文，中文看起来比较奇怪。

带公式或代码的填空

```
replacecloze:: " '\sqrt{ a^{2}+b^{2} }' "
The Pythagorean theorem is
$$c=\sqrt{ a^{2}+b^{2} }$$
```

[Making multiline cards · debanjandhar12/logseq-anki-sync · Discussion #88](https://github.com/debanjandhar12/logseq-anki-sync/discussions/88)

  + 多行卡片，父节点打上 `card` 标签

![image.png](/assets/image_1730610859166_0.png)

  + 

  + 多行增量卡片，父节点打上 `incremental` 和 `card`  标签，实现复习时遮盖一行展示其他行。

![image.png](/assets/image_1730611077727_0.png)

  + 指定卡片方向卡片，分别用  `#forward`（默认卡片方向）, `#reversed`, `#bidirectional` 标签；或者使用 direction property `direction:: ->`, `direction:: <-`, `direction:: <->`

![image.png](/assets/image_1730611144816_0.png)

  + `#depth-n` 指定展示 child 节点的数量，`#depth-1` 只展示一级子节点

  + 不同步卡片 `#no-anki-sync`

  + 批量转成卡片 You can use the `#card-group` tag to turn all the children of it's block to cards

指定卡组

  + 支持全局和单独 block

  + `deck: : Tutorial`

Swift Arrow cards

  + 语法 `: - >` or `: < -` or `: < - >`
  + 类似于 [[Remnote]] 中的卡片功能


