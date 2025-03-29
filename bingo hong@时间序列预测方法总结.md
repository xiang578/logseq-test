---
public: true
url: "https://zhuanlan.zhihu.com/p/67832773"
title: "bingo hong@时间序列预测方法总结"
tags:
date: "2024-10-05"
updated: "2024-10-05"
toc: true
mathjax: true
---

时间序列问题难点

  + 理解时间序列预测问题是要用历史数据预测未来数据

  + 时间序列问题的训练集、测试集划分

  + 特征工程方法及过程(*方法2的过程很有趣*)

  + 如何转化为监督学习数据集

  + LSTM计算过程理解，包括输入输出维度、参数数量等

  + seq2seq过程的理解，decoder实现

  + attention注意力机制的原理及实现，包括encoder-decoder attention, self attention, multi-head attention等

  + 时间卷积网络的含义，顾名思义就是将CNN方法用于时间序列中，主要是dilated-convolution and causal-convolution

  + prophet预测原理，各参数对模型拟合效果、泛化效果的影响

  + TPA侧重选择关键变量

  + 时间序列基本规则法中周期因子得计算过程

  + 传统方法如周期因子、线性回归、ARMA等的预测结果表现为，预测趋势大致正确，但对波动预测不理想，体现在波动的幅度差异、相位偏移。

  + 时间序列分解方法。理解加法模型和乘法模型，判断分解模型的选取及分解技巧
