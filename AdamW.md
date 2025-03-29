---
tags:
- Optimization
public: true
title: AdamW
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[[L2 Regularization]] 和 [[Weight Decay]] 在 Adam 这种自适应学习率算法中并不等价
使用 Adam 优化带 L2 正则损失并不有效
正常权重衰减是对所有权重都采用相同的系数进行更新，本身比较大的权重对应的梯度也会比较大，惩罚也越大。
Adam 计算步骤中减去项会除以梯度平方的累积，使梯度大的减去项偏小，从而大梯度的权重不会像解耦权重衰减那样得到正则化。
![](https://media.xiang578.com//adam-adamw.png)
红色部分 Adam + L2 regularization，line 12 中 L2 部分会被二阶梯度调整，梯度变化快的方向上，调整之后的值比较小，这个方向上正则化更少。
$\theta_t \rightarrow \theta_{t-1}-a \frac{\beta_1 m_{t-1}+\left(1-\beta_1\right)\left(\nabla f_t+\lambda \theta_{t-1}\right)}{\sqrt{\hat{V}_t}+\epsilon}$
分子右上角的 $\lambda \theta_{t-1}$ 向量各个元素被分母 $\sqrt{\hat{V}_t}$ 项调整。
梯度变化快的方向上，$\sqrt{\hat{V}_t}$ 有更大的值，从而使调整后的 $\frac{\lambda \theta_{t-1}}{\sqrt{\hat{V}_t}}$ 更小
作者提出以绿色的方式来在 Adam 中正确引入 weight decay ，使用相同的参数来正则化所有的权重，完成梯度下降与 WD 的解耦。
AdamWeightDecayOptimizer 通过 [[Weight Decay]] 参数控制
[[BERT]] 中使用 AdamW
[都9102年了，别再用Adam + L2 regularization了 - 知乎](https://zhuanlan.zhihu.com/p/63982470)
实现 [L2正则=Weight Decay？并不是这样 - 知乎](https://zhuanlan.zhihu.com/p/40814046)