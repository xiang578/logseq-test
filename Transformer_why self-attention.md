---
public: true
title: Transformer/why self-attention
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

通过计算复杂度、并行操作数、最长学习距离三个方面来对比 Transformer、CNN、RNN。

![](https://media.xiang578.com//why-self-attention.png)

计算复杂度就是模型中浮点计算次数

CNN 中的最长学习距离是通过[[空洞卷积]]实现

1. 训练效率低下，self-attention 可以并行计算。

2. 长距依赖问题，self-attention 可以忽视不同 token 之间的距离。
