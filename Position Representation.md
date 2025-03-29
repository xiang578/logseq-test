---
public: true
alias:
  - 位置编码
title: Position Representation
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

[[Position Encoding]] 和 [[Position Embedding]] 区别
  + 学习式，不可扩展

    + [[@Convolutional Sequence to Sequence Learning]]

  + 固定式

分类

  + absolute positions 绝对位置编码

  + relative positions 相对位置编码

    + 关注一定范围内的相对次序关系

Position Representation  结果 Concat 和 Add 的区别
  + 联系 :-> 三个 embedding 相加相当于三个原始的 one-hot 拼接再经过一个全连接网络。


  + concat 效果不会比 add 差，但是会增加参数量

Position Representation 信息到达上层之后为什么不好消失？

  + [[ResNet]] 机制，模型输入特征会直接传递到上层

  + 有一个 Transformer 版本每一个 encoder 输入都会加上 position embedding


