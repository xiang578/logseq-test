---
url: http://arxiv.org/abs/2208.06979
authors:
- Jizhou Huang
- Zhengjie Huang
- Xiaomin Fang
- Shikun Feng
- Xuyi Chen
- Jiaxiang Liu
- Haitao Yuan
- Haifeng Wang
doi: 10.1145/3511808.3557091
tags:
- Baidu
- ETA
- Paper
- Graph Transformer
- GNN
- traffic prediction
original-title: DuETA: Traffic Congestion Propagation Pattern Modeling via Efficient Graph Learning for ETA Prediction at Baidu Maps
links: [Local library](zotero://select/library/items/BFB5BZYA), [Web library](https://www.zotero.org/users/4911197/items/BFB5BZYA)
title: @DuETA: Traffic Congestion Propagation Pattern Modeling via Efficient Graph Learning for ETA Prediction at Baidu Maps
public: true
date:
- 2022/10/17
alias:
- DuETA
lastMod: 2025-03-15
toc: "true"
---

[[Attachments]]
[DuETA_2022_Huang.pdf](zotero://select/library/items/XWVFNUMJ) {{zotero-linked-file "DuETA_2022_Huang.pdf"}}
核心贡献
新颖性：通过 route-aware graph transformer 捕捉拥堵敏感图中长距离相关性，建模拥堵传播模式
The design of DuETA is driven by the novel ideas that directly capture the long-distance correlations through a congestion-sensitive graph, and that model traffic congestion propagation patterns via a route-aware graph transformer.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

捕捉任意两个（ 距离很远，但是在路况状态上很相关的）segment 之间的交互
These designs enable DuETA to capture the interactions between any two road segment pairs that are spatially distant but highly correlated with traffic conditions.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

通过学习交通拥堵传播模式可以有效提高 ETA 预测效果
traffic congestion propagation patterns
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

核心问题
业务需求
预测的未来路况状态和真实状态不一致会导致 ETA 误差传播 we observed that a propagation of ETA errors arises from the sharp inconsistency between the predicted traffic condition in the future and ground truth. 
ls-type:: annotation
hl-page:: 2
hl-color:: green

建模 traffic congestion propagation patter

Traffic congestion propagation pattern modeling is challenging, and it requires accounting for impact regions over time and cumulative effect of delay variations over time caused by traffic events on the road network. 
ls-type:: annotation
hl-page:: 1
hl-color:: red

当前交通拥堵路段会影响路网上相邻道路的通行能力 As illustrated in it, the impact regions and cumulative delays over time caused by traffic congestion (the road segments in red) would inevitably affect all the interdependent segments on the road network.
ls-type:: annotation
hl-page:: 2
hl-color:: green

用户请求 ETA 时，只有 3-hop 拥堵，但是由于拥堵传播，等用户到达 target 时，2-hop 拥堵，部分y1-hop 缓行
之前使用 [[STGNN]] 类方法建模直接相邻的路段 existing studies have applied spatial-temporal graph neural networks (STGNNs)[7 , 8 , 21 , 34, 35 , 38 ] to model traffic conditions
ls-type:: annotation
hl-page:: 2
hl-color:: blue
 存在两个问题
没有直接建模路网上不相邻 segment 的远距离相关性，网络传播过程中会有信息损失 The long-distance correlations of indirectly connected road segments are not explicitly modeled, which inevitably suffer from information loss during the multi-step message passing.
ls-type:: annotation
hl-page:: 2
hl-color:: blue

由于 STGCNN 方法计算的复杂度，大部分时候补数很少。两个距离较远的 segment 的路况状态特征不能很好传递。 Traffic conditions are not sufficiently transmitted between two road segments that are spatially distant, because they typically execute only a few steps of message passing (one step in most cases), due to the computational complexity of STGNNs.
ls-type:: annotation
hl-page:: 2
hl-color:: blue

[:span]
ls-type:: annotation
hl-page:: 2
hl-color:: green

面临挑战
ETA 任务需要建模 contextual and predictive factors, such as spatial-temporal interaction, driving behavior, and traffic congestion propagation inference
ls-type:: annotation
hl-page:: 1
hl-color:: green

路网中新 segment 和 未知区域 we plan to investigate the transferability of our model to deal with unseen road segments or regions.
ls-type:: annotation
hl-page:: 9
hl-color:: yellow

路线旁边 poi 的影响 Second, given the observation that the travel times of some routes have a considerable correlation with the POIs distributed along the roads. 
ls-type:: annotation
hl-page:: 9
hl-color:: yellow

特定地点特定时间
poi 密集区域对 eta 预测影响 To address this issue, we plan to utilize the POI retrieval system [5, 11, 13] as an auxiliary tool to forecast which POIs would be densely populated and how extensively they would affect the ETA prediction.
ls-type:: annotation
hl-page:: 9
hl-color:: yellow

TODO 待找 poi 相关
MetaLearned Spatial-Temporal POI Auto-Completion for the Search Engine at Baidu Maps.
Personalized Prefix Embedding for POI Auto-Completion in the Search Engine of Baidu Maps
HGAMN: Heterogeneous Graph Attention Matching Network for Multilingual POI Retrieval at Baidu Maps
相关工作
ETA 任务方法
segment-based methods
computationally efficient and scalable
ls-type:: annotation
hl-page:: 9
hl-color:: blue

do not account for the information of the travel route
ls-type:: annotation
hl-page:: 9
hl-color:: blue

end-to-end methods
之间方法对 拥堵传播建模不够 most existing methods are inefficient for modeling the traffic congestion propagation patterns along the route. 
ls-type:: annotation
hl-page:: 9
hl-color:: blue

STGCNN [[Traffic Flow Forecasting]]
提升 GNN 层数感受野增加太多 increasing the depth of a GNN often means exponential expansion of the neighbor scope
ls-type:: annotation
hl-page:: 9
hl-color:: blue

子图 properly extracted subgraph
ls-type:: annotation
hl-page:: 9
hl-color:: blue

[[@ConSTGAT: Contextual Spatial-Temporal Graph Attention Network for Travel Time Estimation at Baidu Maps]] 建模时空关系
[[@SSML: Self-Supervised Meta-Learner for En Route Travel Time Estimation at Baidu Maps]] 建模驾驶员行为
解决方法
traffic conditions 是动态特征
过去 1 小时路况特征，每 5 分钟一个分桶，共 12 个 he traffic conditions of the past one hour are collected as features, which are divided into 12 time slots (5 minutes per time slot)
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

median speed, max speed, min speed, mean speed, and record counts as features
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

Congestion-sensitive Graph $\mathcal{G}^{C S}=\left(\mathcal{L},\left.\left\{\mathcal{E}_r^f\right\}\right|_{r=1} ^5, \mathcal{E}^h\right)$
we construct a congestion-sensitive graph based on the correlations of traffic patterns. 
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

对于某一个 link  找一阶相邻 link 以及高阶相邻link（可能和当前 link 的路况状态有关系）
we take advantage of the first-order neighbor links, as well as the high-order neighbor links whose traffic patterns are highly correlated to that of link 𝑙
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

First-order Neighbors
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

[[ConSTGAT]] 不同相邻 link 对于当前 link 的影响
当前 link 的路况状态可能受下游影响大于上游 the traffic congestion is more likely to propagate from downstream links to upstream links.
ls-type:: annotation
hl-page:: 3
hl-color:: blue

具体过程
定义多种 link 之间关系，并在建图中考虑这些关系 define multiple types of link relations and incorporate these relations into the construction of the congestion-sensitive graph
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

用 attention 分别处理各种关系捕捉影响 use attention mechanism separately for each relation to capture the impact of neighbor links,
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

用 edge 描述两个 link 之间的关系，一共有 5 种类型
[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

An edge describes the relation between two links
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

2 是上游 link
3 是下游 link
剩余三种 link 不在路线中，但是这些 link 的路况状态可能影响目标 link（车辆阻塞路口）
High-order Neighbors
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

间接连接 link 也很重要 the long-distance associations between indirectly connected links are also crucial for ETA prediction
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

如何从高阶邻居采样？
link 从 historical route 从取 2-hop 到 5-hop 的邻居 link
计算 link 和邻居 link 的 Pearson correlation
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
 $c^r_{i,j} = \frac{\operatorname{cov}\left(T_1, T_2\right)}{\rho_{T_1} \rho_{T_2}}$
取 link 过去 2 小时，每 5 分钟的平均通过时间序列 $T_1=\left[t_1^0, t_1^1, \cdots, t_1^{23}\right]$ 和 $T_2=\left[t_2^0, t_2^1, \cdots, t_2^{23}\right]$
累加同一个 link pair 在不同 route 上的相关系数得到 $c^{final}_{i,j}$
每个 link 取相关系数 top5 的邻居 link
连接 link 和 high-order neighbor links high-order edge is defined as an edge that connects a link and one of its high-order neighbor links.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

[[Graph Transformer]] Masked Label Prediction: Unified Message Passing Model for Semi-Supervised Classification
多头学习 edge 的权重 t adopts the multi-head attention mechanism [ 23] to learn edge weights. 
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

对于每个 edge 计算 attention score
$\begin{gathered}\mathbf{q}_{c, i}=\mathbf{W}_c^Q \mathbf{x}_i+\mathbf{b}_c^Q, \\ \mathbf{k}_{c, j}=\mathbf{W}_c^K \mathbf{x}_j+\mathbf{b}_c^K, \\ \mathbf{v}_{c, j}=\mathbf{W}_c^V \mathbf{x}_j+\mathbf{b}_c^V, \\ \alpha_{c, i, j}=\frac{\left\langle\mathbf{q}_{c, i}, \mathbf{k}_{c, j}\right\rangle}{\sum_{k \in \mathcal{N}(i)}\left\langle\mathbf{q}_{c, i}, \mathbf{k}_{c, k}\right\rangle},\end{gathered}$
计算 link i 的表示
$\mathbf{h}_i=\mathbf{x}_i+\frac{1}{C} \sum_{c=1}^C \sum_{j \in \mathcal{N}(i)} \alpha_{c, i, j} \mathbf{v}_{c, j}$
resnet 解决 [[GNN]] 的 oversmoothing 问题 t addresses the oversmoothing problem in vanilla GNNs by residual connections.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

route-aware graph transformer
[:span]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
 
tags:: #[[Model Architecture]] #[[Graph Transformer]]
重新构建的图$\mathcal{G}^{C S}=\left(\mathcal{L},\left.\left\{\mathcal{E}_r\right\}\right|_{r=1} ^6\right)$有六种类型的边，拆分成六张子图，每一张子图用一个 transformer
$\mathbf{h}_i=\mathbf{x}_i+\frac{1}{6 C} \sum_{r=1}^6 \sum_{c=1}^C \sum_{j \in \mathcal{N}_r(i)} \alpha_{c, i, j}^{(r)} \mathbf{v}_{c, j}^{(r)}$
之前的特征 transformer 无法区分一个 link 是否在路线上，无法生成不同的表示
the graph transformer is unable to identify whether a link belongs to a given route or not
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

5a 中路线不同，但是 a 通过 transformer 学习到表示可能相同
[:span]
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

route-aware structural encoding
position encoding
与当前 link 的最近距离
encode the order information of a link.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

控制控制依赖这条 link 路况的程度 be regarded as a gate to control the degree of dependency of the traffic condition when a user requests the ETA.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

route identifier
表示当前 link 是否在路线上
Integration
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

a 1-D convolution layer (Conv1D) with a window size of 3
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

MLP+ReLU 预估每条 link 的 travel time，累加得到整个行程的 eta
$\left[\hat{y}_1, \hat{y}_2, \cdots, \hat{y}_m\right]=\operatorname{MLP}\left(\operatorname{Conv1D}\left(\left[\mathbf{h}_1, \mathbf{h}_2, \cdots, \mathbf{h}_m\right]\right)\right)$
[[Multi-Task Learning]] 优化 link 级别和路线级别 eta Multi-task learning is adopted to optimize the model parameters from both the link-level and the route-level.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

link-level loss function [[Huber Loss]]
$L_{l i n k}\left(\hat{y}_i, y_i\right)= \begin{cases}\frac{1}{2}\left(\hat{y}_i-y_i\right)^2, & \left|\hat{y}_i-y_i\right|<\delta, \\ \delta\left(\left|\hat{y}_i-y_i\right|-\frac{1}{\delta}\right), & \text { otherwise }\end{cases}$
route-level loss function
$L_{\text {route }}(\hat{y}, y)=\frac{|\hat{y}-y|}{y}$
最终 loss
$L=\frac{1}{n} \sum_i^n\left(\frac{1}{m^{(i)}} \sum_{j=1}^{m^{(i)}} L_{\text {link }}\left(\hat{y}_j^{(i)}, y_j^{(i)}\right)+L_{\text {route }}\left(\hat{y}^{(i)}, y^{(i)}\right)\right)$
实验结论
实验数据
行程 link 数和 didi 差不多
2021.10.10-2021.11.20，5周训练，1周测试
指标
mae rmse mape
Baseline
AVG 请求时刻路况速度
STANN
STGNN、attention+LSTM
只考虑相邻 link
[[DCRNN]]
GCN 处理 spatial info
LSTM 处理 temporal info
DeepTravel
bidirectional LSTM
[[ConSTGAT]]
DuETA
the embedding size and the hidden size of DuETA to be 32
ls-type:: annotation
hl-page:: 6
hl-color:: green

attention heads 𝐶 is set to be 8
ls-type:: annotation
hl-page:: 6
hl-color:: green

Adam
3e-5
结果
DeepTravel 和 ConSTGAT
End-to-end methods are more effective than the segment-based methods
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

the correlations of spatial and temporal information are jointly modeled.
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

DuETA
对远距离拥堵更加敏感 sensitive to long-distance traffic congestion,
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

处理交通事件带来的影响 On the other hand, the cumulative effect of delay variations over time caused by traffic events on the road network can be alleviated by the high efficiency of traffic congestion pattern modeling.
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

Ablation Studies
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

主要组件对比
removing both components hurts performance significantly in all three cities.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 6
hl-color:: yellow

route identifier 效果 To obtain an understanding of the effect of the route identifier, we visualize the distributions of the attention weights in Figure 7. 
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

w/o 组 Off route 的 attention weight 比 Complete 组大，加上这个模块模型能更关注路线上的 link
enables DuETA to pay more attention to the links that are in the travel routes.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

congestion-sensitive graph
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

存在部分远处 link 相关性比附近 link 强 he average Pearson correlation coefficients of our selected high-order neighbors is much higher than those of the second-order and third-order neighbors
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow

远处拥堵 case 提升效果大 examine the relative improvements of high-order neighbors in cases of traffic congestion2 and normal traffic.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow


[:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow

Practical Applicability
ls-type:: annotation
hl-page:: 8
hl-color:: yellow

P 发生拥堵，dueta 能预测未来路线上会堵
[:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow

Online Evaluation
ls-type:: annotation
hl-page:: 8
hl-color:: yellow

2022.4.12-2022.4.18
全部、长短单、平峰和高峰
在线 RMSE 高 averaged RMSE scores in the online evaluation of DuETA are higher than those in the offline evaluation
ls-type:: annotation
hl-page:: 8
hl-color:: green

数据噪音大
[:span]
ls-type:: annotation
hl-page:: 9
hl-color:: yellow

读后总结
只考虑下游关系，tcn 之类的考虑上游真的有用吗
