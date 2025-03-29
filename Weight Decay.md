---
alias:
- 权重衰减
tags:
- Machine Learning trick
public: true
title: Weight Decay
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

$\theta_{t+1}=(1-\lambda)\theta_t-\alpha \nabla f_t(\theta_t)$
$\lambda$ 是 weight decay 的系数 ，减少参数的值，调节模型复杂度对损失函数的影响
SGD 中权重衰减相当于加入一个 L2 regularization （对损失函数求导，然后化简）
[[L2 Regularization]] 的目的就是为了让权重衰减到更小的值，在一定程度上减少模型过拟合的问题
为什么能避免模型过拟合问题？
过拟合模型的系数往往非常大，因为过拟合就是需要顾忌每一个点，最终形成的拟合函数波动很大，这意味着在某些小区间里的导数值非常大，也就是系数很大，通过正则化约束参数的范围使其不要太大，可以在一定程度上减少过拟合情况。
## Ref
[权重衰减（weight decay）与学习率衰减（learning rate decay）_Microstrong0305的博客-CSDN博客](https://blog.csdn.net/program_developer/article/details/80867468)