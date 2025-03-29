---
public: true
tags:
  - Optimization
title: LazyAdam
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

NLP 之类的任务，每个 batch 采样到的词有限，每次更新对 embedding 的梯度估计是稀疏的，对 momentum-based 的 Optimizer，现在所有框架实现都会用当前的 momentum 去更新所有的词，即时这些词在连续的几十步更新都没有被采样到，这可能会使 embedding 过拟合。

LazyAdam 仅更新当前 batch 中出现的稀疏变量索引的移动平均累加器，而不是更新所有索引的累加器。



## Ref

  + [优化方法总结以及Adam存在的问题(SGD, Momentum, AdaDelta, Adam, AdamW，LazyAdam)_sgd收敛比adam慢_糖葫芦君的博客-CSDN博客](https://blog.csdn.net/yinyu19950811/article/details/90476956)
