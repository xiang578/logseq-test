---
date:
- 2022/03/07
tags:
- Statistics - Machine Learning
- Paper
- Time Series Transformer
- Transformer
- Survey
- Computer Science - Artificial Intelligence
- DAMO Academy
- Electrical Engineering and Systems Science - Signal Processing
- Time Series Forecasting
- Computer Science - Machine Learning
authors: Qingsong Wen, Tian Zhou, Chaoli Zhang, Weiqi Chen, Ziqing Ma, Junchi Yan, Liang Sun
links: [Local library](zotero://select/library/items/H62QARE9), [Web library](https://www.zotero.org/users/4911197/items/H62QARE9)
title: @Transformers in Time Series: A Survey
public: true
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]]

  + Transformers have achieved superior performances in many tasks in natural language processing and computer vision, which also triggered great interests in the time series community.

  + Among multiple advantages of transformers, the ability to capture long-range dependencies and interactions is especially attractive for time series modeling, leading to exciting progress in various time series applications.

    + In this paper, we systematically review transformer schemes for time series modeling by highlighting their strengths as well as limitations. In particular, we examine the development of time series transformers in two perspectives.

      + From the perspective of network structure, we summarize the adaptations and modiﬁcation that have been made to transformer in order to accommodate the challenges in time series analysis.

      + From the perspective of applications, we categorize time series transformers based on common tasks including forecasting, anomaly detection, and classiﬁcation.

    + Empirically, we perform robust analysis, model size analysis, and seasonal-trend decomposition analysis to study how transformers perform in time series.

    + Finally, we discuss and suggest future directions to provide useful research guidance.

  + A corresponding resource list which will be continuously updated can be found in the GitHub repository1.

[[Attachments]]

  + [Transformers in Time Series-2022.pdf](zotero://select/library/items/58ZH9KIU) {{zotero-linked-file "Transformers in Time Series_2022_Wen.pdf"}}

![](https://media.xiang578.com/taxonomy-of-transformers-for-time-series-modeling.png)

## Input Encoding and Positional Encoding

  + Absolute Positional Encoding

  + Relative Positional Encoding

  + Hybrid positional encodings

## Network Modiﬁcations for Time Series

  + [[Positional Encoding]]

    + Vanilla Positional Encoding

    + Learnable Positional Encoding

      + [[A transformer-based framework for multivariate time series representation learning]] introduce an embedding layer in Transformer that learn embedding vectors for each position index jointly with other model parameters.

      + [[Temporal Fusion Transformers]] 使用 LSTM 对位置进行编码，更好适应时序预测任务

    + Timestamp Encoding

      + calendar timestamps(hours, minute...) 和 special timestamps (holidays and events)

      + [[@Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting]] [[Autoformer]] [[FEDformer]] 将 timestamps 特征转换成 embedding 通过网络学习

      + 如何生成好的 timestamp encoding 比较依赖人工先验

  + Attention Module

    + 提升 self-attention 计算效率

![](https://media.xiang578.com/transformer-in-time-series-table-1.png)

      + [[LogTrans]] [ Li et al., 2019 ] and [[Pyraformer]] explicitly introducing a sparsity bias

      + 移除 self-attention 矩阵部分值 [[@Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting]] [[FEDformer]]

  + Architecture Level

    + renovate transformer

    + hierarchical architecture 分层结构

      + 针对考虑到时间序列的多分辨率(多周期，多趋势叠加)

        + [[@Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting]] max-pooling layer

        + [[Pyraformer]] C-ary tree base attention mechanism

          + nodes at the ﬁnest scale correspond to the original time series

          + nodes in the coarser scales represent series at lower resolutions

          + both intra-scale and inter-scale attentions in order to better capture temporal dependencies across different resolutions

## Applications of Time Series Transformers

  + Forecasting

    + Time Series Forecasting

      + [[LogTrans]]

        + proposed convolutional self-attention by employing causal convolutions to generate queries and keys in the self-attention layer 因果卷积引入子注意力计算

        + a Logsparse mask

      + [[@Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting]]

      + AST [[Adversarial sparse transformer for time series forecasting]]

        + 使用生成对抗编码器-解码器架训练用于时间序列预测的稀疏 Transformer 模型

        + 对抗训练可以直接塑造网络的输出来改善预测效果，避免逐步预测带来的累积误差


          + directly shaping the output distribution of network to avoid the error accumulation through one-step ahead inference

      + [[Autoformer]]

        + simple seasonaltrend decomposition architecture 简单季节性趋势分解架构

        + an auto-correlation mechanism working as an attention module 自相关机制注意力模块 $O(L\log L)$

          + measures the time-delay similarity between inputs signal and aggregate the top-k similar sub-series to produce the output

      + [[FEDformer]]

        + 利用 [[Fourier transform]] 和 [[Wavelet transform]] 处理 frequency domain 频域中的注意力操作

          + linear complexity

      + [[@Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting]]

        + multi-horizon forecasting model with static covariate encoders, gating feature selection and temporal self-attention decoder

      + [[SSDNet]] [[ProTran]]

        + combine Transformer with state space models to provide probabilistic forecasts 提供概率预测

      + [[Pyraformer]]

        + hierarchical pyramidal attention module with binary tree following path

        + 分层金字塔注意力模块，二叉树

      + [[Aliformer]]

        + Knowledge-guided attention

    + Spatio-Temporal Forecasting [[Traffic Flow Forecasting]]

      + Trafﬁc transformer: Capturing the continuity and periodicity of time series for trafﬁc forecasting

        + self attention module to capture temporal-temporal dependencies 时序特征

        + Graph neural network module to capture spatial dependencies 空间特征

      + Spatialtemporal Transformer

        + 空间 transformer 辅助图卷积网络来捕获空间依赖关系

      + Spatio-temporal graph Transformer

        + 基于注意力的图卷积机制

    + Event Forecasting

      + temporal point processes (TPP)

  + Anomaly Detection

    + 

  + Classification

    + [[GTN]]

## Experimental Evaluation and Discussion

模型鲁棒性、模型大小以及对时序季节性和趋势捕捉能力

  + robustness analysis, model size analysis, and

seasonal-trend decomposition analysis

  + seasonal-trend decomposition 是 transformer 解决时序预测的重要组成部分

  + 所有模型加上 moving average trend decomposition architecture proposed 结构后，和原始模型相比效果都获得提升

## Future Research Opportunities

  + [[inductive bias]] for Time Series Transformers

    + 避免过拟合，训练 transformer 需要大量数据。

    + 时序数据具有 seasonal/periodic and trend patterns

    + 将对于时序数据模型的理解和特定任务的特征做为归纳偏置引入 transformer

  + [[GNN]]

    + 增强对于空间依赖和多维度之间的关系建模能力

  + [[预训练]]

    + 目前针对时间序列的预训练 transformer 集中在时序分类任务中

  + [[Neural architecture search]]

    + 如果构建高效的 transformer 结构

## Ref

  + TODO [[A transformer-based framework for multivariate time series representation learning]]

  + TODO [[Adversarial sparse transformer for time series forecasting]]

  + DONE [[@Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting]]
completed:: [[2022/11/08]]

  + TODO [[SSDNet]]

  + TODO [[ProTran]]

  + [[LogSparse Transformer]]

  + [Transformer应用于时序任务的综述【2022by阿里达摩院】 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/468823664)

    + 影响预测效果的细节

      + 训练

      + Encoder 间的特征工程


