---
alias:
  - Dropouts meet Multiple Additive Regression Trees
tags:
  - Paper
  - LightGBM
public: true
deck: being/ML/DART
title: DART
date: 2024-10-05
updated: 2024-12-08
toc: true
mathjax: true
---

主要思想 :-> 每次新加的树要拟合并不是之前全部树 ensemble 后的负梯度，而是随机抽取一些树 ensmeble 后的负梯度。
  + 解决 {{c1 GBDT over-specialization}} 问题
    + 问题现象 :-> 前面迭代树对预测值的贡献比较大，后面的树会集中预测一小部分样本的偏差
    + 常规方法 :-> Shrinkage
算法流程图 
![image.png](/assets/image_1733636028835_0.png)

  + S1 :-> 训练数据集
  + T1 :-> 使用 S1 数据训练得到决策树
  + 针对决策树 2 到 N #card #incremental
    + 从 M 中随机抽取决策树集合 D，$\hat{M}$ 是 M 和 D 的差集

    + 利用 $\hat{M}$ 计算样本负梯度，得到数据集 St

    + 利用 St 训练 Tt

    + 调整 Tt 的权重

      + 负梯度只有 $\hat{M}$ 树得到，实际上这个少的负梯度由 Tt 和 D 中的树共同拟合，所以需要对 T_t 缩小 D+1 倍

    + 调整 D 中其他树的权重

[[lightgbm 使用记录]] Early stopping is not available in dart mode
