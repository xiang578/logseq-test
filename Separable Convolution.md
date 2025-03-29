---
alias:
- 可分离卷积
public: true
title: Separable Convolution
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

减少卷积计算量
它的核心思想是将一个完整的卷积运算分解为两步进行，分别为Depthwise Convolution与Pointwise Convolution。
![](https://media.xiang578.com//separable-convolution-1.png)
Depthwise Convolution
参数量从  $$d^2k$$ 降到 $$dk$$
![](https://media.xiang578.com//depthwise-convolution.png)
Pointwise Convolution
![](https://media.xiang578.com//pointwise-convolution.png)
