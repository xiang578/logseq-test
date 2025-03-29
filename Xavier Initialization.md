---
title: Xavier Initialization
public: true
author:
  - Xavier Glorot
tags:
  - Algorithm
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

Glorot 条件 :-> 好的初始化应该使得各层的激活值和梯度的方差在传播过程中保持一致。
  + `mean=0.0， std_dev=(2.0 / (input_dim + output_dim)) ** 0.5`

  + tf.contrib.layers.xavier_initializer

  + `W = tf.Variable(np.random.randn(node_in, node_out)) / np.sqrt(node_in)`

保持输入与输出的方差一致。在线性函数上推导出来，部分非线性函数比如（tanh）也可以使用。ReLU 需要使用 [[He Initialization]] 解决

## Ref

  + [初始化方法 - Keras中文文档](https://keras-cn.readthedocs.io/en/latest/other/initializations/)
