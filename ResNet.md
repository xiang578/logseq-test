---
tags:
  - Algorithm
  - Paper
public: true
title: ResNet
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

单纯堆积卷积层，并不能让模型表现的更好。

vanishing/exploding gradients

离输入近的网络层会产生梯度消失现象，比较难训练，接到靠近输出的层。
使用 Residual Block

Deep Residual Learning for Image Recognition

  + 学习 residual mapping 比 original unreferenced mapping 轻松

  + identity mapping 给模型提供 shortcuts，如果 block 前后输入输出大小不同，可以通过 w 参数转化

  + 在加法之后过第二个非线性单元

![](https://media.xiang578.com//resnet.png)

  + bottleneck architectures

  + 为了解决层数变多时，参数数量增加问题。通过 bottleneck 结构，减少维持和左边相同的参数量，然后网络变成 3 层

![](https://media.xiang578.com//bottleneck-architectures.png)

[[Identity Mappings in Deep Residual Networks]]

[[Residual Networks Behave Like Ensembles of Relatively Shallow Network]]

[[ResNet/Question]]

[[Ref]]

  + [残差网络解决了什么，为什么有效？ - 知乎](https://zhuanlan.zhihu.com/p/80226180)

  + [给妹纸的深度学习教学(4)——同Residual玩耍 - 知乎](https://zhuanlan.zhihu.com/p/28413039) 里面有解释 ResNet 的 ReLU 放在哪里的原因

  + [对ResNet本质的一些思考 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/60668529)
