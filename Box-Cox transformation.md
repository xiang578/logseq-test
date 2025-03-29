---
public: true
tags:
- Mathematics
title: Box-Cox transformation
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

标准变换

  + $y(\lambda)=\left\{\begin{array}{l}\frac{y_i^\lambda-1}{\lambda}, \text { 如果 } \lambda \neq 0 ; \\ \ln \left(y_i\right), \text { 如果 } \lambda=0 .\end{array}\right.$

选择 $\lambda$ 使得变换后的样本正态性最好

  + 

常用 $\lambda$ 值，$y(\lambda)= y_i^{\lambda}$

  + $\lambda = 2, y(\lambda)= y_i^2$

  + $\lambda = 0.5, y(\lambda)= \sqrt {y_i}$

  + $\lambda = -0.5, y(\lambda)= \frac{1}{\sqrt {y_i}}$

  + $\lambda = -1, y(\lambda)= \frac{1}{y_i}$



## Ref

  + [Box-Cox 变换 的方法和公式 - Minitab](https://support.minitab.com/zh-cn/minitab/21/help-and-how-to/quality-and-process-improvement/control-charts/how-to/box-cox-transformation/methods-and-formulas/methods-and-formulas/)
