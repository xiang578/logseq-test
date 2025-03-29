---
alias:
  - 学习率衰减
public: true
title: Learning Rate Decay
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

训练集的损失下降到一定程度后不在下降，training loss 一直在一个范围内震荡，遇到这种情况可以适当降低学习率。

常用方法

  + 线性衰减，每过 5 个 epochs 学习率减半

  + [[指数衰减]]

    + `decayed_learning_rate=learning_rate*decay_rate^(global_step/decay_steps)`

[[Adam]] 自适应的优化方法还需要学习率衰减吗？

  + [neural network - Should we do learning rate decay for adam optimizer - Stack Overflow](https://stackoverflow.com/questions/39517431/should-we-do-learning-rate-decay-for-adam-optimizer)

  + [自适应优化器Adam还需加learning-rate decay吗？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/423375831)

    + [[AdamW]] 中提到加 Learning Rate Decay 的 Adam 还是有效提升模型表现。
