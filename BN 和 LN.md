---
public: true
tags:
  - "Batch Normalization"
  - "Layer Normalization"
deck: "being/Normalization"
title: "BN 和 LN"
date: "2024-10-05"
updated: "2024-11-25"
toc: true
mathjax: true
---

归一化目的是将具有 {{c3 相同性质的数据}}转化成 {{c2 标准正态分布}}，其结果不会破坏 {{c1 数据之间的可比较性}}。
LN 的操作可以类比于从一个句子中找到一个中心词，计算所以词和中心词的关系。

为什么处理不定长序列场景需要 LN ？ #card
  + 使用 BN padding 部分特征 pooling， 会扰乱正常非 padding 部分特征

BN 和 LN 有哪些区别？ #card
  + 做 norm 的维度不同

    + 在哪个维度做 norm，就在其他维度不动的情况下，基于该维度下的所有元素计算均值和方差，然后再做 norm

    + BN 在 batch 维度，LN 一般在最后一维

  + BN 计算代码 :-> `for i in range(seq_len): for j in range(hidden_size): Norm([bert_tensor[k][i][j] for k in range(batch_size)])`
  + LN 计算代码 :-> `for i in range(batch_size): for j in range(seq_len): Norm([bert_tensor[i][j][k] for k in range(hidden_size)]) `
[[Ref]]

  + [RNN为什么不适合做BN？ - 知乎](https://www.zhihu.com/question/308310065)

    + BN 需要记录均值和方差
