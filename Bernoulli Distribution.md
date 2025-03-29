---
title: Bernoulli Distribution
tags:
  - Mathematics
alias:
  - 伯努利分布
  - 二元分布
  - 二值分布
  - binary distribution
public: true
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

$f(x)=p^x(1-p)^{1-x}$

$E(x)=xf(x)= 0 * (1-p) + p= p$
$D(x)=p(1-p)$
抛一次硬币

求解唯一的参数 $\mu$ 或 $p$

  + 根据似然函数

    + $p(\mathcal{D} \mid \mu)=\prod_{n=1}^N p\left(x_n \mid \mu\right)=\prod_{n=1}^N \mu^{x_n}(1-\mu)^{1-x_n}$

  + 求对数似然函数

    + $\ln p(\mathcal{D} \mid \mu)=\sum_{n=1}^N \ln p\left(x_n \mid \mu\right)=\sum_{n=1}^N\left\{x_n \ln \mu+\left(1-x_n\right) \ln (1-\mu)\right\}$

  + 对对数似然求导，令结果等于 0

    + $\mu_{\mathrm{ML}}=\frac{1}{N} \sum_{n=1}^N x_n$

样本的均值是伯努利分布的[[充分统计量]] sufﬁcient statistic
ls-type:: annotation
hl-page:: 89
hl-color:: yellow
（分布的参数 $\mu$ 可以由该统计量估计得到）




