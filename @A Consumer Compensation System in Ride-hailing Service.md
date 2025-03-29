---
date:
- 2023/07/19
authors:
- Zhe Yu
- Chi Xia
- Shaosheng Cao
- Lin Zhou
- Haibin Huang
links: [Local library](zotero://select/library/items/UAXLKKJV), [Web library](https://www.zotero.org/users/4911197/items/UAXLKKJV)
tags:
- SIGIR/2023
- Paper
- Dynamic Pricing
- 2024
- 已读
affiliation:
- didi/货运算法团队
public: true
title: @A Consumer Compensation System in Ride-hailing Service
lastMod: 2024-10-05
toc: "true"
---

[[Attachments]]
[A Consumer Compensation System in Ride-hailing Service_2023_Yu.pdf](zotero://select/library/items/4S77U7I3) {{zotero-linked-file "A Consumer Compensation System in Ride-hailing Service_2023_Yu.pdf"}}
代驾和货运的补贴系统
价格弹性建模 a transfer learning enhanced uplift modeling is designed to measure the elasticity
ls-type:: annotation
hl-page:: 1
hl-color:: yellow

预算分配 a model predictive control based optimization is formulated to control the budget accurately
ls-type:: annotation
hl-page:: 1
hl-color:: yellow

系统目标：在预算范围内，通过补贴最大化平台收入。
Given a total compensation budget or an average compensation rate, find an optimal policy to subsidize queries so that the overall revenue is maximized. 
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

难点
如何用历史数据建模用户弹性 Consumer elasticity
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

个保法下公平原则（不同用户相同 odt 补贴相同） Consumer fairness
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

如何建模线上随机的发单请求 Randomness in queries:
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

Transfer Learning Enhanced Uplift Modeling
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

常规训练 uplift 模型需要大量随机补贴下的响应数据（成本高），本文方法使用大量线上观测数据（有偏，受线上策略影响）和少量随机补贴数据训练模型。
DNN + GBDT：解决 tabular input space and transfer learning
ls-type:: annotation
hl-page:: 2
hl-color:: yellow

超过 90% 特征是 dense numerical feature ，需要用 GBDT建模，但是 GBDT 不好 fine-tuning 新数据以及处理稀疏特征。
训练 s-learner model
[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

两个 XGB 模型分别用观测数据  observational  data 和随机数据 RCT data 训练，目标是二分类（用户是否下单）。
数据过两个 XGB 模型得到叶子信息，再过 embedding 层，concat 两个 embedding  过 inner 层。
先用 observational  data 训练整个网络 Massive observational data is first fed into both inputs to pre-train the model
ls-type:: annotation
hl-page:: 3
hl-color:: red

RCT data 用另外一个输出层训练 RCT data is used to fine-tune using a different output layer
ls-type:: annotation
hl-page:: 3
hl-color:: red

fine-tuning 时使用  early stopping

Optimization Formulation
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

订单聚类成 OD 网格
网格内历史订单平均弹性作为网格弹性 use the mean of the historical query-wise elasticity to forecast the class-wise elasticity
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

model predictive control (MPC) technology
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
 建模成最优化问题求解分配方案
线上系统：离线生成补贴词典供线上使用
[:span]
ls-type:: annotation
hl-page:: 3
hl-color:: yellow

离线实验
Uplift 模型
特征
The features include query information (e.g., the origin, destination, time, weekday, and distance), spatial features (e.g., point of interest information, and order statistics in the same cells), subsidy information, and trading features (e.g., historical order placement rate). I
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

模型细节
ob data xgb，35 棵树，1120 个叶子节点
rct xgb，51 棵树，1314 叶子节点
embedding size 8
The size of the common inner layers and output layer is set to 128, 64, and 32
ls-type:: annotation
hl-page:: 4
hl-color:: green

结果分析
T-XGB+DNN AUUC 效果比 S-XGB+DNN 效果好，说明需要两棵树去提取特征？
S-XGB+DNN：a single GBDT distiller DNN
T-XGB+DNN：two-distiller GBDT  distiller DNN
[:span]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

优化结果评估
假设 uplift 模型结果是真值，评估不同分配策略的影响。
No Cluster Oracle
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
 不对订单聚类，考虑用户特征。
Open Loop 用前 14 天数据预测后 7 天
新系统补贴率低但是更高利润 Compared with the baseline, our system obtains a lower subsidy rate and higher revenue, for its accurate compensation, to achieve a higher ROI.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow

![image.png](/assets/image_1706185089504_0.png)
一些问题？
为什么不是常规构建 uplift 模型的方法（实验组 + 空白对照组）？
T-XGB 和 S-XGB 具体怎么训练？
为什么 rct 树的数量比 ob 树多？从样本角度 ob 树样本更多
uplift 没有给纯 xgb 的