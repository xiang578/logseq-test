---
alias:
- 分位数回归
public: true
title: quantile regression
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

自变量与因变量的特定百分位数之间的关系建模

数据从小到大排列，q 分位数为 m 则表示该组数据中 100q% 的数据小于 m。满足q%的样本在曲线下方

特点

  + 分位数回归不会假设目标变量的分布

  + 分位数回归趋向于抑制偏离观测值的影响

MAE 是一种中位数的分位数回归



公式定义 #card
  + 条件概率 $F(y \mid X=x)=P(Y \leq y \mid X=x)=E\left(1_{\{Y \leq y\}} \mid X=x\right)$

  + $Q_\alpha=\inf \{y: F(y \mid X=x) \geq \alpha\}$

分位数回归用途： #card
  + 区间预测（interval prediction）,

  + 异常值检测（outlier detection）

单点损失函数--weighted absolute deviations #card
  + $L_\alpha(y, q)= \begin{cases}\alpha|y-q| & \text { if } y>q \\ (1-\alpha)|y-q| & \text { if } y \leq q\end{cases}$

  + 整体优化目标

    + $Q_\alpha(x)=\arg \min _q E\left\{L_\alpha(Y, q) \mid X=x\right\}$.

分位数回归可以通过随机森林实现 #card
  + 训练中单颗树每个落入叶子结点的样本权重占比

    + $w_i(x, \theta)=\frac{1_{\left\{X_i \in R_{\ell(x, \theta)}\right\}}}{\#\left\{j: X_j \in R_{\ell(x, \theta)}\right\}}$.

  + 随机森林每个落入叶子结点样本权重占比

    + $w_i(x)=k^{-1} \sum_{t=1}^k w_i\left(x, \theta_t\right)$

  + 随机森林的预测结果

    + $\hat{\mu}(x)=\sum_{i=1}^n w_i(x) Y_i$.

随机森林本质上在approximate the conditional mean $E(Y \mid X=x)$ ，因此考虑用 #card
  + $$
\hat{F}(y \mid X=x)=\sum_{i=1}^n w_i(x) 1_{\left\{Y_i \leq y\right\}},
$$

总结通过随机森林得到分位数回归的过程 #card
![image.png](/assets/image_1742050245176_0.png)


