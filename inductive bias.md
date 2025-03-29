---
title: inductive bias
tags:
- Algorithm
alias:
- 归纳偏置
public: true
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

先验知识以及假设

  + 算法对学习问题做的假设

归纳偏置

  + 归纳和演绎 induction deduction

  + 从一些例子中寻找共性、泛化，形成一个比较通过的规则的过程

  + 偏置代表对模型的偏好

  + 用规则约束模型，从而起到模型选择

    + 将无限可能的目标函数约束在一个有限的类别假设中

    + 近似损失 + 估计损失(更宽松的假设会增大这个损失)

常见的例子

  + [[奥卡姆剃刀]] :-> 希望学习到的模型复杂度更低
  + [[KNN]] :-> 特征空间中相邻的样本倾向于属于同一类
  + {{c2 SVM 好的分类器}} 应该 {{c1 最大化类别边界距离}}
  + [[RNN]] :-> 每一个时刻的计算依赖历史计算结果
    + sequentiality

    + time invariance

      + 序列顺序上的 timesteps 有联系

    + 时间变换不变性

      + 权重共享

  + 双向 RNN

    + RNN 假设当前输入和之前的输入有关系，双 RNN 假设当前输入和之前、之后的输入都有关系

  + [[DNN]] :-> 信息应该逐级加工，层层抽象
  + [[CNN]] :-> 信息具有空间局部性，滑动卷积共享权重方式降低参数空间
    + locality

    + spatial invariance

      + 空间相近的 grid elements 有联系而远的没有

    + 空间变换不变性 translation invariant

      + kernel 权重共享

  + [[GNN]] 连接不变性

  + [[Attention]]

  + [[Word2Vec]] :-> A word’s meaning is given by the words that frequently appear close-by.
    + 结构相似性

    + 例子：猫和狗在语料中没有同时出现，但是他们的上下文完全一致，所以最终 embedding 相似。

      + 我有一只猫。

      + 我有一只狗。
