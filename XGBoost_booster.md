---
title: XGBoost/booster
public: true
deck: Machine Learning/XGBoost
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---



[[DART]]

  + 带 dropout 的树学习器

gblinear

  + 线性模型,迭代器增加再多对模型的收敛能力提升也不大

  + 数据高维稀疏的场景可以尝试使用

  + 利用 gbm 框架求解 linear，利用梯度提升方法代替梯度下降方法
