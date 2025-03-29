---
public: true
title: TFT Interpretability Use Cases
tags:
date: 2024-10-05
updated: 2025-03-15
toc: true
mathjax: true
---

以往基于 attention 进行神经网络解释的方法，侧重于用注意力权重对特定样本的解释。当前方法聚焦如何汇总整个数据集中的模式  #card
  + In contrast to other examples of attention-based interpretability [25, 12, 7] which zoom in on interesting but instance-specific examples, our methods focus on ways to aggregate the patterns across the entire dataset – extracting generalizable insights about temporal dynamics.
ls-type:: annotation
hl-page:: 17
hl-color:: red


检查每个变量对预测的重要性 Analyzing Variable Importance
ls-type:: annotation
hl-page:: 17
hl-color:: yellow
 [[Feature Importance]]  #card
  + 通过分析特征在 [[Variable Selection Networks]] 中的权重大小 (同时考虑 10th，50th，90th 分位数)

  + 结果

    + Static Covariates 可以区分不同物品的特征权重大

      + the largest weights are attributed to variables which uniquely identify different entities (i.e. item number and store number).
ls-type:: annotation
hl-page:: 18
hl-color:: yellow


      + [:span]
ls-type:: annotation
hl-page:: 18
hl-color:: yellow


    + Past Inputs 目标（log sales）是关键，预测是对过去观察结果的外推

      + past values of the target (i.e. log sales) are critical as expected, as forecasts are extrapolations of past observations
ls-type:: annotation
hl-page:: 18
hl-color:: yellow


      + [:span]
ls-type:: annotation
hl-page:: 18
hl-color:: yellow


    + Future Inputs 促销和公共假日比较重要

      + [:span]
ls-type:: annotation
hl-page:: 18
hl-color:: yellow


  + 识别相似的持续模式 identify similar persistent patterns
ls-type:: annotation
hl-page:: 19
hl-color:: red


    + id:: 64400143-1db4-4724-96fb-b0dcf203664a

可视化持续时序模式 Visualizing Persistent Temporal Patterns
ls-type:: annotation
hl-page:: 20
hl-color:: yellow
  #card
  + 把不同分位数损失下的自注意力层权重（或均值）绘制出来。

  + 结论

    + 前三个数据集上，自注意力层的权重值都表现出了于数据特征相符的周期性

识别重大事件 Identifying Regimes & Significant Events
ls-type:: annotation
hl-page:: 20
hl-color:: yellow
  #card
  + 用注意力的相异度（距离）来判断是否有重大事情发生

  + regime-switching behavior
ls-type:: annotation
hl-page:: 20
hl-color:: red
 [[regime switching model]]

    + 随着回报特征（波动性）被观察到在不同的制度之间突然变化  with returns characteristics – such as volatility – being observed to change abruptly between regime
ls-type:: annotation
hl-page:: 20
hl-color:: green


    + 识别这样的转变为寻找显著事件提供洞见  identifying such regime changes provides strong insights into the underlying problem which is useful for identification of the significant events.
ls-type:: annotation
hl-page:: 20
hl-color:: yellow


  + 结论

    + 波动性特征大的时候，注意力的相异度的值也特别大。

[Temporal Fusion Transformer的可解释性 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/464753227)

  + [[@"Why Should I Trust You?": Explaining the Predictions of Any Classifier]] 2016 年 KDD  #card
    + LIME Local Interpretable Model-Agnostic Explanations 提供一种与模型无关的方法，使用可解释的模型和可解释的特征，局部达到和复杂模型相似的效果。

  + [[SHAP]] 从博弈论角度考虑，特征如何影响原始模型的预测值。

[[TFT 关键实验]]

  + 
