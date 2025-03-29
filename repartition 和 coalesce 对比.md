---
tags:
- Spark
deck: being/Spark
public: true
title: repartition 和 coalesce 对比
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

coalesce


repartition




Spark中repartition和coalesce 相同点 :-> 都是调整分区的方法
Spark中repartition和coalesce 区别 :-> repartition 默认有 shuffle 操作，coalesce 使用 hash paritioner 重新 shuffle 数据
什么情况使用 coalesce 调整分区 :-> filter 之后收缩分区
card-last-score:: 5
card-repeats:: 1
card-next-schedule:: 2022-10-22T02:05:11.083Z
card-last-interval:: 4
  + 为什么 :-> coalesce 不需要 shuffle



