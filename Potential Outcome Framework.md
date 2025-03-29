---
tags:
- Causal Inference
public: true
title: Potential Outcome Framework
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---


Treatment Effect
[[ITE]] 个体干预效果
[[ATE]] Average Treatment Effect，针对全体用户
[[CATE]] 条件，给定条件下的全体用户
[[ATT]] 实验组
简化问题的三个假设 #card
Stable Unit Treatment Value Assumption [[稳定单元干预值假设]]
不同个体的潜在结果之间不会有交互影响
干预水平对所有个体一致
[[No unmeasured confounders]] 没有未测量的混杂因子
$W \perp \!\!\! \perp Y(W=0), Y(W=1) \mid X$
给定X，则分配机制与Y无关
如果两个个体的x一样，则无论W是什么，其潜在结果一样
如果两个个体的×一样，则无论潜在结果是什么，它们的分配机制都一样
Positivity [[正值假设]]
$P(W=w \mid X=X)>0 \quad \forall w$ and $x$
common support / overlap
经典方法
[[Re-weighting methods]] 解决的问题是控制组和治疗组的分布不同
[[Matching methods]] 关键在于如何度量样本之间的相似性
Tree-based Method - [[Causal Forest]] 在分裂最大化 ITE 方差
[[Representation Learning Method]] 本质是对反事实进行预测
[[Meta-Learner]]
评估
