---
public: true
tags:
  - Mathematics
alias:
  - logarithmic normal distribution
  - 对数正态分布
title: Log-Normal Distribution
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

一个随机变量的对数服从 [[正态分布]]，则该随机变量服从对数正态分布。

  + 对于一条路线的 ETA 来说，有一个无人可及的最小时间，然后是少数一些非常快的司机，接下来是普通司机最具代表性的完成时间形成一个高峰，最后是尾部一长串的“掉队者”。

$\ln (Y) \sim N\left(\mu, \sigma^2\right)$

[[概率密度函数]]

  + $f_{\lg -N}(x ; \mu, \sigma)=\frac{1}{x \sigma \sqrt{2 \pi}} e^{-\frac{(\ln x-\mu)^2}{2 \sigma^2}}$

期望

  + $E(x)=e^{\mu+\frac{\sigma^2}{2}}$

方差

  + $D(X)=\left(e^{\sigma^2}-1\right) e^{2 \mu+\sigma^2}$
