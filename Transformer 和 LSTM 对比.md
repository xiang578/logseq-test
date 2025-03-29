---
public: true
tags:
  - Transformer
  - LSTM
url: https://www.zhihu.com/question/439243827
title: Transformer 和 LSTM 对比
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

RNN 为了解决不定长输入，LSTM 的三个门结构为了解决标准 RNN 的梯度爆炸和长序列信息消失问题

硅谷谷主

  + [[self-attention]] 用句子中有所单词向量的加权和来代表某一个单词的向量。

Transformer 缺乏时间维度建模，通过 [[Positional Encoding]] 也和 LSTM 这种天然的时序网络有差距。

  + 缺乏时间维度建模导致深层 Transformer 编码器的每个位置输出都会很相似(每一层不断在上一层的基础上加权和)

Transformer 效果表现好建立在预训练的基础上，单独训练 Transformer 需要大量技巧

  + 编码器层数，attention head 数量，学习率，权重衰减
