---
public: true
links: [Local library](zotero://select/library/items/YGB7L7C9), [Web library](https://www.zotero.org/users/4911197/items/YGB7L7C9)
authors:
  - Haixu Wu
  - Jiehui Xu
  - Jianmin Wang
  - Mingsheng Long
tags:
  - Paper
  - Time Series Transformer
  - Time Series Forecasting
  - autocorrelation
  - NeurIPS/2021
date:
  - 2022/01/07
title: @Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting
alias:
  - Autoformer
updated: 2024-10-05
toc: true
mathjax: true
---

[[Attachments]]

  + [Autoformer_2022_Wu.pdf](zotero://select/library/items/JBITCP29) {{zotero-linked-file "attachments:Autoformer_2022_Wu.pdf"}}

关键信息

  + [[Long Term Series Forecasting]] [[时间序列分解]]

核心贡献

  + Autoformer as a novel decomposition architecture with an Auto-Correlation mechanism
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
 [[Auto-Correlation Mechanism]] 自相关机制，代替点向连接的注意力机制，实现序列级连接和较低复杂度

    + 序列级别依赖发现以及表示聚合 conducts the dependencies discovery and representation aggregation at the sub-series level.
ls-type:: annotation
hl-page:: 1
hl-color:: yellow


  + Decomposition Architecture 深度分解架构，从复杂时间模式种分解出可预测性更强的成分

    + 推理复杂时间模式 intricate temporal patterns
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


      + process the complex time series and extract more predictable components.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


      + 常规对前向数据进行分解，忽视未来可能发生的分解组件之间的潜在交互作用

        + This common usage limits the capabilities of decomposition and overlooks the potential future interactions among decomposed components. 
ls-type:: annotation
hl-page:: 2
hl-color:: blue


      + 分解可以解开纠缠的时间模式并突出时间序列的固有属性 can ravel out the entangled temporal patterns and highlight the inherent properties of time series 
ls-type:: annotation
hl-page:: 2
hl-color:: blue


      + 对子序列进行分解，基于时间序列周期性导出的过程相似性构建一种系列级连接  sub-series at the same phase position among periods often present similar temporal processes
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


      + 逐步分解整个预测过程中的隐藏序列，包括过去的序列和预测的中间结果

        + decompose the hidden series throughout the whole forecasting process, including both the past series and the predicted intermediate results.
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


核心问题

  + 原始序列中各种趋势信息比较混乱，无法在长时间序列中发现时间依赖

    + unreliable to discover the temporal dependencies directly from the long-term time series because the dependencies can be obscured by entangled temporal patterns.
ls-type:: annotation
hl-page:: 1
hl-color:: green


    + 需要处理复杂的时间模式，打破计算效率和信息利用的瓶颈 handling intricate temporal patterns and breaking the bottleneck of computation efficiency and information utilization. 
ls-type:: annotation
hl-page:: 3
hl-color:: blue


    + 待预测序列长度远远大于输入长度

  + Transformer 平方级别复杂度

    + 之前方法尝试使用稀疏 self-attention mproving self-attention to a sparse version
ls-type:: annotation
hl-page:: 1
hl-color:: green


      + 稀疏注意力机制将造成信息的丢失，成为长时间序列预测的瓶颈

    + these models still utilize the point-wise representation aggregation
ls-type:: annotation
hl-page:: 1
hl-color:: blue


  + Transformer  point-wise 维度聚合

    + self-attention 来捕捉时刻间的依赖

      + 难以直接发现可靠的时间依赖

相关工作

  + 之前方法集中在 recurrent connections, temporal attention or causal convolution.
ls-type:: annotation
hl-page:: 2
hl-color:: blue


    + [[DeepAR]] 自回归 + RNN 建模未来序列的概率分布

      + combines autoregressive methods and RNNs to model the probabilistic distribution of future series.
ls-type:: annotation
hl-page:: 2
hl-color:: blue


    + [[LSTNet]] CNNs + ResNet 捕捉 short-term 和 long-term temporal patterns

    + [[TCN]]

  + Transformer 类方法

    + [[Reformer]] [[local-sensitive hashing attention]] #mark/paper

    + [[Informer]] KL + [[ProbSparse Attention]]

  + Decomposition of Time Series

    + 将原始时间序列分解成多个序列，新序列更容易预测

      + each representing one of the underlying categories of patterns that are more predictable.
ls-type:: annotation
hl-page:: 3
hl-color:: blue


    + [[Prophet]] with trend-seasonality decomposition

    + [[N-BEATS]] with basis expansion

    + [[DeepGLO]] with matrix decomposition

    + 缺点

      + 简单分解限制

        + limited by the plain decomposition effect of historical series
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


      + 忽视层次交互

        + overlooks the hierarchical interaction between the underlying patterns of series in the long-term future. 
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


        + 预测问题未来的不可知性，通常方法先对过去序列进行分解，再分别预测，这会造成预测结果受限于分解效果，并且忽视了未来各个组分之间的相互作用。

解决方法

  + Decomposition Architecture
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


    + [:span]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

tags:: #[[Model Architecture]] [[Encoder-Decoder]]

    + series decomposition block
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
 保留周期部分

      + 序列分解成趋势项和周期项部分 separate the series into trend-cyclical and seasonal parts.
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


      + 在预测过程中，模型交替进行预测结果优化和序列分解，从隐藏变量中逐步分离趋势项与周期项

      + 逐步从预测的中间隐藏变量中提取长期稳定的趋势 xtract the long-term stationary trend from predicted intermediate hidden variables progressively. 
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


      + 使用 [[Moving Average]] 平滑周期性、突出趋势项 smooth out periodic fluctuations and highlight the long-term trends
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


        + $\mathcal{X}_{\mathrm{s}}, \mathcal{X}_{\mathrm{t}}=\operatorname{SeriesDecomp}(\mathcal{X})$

          + $\begin{aligned} & \mathcal{X}_{\mathrm{t}}=\operatorname{Avg} \operatorname{Pool}(\operatorname{Padding}(\mathcal{X})) \\ & \mathcal{X}_{\mathrm{s}}=\mathcal{X}-\mathcal{X}_{\mathrm{t}}\end{aligned}$

          + xs seasonal

          + xt trend-cyclial part

    + [[Encoder]]

      + Encoder 输入过去 I 步 $\mathcal{X}_{\mathrm{en}} \in \mathbb{R}^{I \times d}$

      + 建模周期性部分，逐步消除趋势项（在 decoder 中通过累积得到） focuses on the seasonal part modeling
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


        + 当成 decoder 的交叉信息 be used as the cross information to help the decoder refine prediction results
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


      + 流程

        + _ the eliminated trend part
ls-type:: annotation
hl-page:: 4
hl-color:: red
 消除趋势项

        + $\begin{aligned} & \mathcal{S}_{\text {en }}^{l, 1},_{-}=\operatorname{SeriesDecomp}\left(\text { Auto-Correlation }\left(\mathcal{X}_{\text {en }}^{l-1}\right)+\mathcal{X}_{\text {en }}^{l-1}\right) \\ & \mathcal{S}_{\text {en }}^{l, 2},_{-}=\operatorname{SeriesDecomp}\left(\text { FeedForward }\left(\mathcal{S}_{\text {en }}^{l, 1}\right)+\mathcal{S}_{\text {en }}^{l, 1}\right)\end{aligned}$

    + [[Decoder]]  分解对趋势项与周期项建模

      + 一半过去信息 + 填充

        + $\begin{aligned} \mathcal{X}_{\text {ens }}, \mathcal{X}_{\text {ent }} & =\operatorname{SeriesDecomp}\left(\mathcal{X}_{\text {en } \frac{I}{2}: I}\right) \\ \mathcal{X}_{\text {des }} & =\operatorname{Concat}\left(\mathcal{X}_{\text {ens }}, \mathcal{X}_0\right) \\ \mathcal{X}_{\text {det }} & =\operatorname{Concat}\left(\mathcal{X}_{\text {ent }}, \mathcal{X}_{\text {Mean }}\right),\end{aligned}$

        + seasonal part $\mathcal{X}_{\mathrm{des}} \in \mathbb{R}^{\left(\frac{1}{2}+O\right) \times d}$

        + trend-cyclical part $\mathcal{X}_{\mathrm{det}} \in \mathbb{R}^{\left(\frac{1}{2}+O\right) \times d}$

      + 趋势-周期累积结构 the accumulation structure for trend-cyclical components
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


        + 从中间隐变量提取潜在趋势，使得模型可以逐步改进趋势预测并且消除干扰信息，以便于在自相关性中发现基于周期的依赖关系。

        + 其中，对于周期项，自相关机制利用序列的周期性质，聚合不同周期中具有相似过程的子序列；

        + Note that the model extracts the potential trend from the intermediate hidden variables during the decoder, allowing Autoformer to progressively refine the trend prediction and eliminate interference information for period-based dependencies discovery in Auto-Correlation. 
ls-type:: annotation
hl-page:: 4
hl-color:: red


      + the stacked Auto-Correlation mechanism for seasonal component
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


      + 流程

        + $\begin{aligned} \mathcal{S}_{\mathrm{de}}^{l, 1}, \mathcal{T}_{\mathrm{de}}^{l, 1} & =\operatorname{SeriesDecomp}\left(\text { Auto-Correlation }\left(\mathcal{X}_{\mathrm{de}}^{l-1}\right)+\mathcal{X}_{\mathrm{de}}^{l-1}\right) \\ \mathcal{S}_{\mathrm{de}}^{l, 2}, \mathcal{T}_{\mathrm{de}}^{l, 2} & =\operatorname{SeriesDecomp}\left(\text { Auto-Correlation }\left(\mathcal{S}_{\mathrm{de}}^{l, 1}, \mathcal{X}_{\mathrm{en}}^N\right)+\mathcal{S}_{\mathrm{de}}^{l, 1}\right) \\ \mathcal{S}_{\mathrm{de}}^{l, 3}, \mathcal{T}_{\mathrm{de}}^{l, 3} & =\operatorname{SeriesDecomp}\left(\text { FeedForward }\left(\mathcal{S}_{\mathrm{de}}^{l, 2}\right)+\mathcal{S}_{\mathrm{de}}^{l, 2}\right) \end{aligned}$

        + 趋势项，通过累积的方式逐步从预测的隐变量中提取出趋势信息

          + ${\mathcal{T}_{\mathrm{de}}^l =\mathcal{T}_{\mathrm{de}}^{l-1}+\mathcal{W}_{l, 1} * \mathcal{T}_{\mathrm{de}}^{l, 1}+\mathcal{W}_{l, 2} * \mathcal{T}_{\mathrm{de}}^{l, 2}+\mathcal{W}_{l, 3} * \mathcal{T}_{\mathrm{de}}^{l, 3}}$

  + [[Auto-Correlation Mechanism]]

    + [:span]
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


    + 高效的序列级连接，从而扩展信息效用

    + Period-based dependencies 基于周期的依赖发现

      + 不同周期相同相位之间通常表现出相似的子过程 same phase position among periods naturally provides similar sub-processes.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


      + [[Stochastic process theory]] discrete-time process 的 [[autocorrelation]]

        + $\mathcal{R}_{\mathcal{X} \mathcal{X}}(\tau)=\lim _{L \rightarrow \infty} \frac{1}{L} \sum_{t=1}^L \mathcal{X}_t \mathcal{X}_{t-\tau}$

        + $\mathcal{R}_{\mathcal{X} \mathcal{X}}(\tau)$  代表序列 $\{ \mathcal{X}_t \}$ 和 $\tau$ 延迟  $\{ \mathcal{X}_{t - \tau} \}$ 之间的相似性

        + 将这种时延相似性看作未归一化的周期预估的置信度，即周期长度为 \tau 的置信度为 $\mathcal{R}(\tau)$

          + 假设周期为 \tau， $\mathcal{X}_{\tau: L-1}$ 与 $\mathcal{X}_{0: L-\tau-1}$ 会极为相似

      + 取最相关 k 个长度 choose the most possible k period lengths 
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


    + Time delay aggregation 时延信息聚合

      + 该部分聚合组序列 oll the series based on selected time delay
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


      + 相似的子序列信息进行聚合

      + 流程

        + 计算 top k=clogL 个长度

          + $\tau_1, \cdots, \tau_k=\underset{\tau \in\{1, \cdots, L\}}{\arg \operatorname{Topk}}\left(\mathcal{R}_{\mathcal{Q}, \mathcal{K}}(\tau)\right) \\$

        + 计算长度后计算相关性，然后求 softmax

          + $\widehat{\mathcal{R}}_{\mathcal{Q}, \mathcal{K}}\left(\tau_1\right), \cdots, \widehat{\mathcal{R}}_{\mathcal{Q}, \mathcal{K}}\left(\tau_k\right)=\operatorname{SoftMax}\left(\mathcal{R}_{\mathcal{Q}, \mathcal{K}}\left(\tau_1\right), \cdots, \mathcal{R}_{\mathcal{Q}, \mathcal{K}}\left(\tau_k\right)\right) \\$

        + Roll 进行信息对齐，$\mathcal{X}_{0: L-\tau-1}$ 移到序列最前面，$\mathcal{X}_{0: L-\tau-1}$ 和 $\mathcal{X}_{\tau: L-1}$ 保存着相似的趋势信息

          + during which elements that are shifted beyond the first position are re-introduced at the last position
ls-type:: annotation
hl-page:: 5
hl-color:: red


          + $\begin{aligned}\text { Auto-Correlation }(\mathcal{Q}, \mathcal{K}, \mathcal{V})=\sum_{i=1}^k \operatorname{Roll}\left(\mathcal{V}, \tau_i\right) \widehat{\mathcal{R}}_{\mathcal{Q}, \mathcal{K}}\left(\tau_i\right) \end{aligned}$

      + 多头

        + $\begin{aligned} \text { MultiHead }(\mathcal{Q}, \mathcal{K}, \mathcal{V}) & =\mathcal{W}_{\text {output }} * \text { Concat }\left(\operatorname{head}_1, \cdots, \text { head }_h\right) \\ \text { where } \text { head }_i & =\text { Auto-Correlation }\left(\mathcal{Q}_i, \mathcal{K}_i, \mathcal{V}_i\right)\end{aligned}$

      + 复杂度 $\mathcal{O}(L \log L)$

        + 计算 $\tau \in [1, L)$ 的相关性

        + Wiener-Khinchin 理论，自相关信息可以使用[[快速傅里叶变换]] Fast Fourier Transforms
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
 得到

    + 与其他方法对比

      + [:span]
ls-type:: annotation
hl-page:: 6
hl-color:: yellow


    + 序列级高效连接

    + self-attention family only calculates the relation between scattered points
ls-type:: annotation
hl-page:: 6
hl-color:: blue


    + 我们采用时间延迟块来聚合底层周期中相似的子序列。 we adopt the time delay block to aggregate the similar sub-series from underlying periods. 
ls-type:: annotation
hl-page:: 6
hl-color:: yellow


    + 

实验结论

  + 参数设置

    + ADAM + early stopped

    + Autoformer contains 2 encoder layers and 1 decoder layer.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


  + 对比

    + Informer [ 48 ], Reformer [23 ], LogTrans [26 ], two RNN-based models: LSTNet [ 25], LSTM [ 17] and CNN-based TCN [ 4] as baselines.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


    + N-BEATS[ 29 ], DeepAR [34 ], Prophet [ 39 ] and ARMIA
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


  + 实验结果

    + 预测方式 前 96 预测后 96

      + we fix the input length and evaluate models with a wide range of prediction lengths: 96, 192, 336, 720. 
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


    + [[multivariate]]

      + 训练变长预测表现变化也平稳 we can also find that the performance of Autoformer changes quite steadily as the prediction length O increases
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


      + [:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


    + Univariate results
ls-type:: annotation
hl-page:: 8
hl-color:: yellow
 单变量

      + . This situation of ARIMA can be benefited from its inherent capacity for non-stationary economic data but is limited by the intricate temporal patterns of real-world series.
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


      + [:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


  + [[Ablation Study]]

    + Decomposition architecture
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


      + 具有较好的通用性，其他模型加分解结构效果有提升，预测时效的延长，效果提升更明显

        + 减少复杂模式引起的干扰 our method can generalize to other models and release the capacity of other dependencies learning mechanisms, alleviate the distraction caused by intricate patterns
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


      + 对比深度分解架构和先分解再使用两个模型预测的方式，后者参数多，但是表现不好。

      + [:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


    + Auto-Correlation vs. self-attention family
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


      + 效果超过 full attention，序列级别建模带来的收益

      + 可以预测更长序列

      + [:span]
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


  + Model Analysis
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


    + time series decomposition

      + 随着序列分解单元的数量增加，模型学到的趋势项会越来月接近数据的正式结果，周期项可以更好的捕捉序列变化情况。

      + [:span]
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


    + Dependencies learning

      + 找到的注意力更合理 Autoformer can discover the relevant information more sufficiently and precisely.
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


      + 模型自相关机制可以正确发掘出每个周期的下降过程，没有误识别和漏识别，注意力机制存在错误和漏缺

      + [:span]
ls-type:: annotation
hl-page:: 10
hl-color:: yellow


    + Complex seasonality modeling
ls-type:: annotation
hl-page:: 9
hl-color:: yellow


      + 学习到的长度有意义 Autoformer can capture the complex seasonalities of real-world series from deep representations and further provide a human-interpretable prediction.
ls-type:: annotation
hl-page:: 10
hl-color:: yellow


      + 高的部分说明有对应的周期性

      + [:span]
ls-type:: annotation
hl-page:: 10
hl-color:: yellow


    + Efficiency analysis

读后总结

  + 





[[Autoformer Code]]


