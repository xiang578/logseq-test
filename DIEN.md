---
title: DIEN
alias:
  - @Deep Interest Evolution Network for Click-Through Rate Prediction
type: Paper
public: true
tags:
  - CTR
  - Alibaba
  - Algorithm
date: 2024-10-05
updated: 2025-01-19
toc: true
mathjax: true
---

亮点

  + 1. 引入辅助 Loss：利用 GRU 的 hidden state 与下一个点击的商品做一个

  + 2. 一般模型把用户行为直接当成兴趣，dien 认为用户兴趣是隐藏在行为中，需要去挖掘

![image.png](/assets/image_1737292307135_0.png)

  + feature 分成四类：User Proﬁle, User Behavior, Ad and Context

  + [[interest extractor layer]] 作用 :-> 兴趣抽取层，用 GRU 抽取序列信息
  + [[interest evolving layer]] 作用 :-> 兴趣进化层，将Target Attention引入GRU，过滤掉与待排序的广告不相关的信息。
  + [[AUGRU]] 计算方法 #card
    + 这里是先用序列中Item的隐状态和待排序的广告Embedding计算一个Attention标量，再将该标量乘以更新门控向量。

    + 最终隐藏状态和候选状态，以及每一个维度的重要性，由当前Item隐状态，待排序广告，前一Item隐状态，当前Item原特征（后两者用于计算更新门）共同决定。

源码阅读

  + train.py 指定模型

  + model 中包含对模型的实现

  + 数据

    + uid_voc.pkl: 用户名对应的id

    + mid_voc.pkl: item对应的id

    + cat_voc.pkl:category对应的id

    + item-info:item对应的category信息

    + reviews-info：用于进行负采样的数据

    + local_train_splitByUser:训练数据，一行格式为：label、用户名、目标item、 目标item类别、历史item、历史item对应类别。

    + local_test_splitByUser:测试数据，格式同训练数据

  + 网络设置

    + embeeding 18

    + hidden size 18＊2

    + attention_size 18*2

    + fcn: 200-80-2

    + dice

    + prelu

  + 需要分析代码：

    + aux 网络

    + gru 改造

    + din_fcn_attention

[[Ref]]

  + [详解阿里之Deep Interest Evolution Network(AAAI 2019) - 知乎](https://zhuanlan.zhihu.com/p/50758485)

  + [Deep Interest and Evolution Network for CTR - 知乎](https://zhuanlan.zhihu.com/p/49263704)

  + [也评Deep Interest Evolution Network - 知乎](https://zhuanlan.zhihu.com/p/54838663)
