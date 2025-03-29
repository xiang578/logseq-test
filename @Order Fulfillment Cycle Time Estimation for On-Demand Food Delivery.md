---
url: https://dl.acm.org/doi/10.1145/3394486.3403307
pages: 2571-2580
place: Virtual Event CA USA
library-catalog: DOI.org (Crossref)
authors:
- Lin Zhu
- Wei Yu
- Kairong Zhou
- Xing Wang
- Wenxing Feng
- Pengyu Wang
- Ning Chen
- Pei Lee
doi: 10.1145/3394486.3403307
tags:
- ETA
- Paper
conference-name: KDD '20: The 26th ACM SIGKDD Conference on Knowledge Discovery and Data Mining
original-title: Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery
links: [Local library](zotero://select/library/items/7T6G7NAC), [Web library](https://www.zotero.org/users/4911197/items/7T6G7NAC)
title: @Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery
publisher: ACM
public: true
date:
- 2020/08/23
access-date: 2022-09-19T07:15:17Z
language: en
proceedings-title: Proceedings of the 26th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining
item-type:
- conferencePaper
isbn: 978-1-4503-7998-4
lastMod: 2024-10-05
toc: "true"
---

[[Abstract]]
送达时间 Order Fulfillment Cycle Time (OFCT)
a novel post-processing layer
accounting for the distributional mismatch between the true OFCT values and those predicted by the model at initialization
By providing customers with conveniences such as easy access to an extensive variety of restaurants, effortless food ordering and fast delivery, on-demand food delivery (OFD) platforms have achieved explosive growth in recent years. A crucial machine learning task performed at OFD platforms is prediction of the Order Fulfillment Cycle Time (OFCT), which refers to the amount of time elapsed between a customer places an order and he/she receives the meal. The accuracy of predicted OFCT is important for customer satisfaction, as it needs to be communicated to a customer before he/she places the order, and is considered as a service promise that should be fulfilled as well as possible. As a result, the estimated OFCT also heavily influences planning decisions such as dispatching and routing.
[[Attachments]]
[Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery-2020.pdf](zotero://select/library/items/F39LG5CI) {{zotero-linked-file "Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery-2020.pdf"}}
相关工作
ETA 分类
Route-based
OD-based
OFCT 比其他 ETA 独特的挑战
Significantly more influencing factors
location and characteristics of the restaurant
the food preparation time
the orders assigned to the same courier (which will alter his/her delivery itinerary) 骑手配送行为
Unavailability of critical information 预估时缺少关键信息
分配到订单的骑手
最终的路线
Time Window Assignment Problem
## BackGroound
城市划分成区域，区域内配送站
订单终点对应一个指定的 poi 类型(学校、写字楼等)
订单生命周期划分 PT(下单到取到餐)，DT(取餐到送达)，OFCT(下单到送达)，CT(下单到做好)

![](https://media.xiang578.com/order-fulfillment-cycle.png)
流程
用户下单时，预估 OFCT
dispatching 分单
routing 路径规划
VRPTW
骑手到达餐厅取餐
骑手配送
## Feature
订单特征
Spartial feature 空间特征
起点终点 id 和坐标，city/grid id
Temporal feature 时间特征
hour of the day
workday
Order size features 订单大小影响商家出餐速度
sku_num
price
sku_num 低估套餐的大小
Aggregation Features 聚合特征
通过手机传感器收集信息(gps，wifi，bluetooth)，得到 dt/pt/ofct
对上面的信息进行聚合：20 分位数、平均、标准差、80 分位数
通过一定规则选取订单集合，在集合中再分组计算统计信息。
相同 city/grid/restaurant/hour of day 的订单
发单前不同时长完成订单
Dish Features 餐品特征
sku 分配 uid，订单可以用包含的 uid 表示
训练分类模型( 116 类)，使用预测的分类结果
sku 标题做为输入，人工标签
fine-tuning 中文 Bert
Cooking Time Features
出餐时间很难获取真值，从历史数据中挖掘。
三种场景
骑手到达太早，需要等到出餐完成
骑手需要在同一个餐厅取多个订单，只有在餐厅完成最后一个订单才能离开
骑手达到时，如果餐厅完成出餐可以立即进行配送统计
聚合 departure time from the restaurant 得到 ct
Supply-and-Demand Features 供需特征
供需比 demand-to-supply ratio (DSR) $\mathrm{DSR}_{o}=|C|^{-1}\left|O_{o}^{\text {uncompleted }}\right|$
订餐需求在时间和空间上都会有突变，此时通过合并订单配送策略减轻影响。合单策略提升整体配送效率，但是单个订单配送时间变长(骑手需要绕路去取或送)。通过 DSR 来描述这种现象
$O_{o}^{\text {uncompleted }}$ 当前未完成订单，DSR 表示当前未完成订单和活跃配送员数的比例
配送比 dropoff_ratio $o_{o}=\left|O_{o}^{\text {uncompleted }}\right|^{-1}\left|O_{o}^{\text {dropoff }}\right|$
未完成订单中，已经取餐在配送中的订单占比
餐厅出餐量 unfetched_order_count
骑手未取订单数，值越大需要等待的时间越大
单量预测相关，尝试后发现没用
单量预测模型中使用的特征 OFCT 预估模型也使用，没有带来新的信息增益。
图例

e DSR 越大，Bundle 越大，g 对应 OCFT 变大
DSR 一定，dropoff ratio 越大，代表快要释放的运力更多，然后bundle变小，ocft 变小。
![](https://media.xiang578.com/dsr-dropoff-ratio-example.png)
Courier Features 骑手特征
预测 OFCT 时，送单的骑手还没有确定，通过预测模型对附近的骑手进行排序，取 top-ranked 骑手做为派单对象。
相关特征
取单距离
work load 负载，骑手当前未完成订单数
urgency 紧急程度，骑手需要配送订单平均或最小剩余时间
Mutual Distances 订单终点、餐厅、骑手当前订单的终点的最短距离。距离越大，骑手越有可能绕路。
ETA-based Drop-off Time Feature 多维度相似订单的配送 ETA
利用回归模型来学习配送段 ETA 无法很好处理长尾不规律 case，比如高峰期等待电梯
利用历史订单作为配送段时间预估的语料
历史订单用多维特征来表示
新订单通过 k 近邻搜索出相似的历史订单
对相似的历史订单真实配送段时间加权平均，作为新订单的预估配送段时间
通过 OD-based ETA 方法(TEMP+R) 预估餐厅到终点的配送时间特征 DTo
$\mathbf{x}_{\widetilde{o}}^{\text {eta }}=\left[\operatorname{lon}\left(r_{\widetilde{o}}\right) \text {, lat }\left(r_{\widetilde{o}}\right), \operatorname{lon}\left(p_{\widetilde{o}}\right) \text {, lat }\left(p_{\widetilde{o}}\right), \operatorname{hr}\left(a_{\widetilde{\sigma}}^{\text {creation }}\right)\right]^{T} \odot w$
用经纬度+时间组成的向量表示订单，w 表示向量中每一项的权重
$\operatorname{dissim}(\widetilde{o}, \widehat{o})=\left\|\mathbf{x}_{\widetilde{o}}^{\text {eta }}-x_{\widehat{o}}^{\text {eta }}\right\|_{2}$
用 Euclidean distance 表示两个不同订单之间的距离
$\left(\sum_{i=1}^{k} w_{i}\right)^{-1} \sum_{i=1}^{k}\left(w_{i} \cdot \mathrm{DT}_{o_{i}}\right)$
在历史订单中取 k 个最相似订单，构建该特征
$w_{i}=\exp \left(-\frac{\operatorname{dissim}\left(o_{i}, o\right)}{\sigma^{2}}\right)$ 代表权重

Meteorological Features 气象
数值特征
气温
空气质量
风速
类别特征
天气
## Model
网络结构

![](https://media.xiang578.com/ele-ofct-model-architecture.png)
[[Feature Engineering]]
数值特征 归一化+ ELU 升维
维度太低限制神经网络表达
类别特征 embedding +  dropout 避免过拟合
一个类别多个id 对应 embedding 进行 average pooling
骑手特征
召回 pickup 距离在 X 米范围内的骑手组成骑手集合
re-ranking module {{< logseq/mark >}}Query Invariant Listwise Context Modeling (QILCM){{< / logseq/mark >}}
对于每个骑手 c 生成表示向量 hc 以及排序分 sc，利用加权得分表示骑手向量
$\sum_{\forall c \in C^{\text {candidate }}} s_{c} \tilde{\mathbf{h}}_{c}$
Postprocessing 后处理
模型收敛速度慢，预测效果差
模型拟合的数据分布与真实履约时间的分布发生偏移，真实的履约时间实际上是一个右偏长尾的分布，相当于有一小部分订单真实的配送时间偏长而模型没有学习到。
$\mathrm{OFCT}_o^{\text {predict }}=\mu^{\text {real }}+\sigma^{\text {real }} \frac{y_o^{\text {out }}-\mu^{\text {ini }}}{\sigma^{\text {ini }}}$
实现拟合和缩放
y_out 是模型输出
real 是根据真实数据统计的均值和方差
ini 是整个训练集的均值和方差
自适应 [[Box-Cox Transformation]] 逆变换
更加能够拟合长尾数据分布
Objective Function
$\ell_{\text {predict }}+\lambda \ell_{\text {rank }}$
ranking loss + predictive loss
$\ell_{\text {predict }}=\left|\mathrm{OFCT}_o^{\text {predict }}-\mathrm{OFCT}_o\right|$
$\ell_{\text {rank }}=-\sum_{\forall c \in C^{\text {candidate }}}\left(\mathbb{I}\left(c=c_o\right) \log \left(s_c\right)\right)$
cross entropy loss
$\mathbb{I}()$ 是指示函数
## Experiments
Ablation Analysis of Feature Groups 消融实验

订单特征、供需特征
![](https://media.xiang578.com/ofct-table2.png)
不同模型对比
GBM
[[DeepFM]] [[@xDeepFM: Combining Explicit and Implicit Feature Interactions for Recommender Systems]]
简单 concatenation&MLP 策略，不适合 OFCT 任务
[[TEMP+R]] [[MURAT]] OD-based ETA methods
## Conclusion
可以改进的点
cooking time features
weather prediction
## Ref
[履约时间预估：如何让外卖更快送达？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/146916779)