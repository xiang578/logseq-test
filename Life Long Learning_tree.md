---
title: Life Long Learning/tree
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---



[[XGBoost]] 支持两种方式

  + 把原来的模型作为新的训练的初始模型

    + 无法解决在新数据上训练后对老数据的遗忘问题

    + `tests/python/test_training_continuation.py`

  + `process_type: update`

    + refresh

    + prune

  + 当前迭代树的基础上增加新树，原树不变

  + 当前迭代树结构不变，重新计算叶节点权重，同时也可增加新树

[[LightGBM]]

  + train 中设置参数 `keep_training_booster=rue`，`init_model` 为上一轮的结果

Ref

  + [xgboost等GBDT能否实现增量学习？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/89285046)
