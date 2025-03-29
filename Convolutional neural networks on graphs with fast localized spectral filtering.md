---
public: true
type: Paper
alias:
  - ChebyNet
title: Convolutional neural networks on graphs with fast localized spectral filtering
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

优点

  + 卷积核只有 K 个参数，K 远小于 n

  + 不需要做特征分解，直接用拉普拉斯矩阵 L 进行变换，但是复杂度还是 n3

  + 卷积核具有很好的 局部性


    + K 是卷积核的 receptive field 感受野

    + 每次卷积将中心顶点 k-hop neighbor 的 feature 进行加权求和

    + 例子

![](https://media.xiang578.com/gcn-example-1.png)

      + K=2 时需要二阶 [[Laplacian matrix]]

![](https://media.xiang578.com/gcn-example-2.png)


