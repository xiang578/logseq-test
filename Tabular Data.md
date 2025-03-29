---
public: true
alias:
  - 表格类数据
title: Tabular Data
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

表格类数据模型 Ref1 #XXX

  + TODO [用torch lightning 开发tabnet - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/514164924)

    + TODO [[TabNet]]

  + TODO [nn在tabular数据上的发展小结 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/364361806)

  + [NeurIPS'22 | 如何实现表格数据上的迁移学习和零样本学习？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/565781553)

  + [表格类数据上的自监督学习方法综述 Survey on Self-supervised Learning in Tabular Data - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/608240178)

  + TODO [2021年，谁才是表格类数据模型的王者？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/381323980)

    + 数据特性

      + 少量类别特征情况下，手工特征+树模型表现比神经网络自动交叉效果好

    + 评估指标

      + 部分指标不好求二阶导数

    + 归纳偏置

      + 当小部分列包含大部分有意义的信息时候

        + nn 缺少全局 feature selection 以及 gain。

        + lgb 能够做 feature selection 重点分割有价值的列，忽略无价值的列。
