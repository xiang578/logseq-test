---
public: true
alias:
  - 即时配送
title: on-demand food delivery
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

派单策略

  + 召回距离

  + 派单距离

  + 拼单上限

难点

  + 出餐时间如何预估？

  + 多任务学习

配送 ETA 分类

![image.png](/assets/image_1692102267709_0.png)

分单挑战

![image.png](/assets/image_1692102312525_0.png)

配送 ETA 和出行 ETA 对比

  + 为什么配送 ETA 是从用户下单到送达，出行 ETA 是从起点到终点的时间？为什么出行不预估从发单到到达终点的时间？

    + 骑手数量供给远大于网约车司机

  + 

TODO 配送相关主题阅读 #XXX

  + TODO [[Applying Deep Learning Based Probabilistic Forecasting to Food Preparation Time for On-Demand Delivery Service]] 美团 深度学习订单出餐时间概率预测 [[KDD/2022]]

  + TODO [[@Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery]]

    + [Order Fulfillment Cycle Time Estimation for On-Demand Food Delivery | Arvin's Blog (arvinzyy.cn)](http://www.arvinzyy.cn/2021/02/07/Order-Fulfillment-Cycle-Time-Estimation-for-On-Demand-Food-Delivery/)

    + [【读论文】20210117-eleOFCT_CompactETA_DTInf - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/344997223)

    + [履约时间预估：如何让外卖更快送达？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/146916779)

  + TODO 美团技术博客配送相关文章
    + [美团外卖骑手背后的AI技术 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2018/03/29/herenqing-ai-con.html)

      + 时间序列问题

        + 事件预测，下一时刻大概会发生什么事情

        + 时机预测，什么时候打电话合适

      + 精细预估

        + 配送时间

        + 上下楼时间

        + 出餐时间

    + [美团智能配送系统的运筹优化实战 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2020/02/20/meituan-delivery-operations-research.html)

    + [配送交付时间轻量级预估实践 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2019/10/10/distribution-time-prediction-practice.html)

    + [机器学习在美团配送系统的实践：用技术还原真实世界 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2018/12/13/machine-learning-in-distribution-practice.html)

    + [即时配送的ETA问题之亿级样本特征构造实践 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2017/11/24/gbdt.html)

    + 美团 郝井华 [[即时配送中的人工智能技术]]

      + [业界 | 每天1800万单，1小时送到，美团外卖如何优化配送模型？-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1133798?cps_key=1d358d18a7a17b4a6df8d67a62fd3d3d)

      + 多场景时间预估

![image.png](/assets/image_1692199943808_0.png)


