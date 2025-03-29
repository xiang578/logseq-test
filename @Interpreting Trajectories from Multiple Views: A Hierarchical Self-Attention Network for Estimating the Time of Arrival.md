---
url: https://dl.acm.org/doi/10.1145/3534678.3539051
authors: Zebin Chen, Xiaolin Xiao, Yue-Jiao Gong, Jun Fang, Nan Ma, Hua Chai, Zhiguang Cao
doi: 10.1145/3534678.3539051
tags:
  - KDD/2022
  - didi
  - ETA
links: [Local library](zotero://select/library/items/N455U6CR), [Web library](https://www.zotero.org/users/4911197/items/N455U6CR)
title: @Interpreting Trajectories from Multiple Views: A Hierarchical Self-Attention Network for Estimating the Time of Arrival
public: true
date:
  - 2022/08/14
alias:
  - HierETA
isbn: 978-1-4503-9385-0
updated: 2024-10-05
toc: true
mathjax: true
---

[[Attachments]]

  + [Interpreting Trajectories from Multiple Views-2022.pdf](zotero://select/library/items/5MTWJKQK) {{zotero-linked-file "Interpreting Trajectories from Multiple Views_2022_Chen.pdf"}}

关键信息

  + 关键字 [[ETA]] [[self-attention]] [[didi]]

相关工作


  + traffic flow prediction [[Traffic Flow Forecasting]]

    + GMAN: A graph multi-attention network for traffic prediction 基于图的多注意力机制来预测交通状况 GMAN [ 50] employs a graph multi-attention structure to extract the spatial and temporal relationships
ls-type:: annotation
hl-page:: 2
hl-color:: green


      + 图学习通常会受到不相关的空间邻域区域的负面影响，尤其当区域变大，这种影响会导致误差传播  graph representation learning generally suffers from the negative impact from irrelevant spatial neighboring regions, resulting in error propagation especially when the involved area grows larger
ls-type:: annotation
hl-page:: 2
hl-color:: green


      + 图建模被限制在狭窄的邻近区域，在开发大规模城市系统中存在不足  graph modeling is limited to process only narrow neighboring regions and falls short on developing large-scale urban-wise systems
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
 [[ConSTGAT]]

  + travel time estimation

  + trajectory recovery and inference

  + DeepTTE
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
 raw GPS sequences geo-convolutional network LSTM

  + [[WDR]] wide-deep-recurrent network

    + CoDriverETA 2020 滴滴

  + ConSTGAT 和 CompactETA 图建模

  + DeepGTT
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
 deep generative model for learning the distribution of travel time

  + [[HetETA]] learns the representation of spatio-temporal information using a multi-relational network;
ls-type:: annotation
hl-page:: 3
hl-color:: blue


  + [[TTPNet]] 张量分解和图embedding从历史轨迹中学习速度和表示 extracts the travel speed and representation of road network from historical trajectories based on tensor decomposition and graph embedding.
ls-type:: annotation
hl-page:: 3
hl-color:: blue


核心贡献

  + 利用三个视图之间的层次关系对道路底层结构进行建模 HierETA exploits the hierarchical relationship among the three views to portray the underlying road structure
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


  + 分层自自注意力网络根据 segment, link, intersection 之间自然关系进行高效组织 proposed hierarchical self-attention network organizes the segment-, link-, and intersection-views efficiently according to their natural relationships.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


  + 自适应自注意力网络合并，以在多视图表示框架中共同利用全局和局部模式进行时空依赖建模。  adaptive self-attention network to jointly leverage the global and local patterns for spatio-temporal dependency modeling within the multi-view representation framework.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


    + 利用多视图序列明确捕捉轨迹的时空依赖关系 we design an adaptive self-attention network to explicitly capture the spatio-temporal dependencies of the trajectory using multi-view sequences
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


  + hierarchy-aware attention decoder 
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
 利用从不同粒度的信息上学习到上下文特征预估最终 ETA

  + 

核心问题


  + 传统 ETA 方法采用分治策略，将一个轨迹拆分成多个小段，然后累加每个小段的预测结果得到整体 ETA traditional ETA algorithms mainly employ the divide-and-conquer strategy by representing a trajectory as a segment sequence and then summing up the local predictions
ls-type:: annotation
hl-page:: 1
hl-color:: blue


    + segment-view 将轨迹拆分成多个小段，然后通过小段计算同行时间 most of them decompose a trajectory into several segments and then compute the travel time by integrating the attributes from all segments
ls-type:: annotation
hl-page:: 1
hl-color:: blue


      + 累积误差

  + 多视图下建模困难

    + 常规方法用 segment 建模，不考虑 link On the one hand
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


      + 不使用 link 建模，现有的研究很困难对同一个 link 中的多个段之间的一致性建模 However, without explicitly modeling the link-view characteristics, existing studies can hardly model the coherent consistency across segments within the same links.
ls-type:: annotation
hl-page:: 2
hl-color:: red


    + segment 和 intersection 的属性是不一致的， 很难用同一个网络去建模，大部分选择忽视路口或简化建模 On the other hand
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


    + ETA 会受到路口等待影响

  + 什么是 trajectory

    + 三个角度 link、Intersection、Segment

      + segement

        + segment 是人工生成的，用来捕捉细粒度的局部交通情况，在表征道路网络结构方面并不完全 segment-view representation is artificially produced to capture the fined-grained local traffic conditions, which is however not comprehensive in characterizing the natural structure of the road network
ls-type:: annotation
hl-page:: 1
hl-color:: green


      + link

        + 提供静态道路属性，pavement type，道路宽度、道路等级 preserve static road characteristics, such as pavement type, road width and road functional level
ls-type:: annotation
hl-page:: 1
hl-color:: green


      + intersection

        + 等待时间、交通灯数量、历史车流量 valued information such as the waiting time, the number of traffic lights, and the historical traffic volume
ls-type:: annotation
hl-page:: 1
hl-color:: green


    + link 和 intersection 粗粒度表示轨迹属性，link 可以进一步拆分成多个小段，segment 可以细粒度对空间依赖性进行建模 the link- and intersection-views characterize the trajectory attributes from a coarse perspective; a link can be further decomposed into several segments, and hence the segment-view representation models the spatial dependencies at a fine granularity
ls-type:: annotation
hl-page:: 2
hl-color:: yellow


      + 猜测基于作者的假设，两个Intersection 之间的整条路被称之为 Link

    + [:span]
ls-type:: annotation
hl-page:: 2
hl-color:: green


HierETA  Hierarchical Self-Attention Network for Estimating the Time of Arrival

  + [:span]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

tags:: [[Model Architecture]] [[ETA]]

  + Attribute Feature Extractor
ls-type:: annotation
hl-page:: 3
hl-color:: yellow


    + 连续特征 z-score

    + 类别特征 embedding

    + 全局特征共享

  + Hierarchical Self-Attention Network for Multi-View Trajectory Representation
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


    + segment encoder

      + 对同一个 link 内的时空依赖进行建模 capture the spatiotemporal dependencies of segments in the same link 
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


        + a segment encoder is developed to capture the spatio-temporal dependencies at a fine granularity
ls-type:: annotation
hl-page:: 1
hl-color:: yellow


      + 利用 BiLSTM 处理 $[x^s_j|x_r]$，正向和反向结果 concat 成 segment 的表示 $H^s_j$

      + 同一个 link 内 segement 记作 $H^s=\left[H_1^s, \ldots, H_n^s\right] \in \mathbb{R}^{n \times d_s}$

        + 计算出 j-th segment 和 link 内其他 segment 的全局相似度 $G P_j=\frac{Q_j K^T}{\sqrt{d}_s}$

        + a local semantic pattern
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
 局部相似度

          + $L P_j(k)= \begin{cases}G P_j(k), & |j-k| \leq \omega \\ -\infty, & \text { otherwise }\end{cases}$

          + 取 j 相邻 $\omega$ 个 segment 计算相似度

          + 捕获局部 segment 的依赖，加强局部的拥堵转移

      + 用门控机制平衡全局和局部attention结果 a gating mechanism
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


        + $F_j^s=\left(1-z_j\right) \odot \operatorname{Att}\left(G P_j\right)+z_j \odot \operatorname{Att}\left(L P_j\right)$

          + 控制参数怎么学 $z_j=\sigma\left(W_h H_j^s+W_g A t t\left(G P_j\right)+W_l A t t\left(L P_j\right)+b_z\right)$

        + ResNet + LN

      + 所有 link 的 encoder 参数共享以及并行计算

        + n adaptive self-attention module is designed to boost performance
ls-type:: annotation
hl-page:: 1
hl-color:: yellow


    + Joint Link-Intersection Encoder.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


      + 道路属性

      + o characterize the natural trajectory structure consisting of alternatively arranged links and intersections
ls-type:: annotation
hl-page:: 1
hl-color:: yellow


      + 为什么要设计这个模块？

        + segment-view 无法对同一个 link 内 segment 共享的一致性进行建模

          + t fails to model the consistency shared within the same link
ls-type:: annotation
hl-page:: 4
hl-color:: red


        + 粗粒度表示 coarse-scale representation
ls-type:: annotation
hl-page:: 4
hl-color:: red


        + link 和 intersections 交替出现 as links and intersections appear alternatively
ls-type:: annotation
hl-page:: 4
hl-color:: yellow


      + link 表示：$x_i^l=\sum_{j=1}^n \gamma_{i j} h_{i j}^s$

        + link 内的 segment 表示是 $\left\{h_{i j}^s\right\}_{j=1}^n$

        + 加权融合 segment 得到 link 表示，权重计算方法 [[Attention]] $\gamma_{i j}=\operatorname{softmax}_j\left(W_\gamma h_{i j}^s+b_\gamma\right)$

      + 得到 link 和 intersections 的表示后，分别用编码 employ two BiLSTMs to respectively encode the links and intersections
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
 得到 ${H^l_i}$ 和 ${H^c_i}$，concat 在一起得到 $\hat{H}_i^l=\left[H_i^l \mid H_i^c\right]$

      + 上一步得到向量经过 the joint link-intersection encoder also includes a self-attention layer, a residual connection and a layer normalization
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
 得到 $\left\{h_i^l\right\}_{i=1}^m$

      + 去除这个 encoder 中的 local pattern 
ls-type:: annotation
hl-page:: 5
hl-color:: red
 ，因为相邻 link 之间的交通影响更加弱和稀疏，避免过拟合

      + 总结

        + segement-view 捕捉局部交通信息 segment-view context feature that captures the local traffic conditions 
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


        + link-intersection context 表达道路属性 joint link-intersection context feature that preserves the common road attributes
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


  + Hierarchy-Aware Attention Decoder
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
 层次感知注意力解码器

    + realize a tradeoff between the multi-view spatio-temporal features
ls-type:: annotation
hl-page:: 1
hl-color:: yellow


    + sub-route 对于最后的 eta 贡献是不一样的（拥堵路口和道路应该给予更多关注）

      + travel time estimation is closely related to the critical components
ls-type:: annotation
hl-page:: 5
hl-color:: green


    + ETA $\mathcal{R}=(1-\lambda) \sum_{i=1}^m \sum_{j=1}^n \alpha_{i j} h_{i j}^s+\lambda \sum_{i=1}^m \beta_i h_i^l$

      + segment 的表示以及 link-intersection 的表示

      + alpha 和 beta 都是注意力权重

      + 设计注意力引导机制，利用 link-view 之间的关系调整 segment-view 之间的 attention attention guidance that adopts the link-view consistency to further adjust the segment-view attention
ls-type:: annotation
hl-page:: 5
hl-color:: red


        + 先计算 link 的注意力 $\beta_i=\underset{i}{\operatorname{softmax}}\left(f^l\left(h_i^l, x^r\right)\right)$

          + $f^l\left(h_i^l, x^r\right)=v^T \tanh \left(w_1 h_i^l+w_2 x^r+b\right)$

          + xr 是外部影响因素

        + 根据 link 注意力计算 segment 之间注意力 $\alpha_{i j}=\underset{(i, j)}{\operatorname{softmax}}\left(\beta_i f^s\left(h_{i j}^s, x^r\right)\right)$

          + 考虑 segment 之间的重要性，如果不考虑 link 之间的重要性， separately processing each segment without considering the link-view correlation is problematic as it lacks the feedback from the link-view consistency. 
ls-type:: annotation
hl-page:: 5
hl-color:: red


      + 改方法可以自适应选择不同表示粒度中最相关的特征 we can adaptively select the most relevant features from different representation granularities.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow


        + 可以实现是几个 link 权重大，还是几个 segment 权重大

    + $\mathcal{L}(\Theta)=\frac{1}{N} \sum_{k=1}^N\left|Y_k-\hat{Y}_k\right|$

EXPERIMENTS
ls-type:: annotation
hl-page:: 5
hl-color:: green


  + 20 天训练，1 天评估，预测 7 天

  + 数据分布 probability density functions (PDFs) and cumulative distribution functions (CDFs) 
ls-type:: annotation
hl-page:: 5
hl-color:: green


    + [:span]
ls-type:: annotation
hl-page:: 6
hl-color:: yellow


  + We repeat each experiment for five times except the statistics-based approach Route-ETA and report the mean and the standard deviation of different runs.
ls-type:: annotation
hl-page:: 6
hl-color:: green
 训练 5 次取平均

  + 指标 mean absolute error (MAE), root mean squared error (RMSE), mean absolute percentage error (MAPE), and satisfaction rate (SR), similar to existing approaches [ 23 ]. Specifically, SR refers to the fraction of trips with error rates less than 10% and a higher SR indicates better performance and customer satisfaction
ls-type:: annotation
hl-page:: 6
hl-color:: green


  + 实验结果

    + [:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


    + [[ConSTGAT]] ConstGAT considers the graph structures of the road network to exploit the joint relations of spatio-temporal information.
ls-type:: annotation
hl-page:: 7
hl-color:: blue


    + HierETA 更具有可解释性，对潜在道路网络结构进行建模

    + 误差分析：所有距离分桶中指标都提升了，长单提升更加明显。

      + 层次化建模效果好 That is, interpreting the trajectory from multiple views effectively portrays the hierarchical structure of road network and eases the error propagation for estimating the travel time.
ls-type:: annotation
hl-page:: 7
hl-color:: green


      + [:span]
ls-type:: annotation
hl-page:: 7
hl-color:: green


  + 模型分析

    + window sizes
ls-type:: annotation
hl-page:: 8
hl-color:: green


      + 局部窗口效果好

      + segment 之间距离越远，之间的关联性越弱 he correlation between adjacent segments slightly decreases while the modeling uncertainty increases.
ls-type:: annotation
hl-page:: 8
hl-color:: green


      + [:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


    + segment 和 link 的权重

      + 只考虑其中一个指标差

    + [[Ablation Study]]

      + 有无 local 或 global 特征

        + 建模细粒度交通信息 The local attention in encoder is removed to verify the effectiveness for modeling the semantic traffic condition.
ls-type:: annotation
hl-page:: 8
hl-color:: green


        + 提取结构化交通模式 verify the necessity of extracting the structural traffic pattern.
ls-type:: annotation
hl-page:: 8
hl-color:: green


      + 有无 guide

        + 无引导信息

      + 有无 路况信息

      + 有无 层次化结构 removing the joint link-intersection encoder
ls-type:: annotation
hl-page:: 8
hl-color:: green
，没有这个效果显著下降

      + 从 1s 就是变化很大来说，这些网络结构都挺重要的

        + HierETA performs better than both variants that eliminating local and global attentions, which is contributed to the introduction of the global structural and local semantic patterns.
ls-type:: annotation
hl-page:: 8
hl-color:: yellow


      + [:span]
ls-type:: annotation
hl-page:: 8
hl-color:: green

