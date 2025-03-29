---
public: true
status: DOING
title: ETA 技术参考
categories: 智能路
tags:
  - ETA
date:
  - 2023/07/06
permalink: note/eta-ref-list
updated: 2024-10-05
toc: true
mathjax: true
---

持续整理中

<!--more-->

## 滴滴

  + [[@Learning to Estimate the Travel Time]] 2018 年KDD，Wide & Deep & RNN

    + 个人笔记：[(WDR) Learning to Estimate the Travel Time - 算法花园](https://blog.xiang578.com/post/wdr.html)

  + [[@Multi-task Representation Learning for Travel Time Estimation]] 多任务框架，预估行程时间和行程距离

  + [[@HetETA: Heterogeneous Information Network Embedding for Estimating Time of Arrival]] 图卷积应用在 ETA 和路况预测任务

  + [[CompactETA]] link 表达 + mlp

  + [[@Interpreting Trajectories from Multiple Views: A Hierarchical Self-Attention Network for Estimating the Time of Arrival]] 和华南理工合作论文，2022 年KDD。

    + 个人笔记：[【滴滴 HierETA】Interpreting Trajectories from Multiple Views A Hierarchical Self-Attention Network for Estimating the Time of Arrival - 算法花园 (xiang578.com)](https://blog.xiang578.com/post/hiereta.html)

  + Dynamic Heterogeneous Graph Neural Network for Real-time Event Prediction 使用异质图神经网络进行实时事件预测

    + [Dynamic Heterogeneous Graph Neural Network for Real-time Event Prediction （KDD 2020） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/581994896)

## 百度

  + [[@ConSTGAT: Contextual Spatial-Temporal Graph Attention Network for Travel Time Estimation at Baidu Maps]] 时空图注意力网络

    + [工业解密：百度地图背后的路线时长预估模型！](https://mp.weixin.qq.com/s/ZqQN7Qep-6sNbNCAx0UE6A)

  + [[@SSML: Self-Supervised Meta-Learner for En Route Travel Time Estimation at Baidu Maps]]

  + [[@DuETA: Traffic Congestion Propagation Pattern Modeling via Efficient Graph Learning for ETA Prediction at Baidu Maps]]

  + [[@DuTraffic: Live Traffic Condition Prediction with Trajectory Data and Street Views at Baidu Maps]]

## 高德

  + [走近高德驾车ETA（预估到达时间） (qq.com)](https://mp.weixin.qq.com/s/laoI9y8cRRZpbferCM7cBg)

    + 概念

      + SP(Speed Profile)：同一特征日相同时间区间的历史平均速度，按 10min 聚合。例如每周一早上 9:00-9:10，某个 link 上所有轨迹，可以将过去几周聚合求一个平均速度，这个平均速度可以代表对这个 link 在未来周一早上 9:00-9:10 这个时间区间内通行速度的静态预测。

      + AutoLR(Autonavi Location Reference)：实时路况

      + link 通行耗时真值：在一个 5min 的时间窗口内进入某一 link 的所有轨迹，在完成去噪后求取平均值，即得到该 link 在该 5min 窗口内的通行耗时真值。

    + 框架

![](https://media.xiang578.com/202307062006132-gaode-eta.png)

    + 真值生产

      + 将各个 link 上 5min 窗口的实走轨迹聚合求平均通行时间，得到 link 通行耗时真值。

      + 给定 trace 推算通行耗时真值

    + link 场景化预测：根据历史真值将 link 归为不同类别

      + 不堵 link 直接用静态 sp

    + link 级别预测

      + 静态 sp，预测时间跨度可达未来一周

      + 线性模型，通过实时信息 autolr 和历史信息 sp 来拟合 link 级真值

      + 精准预测，模型预测

    + trace 级别预测

      + 准点率预测，给出 trace 级别预测结果的可信度

      + 路线 link 每 5 分钟推演，使用对应时间片的预测结果。超过 1 小时用历史。最后累加得到整条路线 eta。

    + 效果评测层面

      + 对问题 link 的 eta 进行自动干预，人工干预

    + 精准预测

      + 每分钟将 link 级多时间跨度预测值写入缓存，预测是有精准预测值的情况下将有限使用精准预测结果

      + 1小时内有实时路况，使用线性模型预测

    + eta 预测难点

      + 未来流量，让深度模型提前感知拥堵的到来

        + 对导航路线进行时间推演，得到未来时间的位置。

      + [[H-STGCN]] 用域转换器整合异质模态的交通流量特征，设计了复合邻接矩阵使得图卷积层能够更好地捕捉路段间的接近性。

    + 效果评估

      + link 评估

        + bad link 定义 link eta 和 link ata 的 ape 大于 0.3

        + $MSE= \frac{\sum_{i=1}^n \sum_{j=1}^k (link_{i,eta}^j - link_{i, ata}^j)^2}{n * k}$

      + trace 评估

        + trace 的 ata 和 eta 对比

  + [[@Hybrid Spatio-Temporal Graph Convolutional Network: Improving Traffic Prediction with Navigation Data]]
    + 预测流量

    + DARTS

    + [[STGCN]]

    + [高德KDD2020论文解读|混合时空图卷积网络：更精准的时空预测模型 (qq.com)](https://mp.weixin.qq.com/s?__biz=Mzg4MzIwMDM5Ng==&mid=2247485057&idx=1&sn=f5f5dccaf41a00c76d62118bf8a42aa7&chksm=cf4a5e62f83dd774ec9a4ef4fc442c8266b587579ed01171a57b6b3bedcbcc3047edc4134a8f&scene=21#wechat_redirect)

    + [混合时空图卷积网络：能“推导”未来路况的智能算法 (qq.com)](https://mp.weixin.qq.com/s/0fV21yi9Og0dxsKIJ0o0Xw)

  + [深度学习在高德驾车导航历史速度预测中的探索与实践 (qq.com)](https://mp.weixin.qq.com/s/DXMyXfuUtUGcgB33Jvn8YQ)

    + 使用历史平均值法预测历史速度的缺点

      + 对于异常点敏感

      + 无法利用时域序列的演化趋势（trend）信息

      + 无法利用去年同期的车辆行驶规律

    + [[TCN]] 特点

      + 存在因果关系，未来到过去不会存在信息泄漏

      + 可以将任意长度的序列映射到固定长度的序列

      + 利用残差模块和空洞卷积来建构长期依赖关欻

    + 目标：构建一个基于历史信息（某时间段
& 去年同期：同一段道路、确定特征日、确定时间批次）和道路属性来预测未来一周历史速度的机器学习模

    + 网络架构

![](https://media.xiang578.com/202307102238274.png)

  + [AI在出行场景的应用实践：路线规划、ETA、动态事件挖掘…-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/782454)

    + 路径规划

      + 多目标平衡，如何在“帕累托最优”的情况下，进行多个目标之间的取舍、平衡。通过带约束的最优化问题来进行建模，保证其他指标不变差的情况下，把某个指标最优化。

      + 偏置网络，解决陌生场景对导航依赖很重，很难决策哪条路线更好，导致首推路线选择率高。

        + **优化的主要目标是实走覆盖率。**

        + 用户偏置网络，把路线排序的顺序，以及引导路线之间的相似度信息输入进去，期望尽可能消除掉偏置带来的影响。

      + TDR 求路算法提供**随时间推演的能力**。比如 8:00 从起点出发，后面要走 1 2 3 ..n 条路到达目的地，假设 8:10 走到第 2 条道路，8:20 走到第 3 条道路，那么我们在 8:00 计算 Shortcuts 的时候，就不能只用到 8:00 的路况，需要把后续进入某个道路的时刻考虑进来，用那个时刻的路况来计算

    + 交通事件抽取-对比知识蒸馏模型 LRC-BERT AAAI2021

## 饿了么

  + [[@Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery]]

## 美团

  + [[深度学习在美团配送ETA预估中的探索与实践]]：提到挺多 eta 相同的算法和工程细节问题，值得仔细读一读。

  + [[@A Deep Learning Method for Route and Time Prediction in Food Delivery Service]]

## Google

  + [[@ETA Prediction with Graph Neural Networks in Google Maps]]

  + [[@BusTr: Predicting Bus Travel Times from Real-Time Traffic]]

## Uber

  + [[@DeeprETA: An ETA Post-processing System at Scale]]

    + 个人笔记：[【Uber ETA】DeeprETA An ETA Post-processing System at Scale - 算法花园 (xiang578.com)](https://blog.xiang578.com/post/deepreta.html)

    + [How Uber Predicts Arrival Times - Xinyu Hu and Olcay Cirit | Stanford MLSys #64 - YouTube](https://www.youtube.com/watch?v=CJTitzj0qBo)：从两个方面介绍他们的 ETA 系统：how we make it faster 以及 how we make it general(loss 和 calibration)

    + [DeepETA: How Uber Predicts Arrival Times Using Deep Learning | Uber Blog](https://www.uber.com/en-JP/blog/deepeta-how-uber-predicts-arrival-times/)

    + [Day 17 Uber 要如何估計司機和外送的抵達時間？（上）- Self attention 介紹](https://ithelp.ithome.com.tw/articles/10302600)：简单讲了 self-attention 的计算过程

    + [Day 18 Uber 要如何估計司機和外送的抵達時間？（下）- DeeprETANet](https://ithelp.ithome.com.tw/articles/10303293)

      + geospatial features

        + geohashing 转成 string

        + 用 multiple feature hashing 转成 index
