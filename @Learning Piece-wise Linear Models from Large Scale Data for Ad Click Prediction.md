---
url: http://arxiv.org/abs/1704.05194
publication-title: "arXiv:1704.05194 [cs, stat]"
authors:
- Kun Gai
- Xiaoqiang Zhu
- Han Li
- Kai Liu
- Zhe Wang
tags:
- Computer Science - Machine Learning
- Statistics - Machine Learning
- Paper
- Alibaba
original-title: Learning Piece-wise Linear Models from Large Scale Data for Ad Click Prediction
links: [Local library](zotero://select/library/items/CUMRR2YN), [Web library](https://www.zotero.org/users/4911197/items/CUMRR2YN)
title: @Learning Piece-wise Linear Models from Large Scale Data for Ad Click Prediction
public: true
date:
- 2017/04/18
alias:
- MLR
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]]

  + CTR prediction in real-world business is a diﬃcult machine learning problem with large scale nonlinear sparse data. In this paper, we introduce an industrial strength solution with model named Large Scale Piece-wise Linear Model (LS-PLM). We formulate the learning problem with L1 and L2,1 regularizers, leading to a non-convex and non-smooth optimization problem. Then, we propose a novel algorithm to solve it eﬃciently, based on directional derivatives and quasi-Newton method. In addition, we design a distributed system which can run on hundreds of machines parallel and provides us with the industrial scalability. LS-PLM model can capture nonlinear patterns from massive sparse data, saving us from heavy feature engineering jobs. Since 2012, LS-PLM has become the main CTR prediction model in Alibaba’s online display advertising system, serving hundreds of millions users every day.

[[Attachments]]

  + [Learning Piece-wise Linear Models from Large Scale Data for Ad Click Prediction_2017_Gai.pdf](zotero://select/library/items/HUD6EBAY) {{zotero-linked-file "attachments:Learning Piece-wise Linear Models from Large Scale Data for Ad Click Prediction_2017_Gai.pdf"}}



分片线性方式对数据进行拟合，将空间分成多个区域，每个区域使用线性的方式进行拟合，最后的输出变为多个子区域预测值的加权平均。

相当于对多个区域做一个 [[Attention]]

结构与三层神经网络类似

Model

处理大规模稀疏非线性特征

LS-PLM 模型学习数据的非线性特征。

question 为什么 LR 模型不能区分下面的数据，如何区分数据？[[SVM]][[FM]]

![](https://media.xiang578.com/15795889621354.jpg)

$$p(y=1 | x)=g\left(\sum_{j=1}^{m} \sigma\left(u_{j}^{T} x\right) \eta\left(w_{j}^{T} x\right)\right)$$

u 和 w 都是 d 维向量

m 为划分 region 数量

一般化使用：

$$p(y=1 | x)=\sum_{i=1}^{m} \frac{\exp \left(u_{i}^{T} x\right)}{\sum_{j=1}^{m} \exp \left(u_{j}^{T} x\right)} \cdot \frac{1}{1+\exp \left(-w_{i}^{T} x\right)}$$

可以把上面的模型看成是三层神经网络

![](https://media.xiang578.com/15795894400329.jpg)

Regularization

  + $$\arg \min _{\Theta} f(\Theta)=\operatorname{loss}(\Theta)+\lambda\|\Theta\|_{2,1}+\beta\|\Theta\|_{1}$$

  + L1 和常规一样，保持参数的稀疏性。

  + L2 如下面的公式，对每一个 feature 的参数进行二阶正则，然后累加。最优化的过程中，L2 项越来越小，相当于做特征选择。每一个特征不止一个参数，只有某一个特征的全部参数都为 0 ，代表这个特征是没有用的。

  + $$\|\Theta\|_{2,1}=\sum_{i=1}^{d} \sqrt{\sum_{j=1}^{2 m} \theta_{i j}^{2}}$$

  + 正则后的效果：

![-w839](https://media.xiang578.com/15795899761365.jpg)

@wait 后面如何求解这损失函数以及工程实现待看。

[[Ref]]

  + [CTR预估 五: Algorithm-LR扩展: MLR - 知乎](https://zhuanlan.zhihu.com/p/31530953)

  + [回顾阿里经典CTR预估模型MLR - 知乎](https://zhuanlan.zhihu.com/p/100532677)
