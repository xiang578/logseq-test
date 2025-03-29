---
title: Initialization
alias:
  - 参数初始化
tags:
  - Algorithm
public: true
deck: being/deep_learning/Initialization
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

影响模型的收敛速度和模型质量。

[[Batch Normalization]] 可以有效降低深度网络对 weight 初始化的依赖。非线性计算之前，输出值有较好的分布。BN 强行将输出值做一次高斯变换和线性变换。

常量初始化

高斯分布初始化

  + tf.truncated_normal 按两倍标准差截断

  + tf.random_normal

[[正交初始化]]

不同方法的均值和方差

  + [[He Initialization]] :<-> 0 均值，标准差为 sqrt(2 / fan_in)
  + [[Xavier Initialization]] :<->  0 均值，标准差为 sqrt(2 / (fan_in + fan_out))
card-last-score:: 5
card-repeats:: 1
card-next-schedule:: 2023-07-23T14:52:57.521Z
card-last-interval:: 4
## See Also

  + [[神经网络参数全部初始化为0]] 不可行

## Ref

  + [聊一聊深度学习的weight initialization - 知乎](https://zhuanlan.zhihu.com/p/25110150)

  + 
