---
title: Normalization
alias:
- 归一化
- 规范化
tags:
- Algorithm
public: true
deck: being
date: 2024-10-05
lastMod: 2024-11-28
toc: "true"
---

解决 [[Internal Covariance Shift]]
本质是平滑 Loss，保持在梯度下降过程中的稳定。
连续特征的值分布不统一，会导致训练波动，影响收敛速度。
归一化：对不同特征维度的伸缩变换的目的是使各个特征维度对目标函数的影响权重是一致的，即使得那些扁平分布的数据伸缩变换成类圆形。
归一化 min-max 线性函数归一化：数值缩放到 01，不改变分布。 $$x'=\frac{x-min(x)}{max(x)-min(x)}$$
1. Rescalingy) (min-culax mormalization) 有时简称 normafization(有点坑)
$$
x^{\prime}=\frac{x-\min (x)}{\max (x)-\min (x)}
$$
2. Mean normalization $x^{\prime}=\frac{x-\operatorname{mean}(x)}{\max (x)-\min (x)}$
3. Standardization(Z-score normalization) $x^{\prime}=\frac{x-\operatorname{mean}(x)}{\sigma}$
4. Scaling to unit length $x^{\prime}=\frac{x}{\|x\|}$

减少人为参数选择
缓解过拟合
减少梯度消失，加快收敛速度，提高训练精度
通过计算均值和方差的集合分成，输入 `[N, C, H, W]` 维度图片
不同方法的区别在于神经元集合 S 的范围如何确定
![image.png](/assets/image_1728018649220_0.png)
[[Group Normalization]]
[[Batch Normalization]] 神经网络中间层进行归一化
C 维度上，计算 `(N, H, W)` 的统计量
[[Layer Normalization]] RNN 等序列模型
[[Instance Normalization]]
与 `LN` 相同对单个样本操作
`IN` 对同一层神经元中的同一个通道进行归一化
[[Weight Normalization]]
## Ref
[详解深度学习中的Normalization，BN/LN/WN - 知乎](https://zhuanlan.zhihu.com/p/33173246)