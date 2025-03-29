---
alias:
- 1D 卷积
public: true
title: 1D Conv
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

1D 卷积其实是特殊的 2D 卷积，卷积核宽度直接和 embedding 维度强制对应。只能在时间顺序上纵向滑动，不能横向滑动。

控制前后卷积的通道数，用于 skip connect 需要 add 操作的场景

应用非线性

  + 神经网络每一层后，都可以应用激活层。

  + 非线性扩展模型的可能性，通常使深度网络比宽网络更好

  + 为了增加非线性层数量而不显著增加参数和计算量，可以用 1D 卷积然后再接激活层。



## Ref

  + [卷积和深度可分离卷积的区别 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/643204108)

  + [A Basic Introduction to Separable Convolutions | by Chi-Feng Wang | Towards Data Science](https://towardsdatascience.com/a-basic-introduction-to-separable-convolutions-b99ec3102728)
