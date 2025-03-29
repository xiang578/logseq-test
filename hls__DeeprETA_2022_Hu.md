---
file: [DeeprETA_2022_Hu.pdf](file:///Users/didi/Dropbox/zotero-lib/DeeprETA_2022_Hu.pdf)
file-path: file:///Users/xry/Dropbox/zotero-lib/DeeprETA_2022_Hu.pdf
public: true
title: hls__DeeprETA_2022_Hu
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

routing engine
Routing engines divide up the road network into small road segments represented by weighted edges in a graph. 
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
graph-based models used by routing engines can be incomplete with respect to realworld planning scenarios typically encountered in ride-hailing and delivery
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
路线不确定

人为失误：开错路
分布偏移：不同任务到达时间分布不同
Empirical arrival time distributions differ markedly across different tasks
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
预估形式不确定：不同业务对 ETA 诉求不同，比如预估价需要平均 ETA，用户可能需要 ETA 分布或者期望
Uncertainty estimation. Different ETA use cases call for distinct point estimates of the predictive distribution.
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
We take a hybrid approach, termed ETA post-processing, that treats the routing engine ETA as a noisy estimate of the true arrival time. We use a deep residual ETA network, referred to as DeeprETANet, to predict the difference between the routing engine ETA and the observed arrival time.
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
routing engine ETA
DeeprETANet 预估 routing engine ETA 和 the observed arrival time 的残差
本文创新点
ETA Post-processing
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
DeeprETANet Architecture
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
Multi-resolution Geospatial Embeddings
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
geo 相关信息如何 embedding
相关工作
geo 相关信息如何 embedding

Past works have encoded these locations with multi-scale sinusoidal embeddings
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
三角函数
have used LSTMs to learn geospatial embeddings [29]
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
LSTM
[30 ] use grid embeddings of latitude and longitude in which the grid cell is augmented with the relative distances between the original point and the four corners of grid.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
格子
In [15 ], latitude and longitude are embedded separately over uniform grids to reduce cardinality, and graph pretraining is used to incorporate road network connectivity information for each origin and destination. 
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
A wide and deep recurrent network was proposed to capture spatial-temporal information [27]. This model uses a cross-product of embeddings to learn feature interactions, which is commonly used in recommendation systems
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
[[@Learning to Estimate the Travel Time]]
Routing Engine ETA
The begin and end location neighborhoods of a request account for a large proportion of noise.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
上下车点偏差带来 RE-ETA 预估不准确
特征
[:span]
hl-type:: area
hl-stamp:: 1675210287675
hl-page:: 3
ls-type:: annotation
系统的挑战性
firstly, the RE-ETA data and the residual distribution are skewed and have long tails.
ls-type:: annotation
hl-page:: 3
hl-color:: green
数据分布倾斜以及长尾

[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
Log-transformation is usually used for normalizing skewed data distribution. 通常使用对数变换来处理这个问题
hl-page:: 3
ls-type:: annotation
transforming the log-scale prediction back to the original scale by exponentiation usually results in some extreme values, which may affect user experience. 预测结果需要经过 exp 还原，可能产生异常值
hl-page:: 3
ls-type:: annotation
We propose to solve this issue by using an asymmetric loss function. 
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
### asymmetric Huber loss function

Secondly, heterogeneity of data is due to multiple trip/request types;
ls-type:: annotation
hl-page:: 3
hl-color:: green
网约车 ETA 和 配送 ETA 分布不一致（数据异构性）
[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
we design a model structure to deal with trip heterogeneity specifically
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
Thirdly, this post-processing system needs to handle a large volume of requests with a low latency.
hl-page:: 3
ls-type:: annotation
低延迟
## DeeprETA Post-Processing System
[:span]
hl-type:: area
hl-stamp:: 1675210539620
hl-page:: 4
ls-type:: annotation
### an Embedding module
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
#### 特征处理 #[[Feature Engineering]]

calibration features
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
区分是什么类型 ETA 请求
The calibration features convey different segments of the trip population such as whether it is a delivery drop-off or ride-sharing pick-up trip.
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
we found discretizing and embedding all the features provided a significant accuracy lift over using continuous features directly. 特征离散化 + embedding 有显著效果提升
hl-page:: 3
ls-type:: annotation
Categorical features
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
Continuous features
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
quantile bucketizing function 数值等频分桶
hl-page:: 4
ls-type:: annotation
等频分桶效果优于等距分桶
We found that using quantile buckets provided better accuracy than equal-width buckets, similar to other literatures have suggested [19 ]
hl-page:: 4
ls-type:: annotation
分位数分桶单位bit下传达更多原始特征信息
One explanation is that for any fixed number of buckets, quantile buckets convey the most information in bits about the original feature value compared to any other bucketing scheme.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
Geospatial features
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
$\boldsymbol{e}_k=E_k\left[H\left(x_k\right)\right]$
为什么这么做？
唯一字符串表示地理信息，然后再对字符串做 embedding
The idea is to first obtain a unique string to represent the2D geospatial information and then map the string to a unique index for embedding look-ups.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
[[Geohash]]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
`geohash(lat, lng, u) => encoded geohash strings`
u 指定 string 长度
将 lat, lng 转换成 [0,1] 之间浮点数，再转换成整数，最后用 base32 编码成字符串
[:span]
hl-type:: area
hl-stamp:: 1676206598188
hl-page:: 4
ls-type:: annotation
[:span]
ls-type:: annotation
hl-page:: 4
hl-color:: red
Feature hashing 将 encoded geohash strings 变成 index
hl-page:: 4
ls-type:: annotation
Exact indexing
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
每个 grid cell 有单独 embdding，geohash 精度越高，该方法内存消耗越大
Multiple feature hashing
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
使用多个哈希函数将格子转化成 index，减少哈希冲突
细节
起点经纬度、终点经纬度、起终点对经纬度都做为特征
MurmurHash 使用不同的种子初始化
使用 $u \in \{4,5,6,7\}$，多种大小的格子，减少数据稀疏性影响
### a Two-layer Module
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
Interaction layer
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
每一个向量代表一个独立特征，无顺序要求（不需要位置编码）
each vector represents a single feature
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
[:span]
ls-type:: annotation
hl-page:: 5
hl-color:: red
Linear self-attention
输入矩阵 $L*d，L >> d$
attention 矩阵计算速度太慢
[[linear transformer]] [[Linformer]] [[performer]]
$\begin{aligned} V_i^{\prime} & =\frac{\sum_{j=1}^L \phi\left(Q_i\right)^T \phi\left(K_j\right) V_j}{\sum_{j=1}^L \phi\left(Q_i\right)^T \phi\left(K_j\right)} \\ & =\frac{\phi\left(Q_i\right)^T \sum_{j=1}^L \phi\left(K_j\right) V_j}{\phi\left(Q_i\right)^T \sum_{j=1}^L \phi\left(K_j\right)}\end{aligned}$
$\phi(x)=\operatorname{elu}(x)+1=\max \left(\alpha\left(e^x-1\right), 0\right)+1$
$f\left(X_{e m b}\right)=V^{\prime}+X_{e m b}$
复杂度: $O(Ld^2)$
Calibration layer
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
输入请求 ETA 类型，得到一个对应的偏置
$\hat{r}_{\mathrm{ij}}=\hat{f}_2\left(\hat{f}\left(X_{i_{\mathrm{emb}}}\right)\right)+\hat{b}_j\left(X_{i_{\mathrm{type}}}\right)$
$b_j$ 第 j 种类型 ETA 的偏置（可学习）
f Interaction 层
f2 全连接层
优点
相当于对预测结果进行整体偏移，最小时间成本
[[MMoE]] 或 [[Multi-Head Attention]]
We also tried the multi-heads structure and mixture of expert structure
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
ReLU 限制预测值范围
## 5 MODEL TRAINING AND SERVING
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
不同类型 ETA 任务需要用不同的指标来评估
when ETA is used for calculating fares, mean ETA error is important
hl-page:: 6
ls-type:: annotation
evaluating delivery ETA requests, not only the mean absolute ETA error, but also the 95th quantile is important.
ls-type:: annotation
hl-page:: 6
hl-color:: green
### asymmetric Huber loss function
对异常值鲁棒性更好，可以平衡多种常用的点估计指标
$\mathcal{L}\left(\omega, \delta, \Theta ;\left(\boldsymbol{q}, y_0\right), y\right)= \begin{cases}\omega \mathcal{L}\left(\delta, \Theta ;\left(\boldsymbol{q}, y_0\right), y\right), & y<\hat{y} \\ (1-\omega) \mathcal{L}\left(\delta, \Theta ;\left(\boldsymbol{q}, y_0\right), y\right), & y \geq \hat{y}\end{cases}$
$\mathcal{L}\left(\delta, \Theta ;\left(\boldsymbol{q}, y_0\right), y\right)= \begin{cases}\frac{1}{2}(y-\hat{y})^2, & |y-\hat{y}|<\delta \\ \delta|y-\hat{y}|-\frac{1}{2} \delta^2, & |y-\hat{y}| \geq \delta\end{cases}$
$\omega \in[0,1], \delta>0$ 分别控制对高低估倾向以及异常值的容忍程度
that control the degree of robustness to outliers and the degree of asymmetry respectively.
hl-page:: 6
ls-type:: annotation
$\delta$  越大，对异常值越不敏感
低估和高估有不同的权重（对业务影响不同）
$\Theta$ 代表模型参数
优点：模拟其他回归损失函数以及使点估计满足多样性的业务指标
These parameters not only make it possible to mimic other commonly used regression loss functions, but also make it possible to tailor the point estimate produced by the model to meet diverse business goals.
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
每周训练模型
## 6 EXPERIMENTS
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
baseline methods
HammockNet
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
在 [[tabular data]] 中优于 XGBoost
DeeprETANet
qkv d=4
fc size=2048
Adam as the optimizer and relative cosine annealing learning rate scheduler.
ls-type:: annotation
hl-page:: 7
hl-color:: yellow
变形
One variant is without feature hashing, i.e. simply using the geohash function and indexing the geohash string. 无 feature hashing
hl-page:: 6
ls-type:: annotation
The other variant is without the calibration layer 无校准层
hl-page:: 6
ls-type:: annotation
评估指标
mean absolute error (MAE), 50th percentile absolute error (p50 error) and 95th percentile absolute error (p95 error
ls-type:: annotation
hl-page:: 7
hl-color:: red
数据集
The dataset consists of global ETA requests from Uber’s platform. The global data has two types of requests, one is ride-hailing and the other is eats delivery.
ls-type:: annotation
hl-page:: 7
hl-color:: red
14 天数据
离线实验
p95 error 模型有无 feature hashing 表现相似，地理信息可能在典型 case 上有提升，但是不能改善极端错误
For the p95 error, DeeprETANet with and without feature hashing has similar performance. This result indicates that richer geospatial embeddings improve performance in typical cases but may not improve extreme errors
ls-type:: annotation
hl-page:: 7
hl-color:: green
w/o calibration 层效果比 restnet 等方法差
对数据采样，分析 RE-ETA 残差和模型 ETA 残差
We can also see the difference before and after DeeprETA post-processing from Figure 7, which visualize the bivariate distribution of the RE-ETA residual and the predicted ETA residual on a 1% sampled data. Although rides and delivery requests have quite different residual distributions, after post-processing the mean residual is closer to 0.
ls-type:: annotation
hl-page:: 7
hl-color:: green
6.5 Online experiments 在线实验
ls-type:: annotation
hl-page:: 8
hl-color:: yellow
The median latency is 3.25ms and the 95th percentile is 4ms.
ls-type:: annotation
hl-page:: 8
hl-color:: green
6.6 Embedding Analysis
ls-type:: annotation
hl-page:: 8
hl-color:: yellow
[[t-SNE]]
1 temporal embedding
深色 weekend 浅色 weekday
minute-of-week embedding 具有局部连续性，没有明确的周末或工作日效应
local continuity
ls-type:: annotation
hl-page:: 8
hl-color:: green
one-dimensional manifold 一维流形
[:span] 
hl-type:: area
hl-stamp:: 1675819746664
hl-page:: 8
ls-type:: annotation
14 geospatial embeddings
颜色代表 speed buckets
hl-page:: 8
ls-type:: annotation
局部聚集性，相似的位置有相似的表示，不同 ETA 的表示部分相似
Similar locations are represented by similar positions in two-dimensional space. Interestingly, the high speed locations of rides and delivery requests do not all overlap.
ls-type:: annotation
hl-page:: 8
hl-color:: green
[:span]
hl-type:: area
hl-stamp:: 1675819938929
hl-page:: 9
ls-type:: annotation
7 CONCLUSION
ls-type:: annotation
hl-page:: 8
hl-color:: yellow
有这样分离架构（RE+模型）的任务都可以尝试使用这种方法提升效果
one of the benefits of our hybrid approach is that it is decoupled from the details of any particular routing engine implementation, and we expect that teams using other routing engines will be able to achieve similar accuracy improvements using our method. 
ls-type:: annotation
hl-page:: 9
hl-color:: yellow
解决不同类型 ETA 数据异制性
请求类型编码放到模型中学习
One is to embed request types for learning the interaction between the type features and others via the interaction layer.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
校准层，每个类型 ETA 都有一个 bias
The other way is through a calibration layer. The calibration layer consists of a fully connected layer and some bias parameters for each request type. 
ls-type:: annotation
hl-page:: 5
hl-color:: yellow

[:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow