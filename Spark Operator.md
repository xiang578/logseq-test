---
title: Spark Operator
public: true
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

区分 RDD 的方法和 Scala 集合对象的方法
Scala 集合对象的方法在同一个节点的内存中完成
RDD 的方法可以将计算逻辑发送到 Executor 端执行
Transformation
map
mapPartitions
映射函数的参数从 RDD 中的每一行元素变成 RDD 中每一个分区的迭代器
一次函数调用会处理一个 partition 所有数据
内存不够，可能会导致 OOM。
解决映射过程中需要频繁创建额外的对象
mapPartitionsWithIndex
多增加一个分区索引
sample
flatMap 先映射，再扁平化
filter
union 求并集
多个 RDD 合并
```scala
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = sc.parallelize([4, 5, 6])
rdd3 = sc.parallelize([7, 8, 9])

rdd = sc.union([rdd1, rdd2, rdd3])
rdd.collect()

## [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
intersection 交叉口，求交集
distinct
groupby
按 key 分组，value 合并（能相加就相加，不能加成为一个数组）
groupByKey
reduceByKey
和 groupByKey
 的区别？
reduceByKey 会先在 map 端聚合，减少 reduce 端压力
有时候使用 groupByKey 执行时间长，极易发生内存溢出
如果 key 非常少，value 非常多，reduceByKey 会触发 shuffle 操作，可以先对数据进行一次 repartition
aggregateByKey
sortByKey
repartition
实现原理 `coalesce(numPartitions, shuffle = true)`
默认对数据进行 [[Spark Shuffle]]
partitionBy
针对 `RDD[(K, V)]`
按指定规则对数据进行重新分区
默认分区器 `HashPartitioner`
repartitionAndSortWithinPartitions(partitioner: Partitioner)
针对 repartition 重分区后进行排序的场景
针对 `RDD[(K, V)]`
传入 partitioner 分区
对数据进行排序
连接
join
leftOuterJoin()
rightOuterJoin()
join
cogroup
cartesian
pipe
coalesce
`rdd.coalesce(numPartitions = 2, shuffle=false)`
调整 RDD 分区数量
收缩合并分区，减少任务调度成本
使用 coalesce 增加分区必定会导致数据倾斜
为什么使用 coalesce 合并分区后会导致数据倾斜？ #card
coalesce 没有对数据进行 [[Spark Shuffle]]，原来属于同一分区的数据会同时进入一个新的分区
cache
Action：遇到一个 action 算子，提交一个 job
reduce
collect
show
first
take 取前几条记录
takeSmaple
takeOrdered 返回前 n 个元素，并按默认顺序排序。
count
countByKey
foreach
lookup 返回给定 key 对应的所有值
saveAsTextFile
saveAsSequenceFile
saveAsObjectFile
collectAsMap kypairs 以 map 形式保存到 driver 上，注意可能会超过 driver 的内存上限
KeyBy：指定 key，将 RDD 变成 key-value 格式