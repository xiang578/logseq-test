---
tags:
- Algorithm
- Position Representation
public: true
alias:
- Position Encoding
title: Positional Encoding
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

为什么使用

[如何理解Transformer论文中的positional encoding，和三角函数有什么关系？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/347678607)

  + 如何构建一种位置编码？

    + 直接使用下标计数 PE= pos

      + 序列没有上限，后面的词可能位置编码非常大。

    + 使用文本长度对每个位置归一化 PE = pos/(T-1)

      + 不同长度文本的位置编码步长是不同的，长文本和短文本中两个相邻词的位置编码存在差异

    + 有界周期函数

  + 本质对位置信息进行建模，需要满足

    + 需要体现同一个单词在不同位置的区别

    + 相对次序关系，体现先后次序关系，编码差异不应该依赖于文本长度

    + 值域落在一定数值区间内

## Ref

  + [Transformer升级之路：1、Sinusoidal位置编码追根溯源 - 科学空间|Scientific Spaces](https://spaces.ac.cn/archives/8231)
