---
alias:
- Area Under the Uplift Curve
tags:
- Causal Inference
public: true
title: AUUC
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

[[UPlift Model]] 目标是学习个体潜在弹性 $\tau=Y(1)-Y(0)$
，没有标签。



计算过程

  + 数据集 $D=\left(Y_i^{\text {obs }}, W_i\right.$, score $\left._i\right)$

    + W 是样本所在的组，1 为实验组，0 为空白组

    + Y_obs 是观测到的样本响应信号

    + socre 是样本的 uplift 值

  + 按 socre 从大到小排序，第 k 个的 uplift 值

    + $u(k)=\frac{R^T(D, k)}{N^T(D, k)}-\frac{R^C(D, k)}{N^C(D, k)}$

      + $R^T(D, k)=\sum Y_i^{o b s} \mathbb{I}\left(W_i=1\right)$ 排在前 k 个样本中属于实验组的人的响应之和

      + $R^C(D, k)=\sum Y_i^{o b s} \mathbb{I}\left(W_i=0\right)$ 空白组的人的响应之和

      + $N^T(D, k)=\sum \mathbb{I}\left(W_i=1\right)$ 前 k 实验组人数

      + $N^C(D, k)=\sum \mathbb{I}\left(W_i=0\right)$ 前 k 空白组人数

      + 避免实验组和对照组用户数量差别较大导致指标不可靠

      + 全量人群的 [[Average Treatment Effect]]

    + 含义：前 k 个样本中实验组平均产生的价值 - 前 k 个样本中空白组平均产生的价值

  + 计算 $A U U C=\frac{S}{n * u(n)}$

    + $S=\sum_{k=1}^n(u(k) * k)$

      + $(u(k) * k)$ 代表前 k 个人产生的 uplift 值



## Ref

  + 实现 [[causalml]]

    + `lift.plot` x=k, y=u(k)

    + `gain.plot` x=k, y= k*u(k)

  + [弹性模型的评测指标AUUC - 知乎](https://zhuanlan.zhihu.com/p/457689388)

    + 画 [[auuc/code]]

    + `auuc_score['random']` 值含义是什么？

      + 无规律排序下，实验组相对于控制组的期望增值

      + TODO 在大多数情况下，使用归一化的auuc_score(normalize=True)函数计算得到的random值应该接近0.5，gain.plot()画出的random应该是一条直线。原因是在多次随机排序下，期望增值应该是稳步上升的。

      + 假如random值不是0.5，图像不是直线时，这意味着什么？

        + 导致不是0.5的背后原因可能有很多，可以先分析下是不是以下三种情况。

          + 1.实验组和空白组不是平衡的，两者人群不是同质的，这时算AUUC没有很大的意义了，应该调平人群后再计算。

          + 2.样本的y值即响应信号的离群点比较多。

          + 3.样本量太小，无法支撑实验组和对照组的匹配。

        + 除此之外，还有一种情况是random值为-0.5，这时整体的ATE为负数，所有样本均为负弹，这时候uplift值不再是“收益”，更像是“花销”。

  + [[@DiDi Food中的智能补贴实战漫谈]]

![image.png](/assets/image_1702136542300_0.png)
