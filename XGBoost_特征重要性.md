---
title: XGBoost/特征重要性
deck: being/Algorithm/XGBoost
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

XGBoost 中有什么方法可以评估特征重要性？ #card
  + 通过整体分布产生随机特征，通过随机特征在特征重要性中的位置，筛除重要性不是非常明显的特征。

  + [[SHAP]]

特征重要性指标 `get_score` 方法
  + weight :-> 特征在树中作为划分属性的次数
  + gain :-> 特征作为划分属性时， loss 平均的降低量
  + cover :-> 特征作为划分属性时，对样本的覆盖度
    + 覆盖度指特征用作分割点后影响的 :-> 样本数量，即多少样本经过特征分割到两个子节点



