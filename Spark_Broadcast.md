---
title: Spark/Broadcast
public: true
tags:
  - Spark
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

`sc.Broadcast(rdd.collectAsMap())`

算子函数使用外部变量，默认情况 Spark 会将该变量复制多个副本，通过网络传输到 task 中，每个 task 都有一个变量副本。

  + 如果变量本身比较大，会占用增大网络中传输的性能开销，以及在各个节点的 Executor 占用过多内存导致频繁 GC。

  + 通过 Broadcast 的变量只在 Executor 内存中保留一份。
    + Executor 会有对应的 BlockManager，BlockManager 负责管理 Executor 对应的内存和磁盘上的数据。

    + 需要使用广播变量时，先尝试从 BlockManager 获取。如果失败， BlockManager 会从 Driver 或者 其他节点的 BlockManager 拉取变量副本。

```scala
// 以下代码在算子函数中，使用了外部的变量。
// 此时没有做任何特殊操作，每个task都会有一份list1的副本。
val list1 = ...
rdd1.map(list1...)

// 以下代码将list1封装成了Broadcast类型的广播变量。
// 在算子函数中，使用广播变量时，首先会判断当前task所在Executor内存中，是否有变量副本。
// 如果有则直接使用；如果没有则从Driver或者其他Executor节点上远程拉取一份放到本地Executor内存中。
// 每个Executor内存中，就只会驻留一份广播变量副本。
val list1 = ...
val list1Broadcast = sc.broadcast(list1)
rdd1.map(list1Broadcast...)

//如果是变量是 hdfs 文件，先 collect
sc.broadcast(link2NodeMap.collectAsMap())
```
