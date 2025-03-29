---
alias:
- 贝叶斯定理
tags:
- Mathematics
public: true
title: Bayes theorem
date: 2024-10-05
updated: 2025-02-10
toc: true
mathjax: true
---

[[Bayesian]]概率：概率很难求，求反概率就很容易。

$P(\theta|X) = \frac{P(X|\theta)P(\theta)}{P(X)}$
  + $posterior = \frac{likehood * prior}{evidence}$

  + posterior 后验概率 $P(\theta|X)$ :<-> 通过样本 X 得到 theta 的概率
  + likehood 似然函数 $P(X|\theta)$ :<-> 通过参数 theta 得到样本 X 的概率
  + prior [[先验概率]] $P(\theta)$ :<-> 在试验尚未发生前，对参数 $\theta$ 的估计
    + 客观先验概率 :<-> 利用过去历史资料计算出来得到的先验概率
    + 主观先验概率 :<-> 凭主观经验来判断而得到的先验概率
  + evidence :<-> 样本 x 发生的概率
[[极大似然估计]]

  + 核心思想：当前发生的事件是概率最大的事件，给定数据集，使得该数据集发生的概率最大求模型中的参数。

    + 最大化似然函数 $p(X \mid \theta)=\prod_{x_1}^{x_n} p(x_i \mid \theta)$

    + 对似然函数取对数变成对数似然函数方便计算

  + 计算似然估计只关注当前的样本(当前已经发生的事情，不考虑事情的先验情况)

[[最大后验估计]]

贝叶斯估计

  + 

## See

  + [[L1和L2正则的先验分布]]

## Ref

  + [详解最大似然估计（MLE）、最大后验概率估计（MAP），以及贝叶斯公式的理解_网络_nebulaf91的博客-CSDN博客](https://blog.csdn.net/u011508640/article/details/72815981)

  + [极大似然估计、最大后验估计 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/93416473)

  + [聊一聊机器学习的MLE和MAP：最大似然估计和最大后验估计 - 知乎](https://zhuanlan.zhihu.com/p/32480810)
