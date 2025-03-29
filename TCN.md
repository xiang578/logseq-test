---
title: TCN
public: true
alias:
- An Empirical Evaluation of Generic Convolutional and Recurrent Networks for Sequence Modeling
tags:
- Algorithm
- Paper
- Google
- CNN
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

![](https://media.xiang578.com/tcn.png)

  + TCN 中输入和输出可能有不同的宽度，c 图表示使用 11 卷积调整输入大小

    + 也可以直接通过 zero padding 来增加 channels

TCN = 1D FCN + causal convolutions

特点

  + 使用因果卷积，不会泄漏未来信息。

    + 论文中强调和 RNN 之类方法进行对比，所以要考虑因果。

  + 可以取任意长度的序列，并将其映射到相同长度的输出序列。

  + 引入 [[ResNet]] 和扩张卷积的组合可以将网络做深以及增加感受野。

细节

  + tcn 中没有 pooling 层

  + normalization 方法是 weight norm，更适合序列问题

增加感受野的方法

  + 更大的 kernel_size (增加参数，卷积核大效果差，卷积核过大会退化成一个全连接层)

  + [[空洞卷积]]

时序问题

  + 1. 输入和输出矩阵大小相同

  + 2. 不能使用没有发生时刻的信息，因果卷积

[[ETA 模型]] 实现

  + `tf.nn.conv1d(input, filters, stride, padding, data_format='NWC', dilations=None, name=None)`

