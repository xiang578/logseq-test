---
title: DCN
tags:
  - Algorithm
  - Paper
public: true
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

在 Wide & Deep 基础上，对 Wide 部分进行改进。LR 无法进行特征交叉，FM 受限于性能一般只去做二阶交叉，Cross 可以实现高阶交叉。DCN 和 DNN 相比，相同效果情况下可以减少参数量。

Cross 网络只能处理定长的输入，[[ETA]] v4 中无法使用……

特征处理和常规的模型一样，Sparse feature 经过 embedding 处理，然后和 Dense feature concat 在一起。由于 Cross network 每一层的大小都和输入向量大小相等，如果 Sparse feature 不处理，输入维度会很大，然后参数量会增加。

Cross 和 Deep 的输出结果 concat 后过一个 LR 直接输出。

![](https://media.xiang578.com/15715510222588.jpg)

Cross Network

  + 每一层都是由 $x_0$ 和前一层的输出 $x_l$ 交叉学习残叉。

  + ResNet 的引入可以将网络做的更深。

  + 特点：有限高阶、自动叉乘、参数共享

  + $$\mathbf{x}_{l+1}=\mathbf{x}_{0} \mathbf{x}_{l}^{T} \mathbf{w}_{l}+\mathbf{b}_{l}+\mathbf{x}_{l}=f\left(\mathbf{x}_{l}, \mathbf{w}_{l}, \mathbf{b}_{l}\right)+\mathbf{x}_{l}$$

  + 图中可以看到随着层数的增加，参数 w 会线性增加。

![](https://media.xiang578.com/15715516832402.jpg)

Deep NetWork

  + Cross Network 中的参数量太少，不能学习高维的非线性特征。

Analysis

  + Cross 的设计最后包含了每个特征的从 1 阶到高阶的特征组合。与 FM 不同每个特征组合的参数部分共享，所以能降低参数量，比 FM 有更好的泛化性和鲁棒性。比如 FM 可以解决 xi 和 xj 没有同时出现过的情况，但是 Cross 能处理 xi 和 xj 都没有出现过的情况 ……

![](https://media.xiang578.com/15715525186005.jpg)
