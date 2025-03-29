---
title: GBDT
type: Algorithm
public: true
alias:
- Gradient Boosting Decision Tree
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

GBDT 核心思想

  + 累加全部决策树的结果作为最终结果

Gradient Boosting Machine 基于梯度提升算法的学习器

从 [[Gradient Descend]] 到 Gradient Boosting

  + Gradient Descend

    + 迭代公式：$${\theta ^t = \theta ^{t-1} + \theta _{t}}$$

    + 负梯度方向更新参数：$${\theta _t = - \alpha _t g_t}$$

    + 最终参数等于每次迭代的增量的累加和：$${\theta = \sum_{t=0}^T \theta _t}$$

  + Gradient Boosting

    + 迭代公式：$${f^t(x) =f^{t-1}(x) + f_t(x)}$$

    + 拟合负梯度：$${f_t(x)= - \alpha _t g_t(x)}$$

    + 最终函数等于每次迭代的增量的累加和：$${F(x) = \sum_{t=0}^T f_t(x)}$$

加法模型

  + $${F(x;w)=\sum^{M}_{m=1} \alpha_m h_m(x;w_m) = \sum^{M}_{m=1}f_t(x;w_t)}$$

  + 其中，x 为输入样本，h 为分类回归树，w 是分类回归树的参数，${\alpha}$ 是每棵树的权重。

  + GBDT 算法可以看成是由 k 棵树组成的加法模型

    + $\hat{y}_i=\sum_{k=1}^K f_k\left(x_i\right), f_k \in F$

流程
  + 通过最小化损失函数求解最优模型：${F^* = argmin_F \sum^N_{i=1}L(y_i, F(x_i))}$

  + 输入: ${(x_i,y_i),T,L}$

  + 1. 初始化：${f_0(x)}$

    + 1. 求解损失函数最小

    + 2. 随机初始化

    + 3. 训练样本的充分统计量

  + 2. 对于 ${t = 1 to T}$ ：

    + 2.1 计算负梯度（伪残差）： ${ \tilde{y_i} = -[\frac{\partial L(y_i, F(x_i))}{\partial F(x)}]_{F(x)=F_{m-1}(x)} ,i=1,2,...,N}$

      + 当损失函数为 MSE 时，负梯度 = 残差

      + [[基于 MSE 的 GBDT 推导]]

    + 2.2 根据 ${\tilde{y_i}}$ 学习第 m 棵树： ${w^*=argmin_{w} \sum_{i=1}^N(\tilde{y_i} - h_t(x_i;w))^2}$

      + 最小化问题中，如果有解析解，直接带入。否则，利用泰勒二阶展开，Newton Step 得到近似解。

    + 2.3 line searcher 找步长：${\rho^* = argmin_\rho \sum_{i=1}^{N}L(y_i, F_{t-1}(x_i)+\rho h_t(x_i;w^*))}$

    + 2.4 令 ${f_t=\rho^*h_t(x;w*)}$，更新模型：${F_t=F_{t-1}+f_t}$

  + 3. 输出 ${F_T}$

[[GBDT/Loss]]

[[GBDT/Question]]

## Ref

  + 

  + [[gbdt 时间序列]]
