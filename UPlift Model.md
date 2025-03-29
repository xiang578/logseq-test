---
public: true
alias:
  - 增益模型
title: UPlift Model
tags:
date: 2024-10-05
updated: 2025-03-16
toc: true
mathjax: true
---

根据 [[营销人群四象限]]，应该针对 TR 人群进行营销活动。

Uplift 干预和不干预的差值

  + 响应模型 Response Model，预测干预情况下用户是否购买

    + $\text { Outcome }=P(\text { buy } \mid \text { treatment })$

  + uplift 通过干预和不干预的反事实来预估计算因果效应

    + $\text { Lift }=P(\text { buy } \mid \text { treatment })-P(\text { buy } \mid \text { no treatment })$

    + $\tau=Y(1)-Y(0)$
  + 样本服从CIA ( [[Conditional Independence Assumption]] ) 条件独立假设

$\tau=Y(1)-Y(0)$ 通过随机对照实验收集数据：实验组全部干预，对照组都不干预。

  + 利用条件平均因果效应[[CATE]]来预估给定条件下用户群体的平均因果效应

    + $\begin{aligned} \tau & =E[Y(1)-Y(0) \mid X] \\ & =E[Y(1) \mid X]-E[Y(0) \mid X] \\ & =E[Y(1) \mid T=1, X]-E[Y(0) \mid T=0, X]\end{aligned}$

  + 利用一个人群的条件平均因果效应去近似个体因果效应

核心问题

  + 混杂因素偏置 Confounding Bias

    + 干预机制导致选择偏差

  + 归纳偏置

    + CATE 干预打分-非干预打分差值

模型方案

  + [[Meta-Learner]]

    + [[S-Learner]] one-model 的差分响应模型 #card
      + 把用户是否干预作为特征加入到模型构建中

      + 优点

        + 可以直接使用现有分类算法

        + 减少双模型误差累积

        + 训练样本增加，提高模型精度

      + 缺点

        + 间接计算增量，无法根据增量对模型进行优化

    + [[T-Learner]] two-model 差分响应模型#card
      + 实验组和对照组的数据分别训练一套模型

      + 差分值就是 uplift socre

      + 缺点

        + 两个模型训练 bias 不一致，容易有累积误差

    + [[X-Learner]] 基于 T-Learner的反事实推断模型#card
      + 方法

        + 无干预组模型

          + $\hat{\mu}_0=f\left(X_0, Y_0\right)$

        + 有干预组模型

          + $\hat{\mu}_1=f\left(X_1, Y_1\right)$

        + 通过与实际结果差分计算增量

          + 用有干预模型预测无干预群体的有干预结果，无干预组近似增量 $D_0=\hat{\mu}_1\left(X_0\right)-Y_0$

          + 用无干预模型预测有干预群体的无干预结果，有干预组近似增量 $D_1=Y_1-\hat{\mu}_0\left(X_1\right)$

        + 根据增量建立两个模型，对增量建模可以引入相关先验知识提升模型精度

          + $\hat{\tau}_0=f\left(X_0, D_0\right)$

          + $\hat{\tau}_1=f\left(X_1, D_1\right)$

        + 引入 [[倾向性评分匹配]]PSM 加权得到最后提升评估结果

          + $\begin{aligned} & e(x)=P(W=1 \mid X=x) \\ & \hat{\tau}(x)=e(x) \hat{\tau}_0(x)+(1-e(x)) \hat{\tau}_1(x)\end{aligned}$

      + 优点

        + 适合实验组和对照组样本数量差别较大场景

        + 增量的先验知识可以参与建模，引入权重系数，减少误差

      + 缺点

        + 多模型造成误差累加

    + [[R-Learner]] 通过 Robinson’s transfomation 定义一个损失函数，然后通过最小化损失函数的方法达到对增量进行建模的目的。#card
      + 倾向性得分模型 $e(x)=P(W=1 \mid X=x)$

      + 通过 CV 方式对 Laebl Y 建模

        + $m^*(x)=\mathbb{E}[Y \mid X=x]$

      + 优化下面损失函数

        + $\tau^*(\cdot)=\arg \min _\tau\left\{\frac{1}{n} \sum_1^n\left(\left(Y_i-m^*\left(X_i\right)\right)-\left(W_i-e^*\left(X_i\right)\right) \tau\left(X_i\right)\right)^2+\Lambda(\tau(\cdot))\right\}$

        + 用权重为 $\left(W_i-e^*\left(X_i\right)\right)^2$ 的样本 X 去拟合 $\tau\left(X_i\right)=\frac{Y_i-m^*\left(X_i\right)}{W_i-e^*\left(X_i\right)}$

![image.png](/assets/image_1701961535891_0.png)

  + CRFnet 和 EFIN （[[Explicit Feature Interaction uplift Network]]）

![image.png](/assets/image_1701961548866_0.png)

  + 

  + 多目标 uplift 模型

![image.png](/assets/image_1701961604646_0.png)

[[Uplift Model 评估]] 不可能同时观察到同一个用户在不同干预策略下的响应，即使无法获取用户真实增量，无法用常规分类和回归问题的评估指标。

  + 通过划分十分位数来对齐实验组和对照组数据去进行间接评估

  + [[Qini curve]]

  + [[AUUC]]


