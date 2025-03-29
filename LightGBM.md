---
title: LightGBM
type: Paper
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

创新点

  + GOSS :-> [[Gradient-based One-Side Sampling]] 单边梯度抽样算法
  + 分裂方法 :-> [[Histogram-based Algorithm]]
  + EFB :-> [[Exclusive Feature Bundling]]
带深度限制的 [[Leaf-wise 叶子生长策略]]

  + level-wise 生长策略不加区分对待同一层的叶子，很多叶子分裂增益较低，没有必要进行搜索和分裂。容易进行多线程优化。

  + [[Level-wise 叶子生长策略]]不加区分对待同一层的叶子，很多叶子分裂增益较低，没有必要进行搜索和分裂。容易进行多线程优化。

  + 每次从当前所有叶子中，找到分裂增益最大的一个叶子，然后分裂，如此循环

    + 分裂次数相同的情况下，leaf-wise 可以降低更多误差，得到更好的精度。

    + 通过树最大生长深度，避免过度拟合

类别特征最优分割
  + 时间复杂度 :-> $O(k\log(k))$
  + 每一次切分尽可能分成两个数量接近的集合
![](https://media.xiang578.com/lgb-many-vs-many.png)

  + 具体实现

    + [[目标编码]] 枚举分割点前，直方图按每个类别的label均值进行排序，然后按均值的结果依次枚举最优分割点
      + 需要大量的约束和正则化解决过拟合问题

![](https://media.xiang578.com/objective-encoding.png)

并行

  + 特征并行 :-> 每台机器保存所有训练数据，找到最佳划分方案后，本地执行重分区。避免[[XGBoost]]中不同机器同步划分方案。
  + 数据并行 :-> Reduce scatter 把直方图合并的任务分摊到不同机器，利用 直方图做差加速

  + 投票并行

    + Parallel Voting Decision Tree, PV-tree

缓存优化

  + xgb pre-sorted算法导致 Cache-miss 问题

[[Ref]]

  + [[LightGBM Bin]]

  + [深入理解LightGBM - 知乎](https://zhuanlan.zhihu.com/p/99069186)

  + 工程优化方案论文 A communication-efficient parallel algorithm for decision tree
