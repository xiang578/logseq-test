---
title: RDD
alias:
- Resilient Distributed Dataset
tags:
- Spark
deck: Computer/Spark
public: true
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

共享内存模型
只读的记录分区的集合
依赖关系
窄依赖 narrow dependency
OneToOneDependency
父 RDD 每个分区只被子 RDD 的一个分区所使用
不需要 shuffle
map，union
宽依赖 wide dependency/shuffle
父 RDD 的每个分区可能被多个子 RDD分区所使用，会有 shuffle 产生
groupByKey
Partitioner 分区器
定义如何分布数据
一个 RDD 分成多少个分区，每个分区数据量多发，从而决定每个 Task 将处理哪些数据
可使用分区器
[[HashPartitioner]] 给定的 key，计算 hashCode，对分区个数取余
[[RangePartitioner]] 尽量保证每个分区中的数据量均匀，且分区与分区之间是有序的。
rangeBounds
自定义分区器
## Question
RDD是弹性数据集，“弹性”体现在哪里呢？
存储弹性
spark 计算产生的中间结果会保存在内存中，如果内存不足会自动存储在磁盘
容错弹性
计算过程中如果出错会自动重试
task 失败会重试
stage 失败会重试失败的分片
计算弹性
如果计算过程中数据丢失，会根据 RDD 的依赖关系重新计算得到数据
分区弹性
RDD 会根据文件大小动态分区
你觉得RDD有哪些缺陷？
惰性计算，中间数据默认不保存，每次操作都会对数据集重复计算，某些计算量比较大的操作可能会影响系统的运行效率。
RDD分区和数据块有啥联系？