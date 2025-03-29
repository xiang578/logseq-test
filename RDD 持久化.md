---
public: true
deck: being/Spark
tags:
- Spark
- RDD
title: RDD 持久化
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

持久化指将数据进行保存，避免数据丢失。

RDD 持久化并非将数据落盘，而是缓存数据，供后续计算使用。

`Cache()`
  + 底层是 persist()，没有指定参数，默认 MEMORY_ONLY

`persist()`
  + 使用指定的方式进行持久化
  + `StorageLevel.`

    + `MEMORY_ONLY`

      + 内存优先

      + RDD 分区空间不够，旧的分区会直接删除

    + `MEMORY_AND_DISK_SER`

      + 优先内存，内存不足到磁盘。

      + 节省重新计算的开销

    + `MEMORY_ONLY_SER`

      + 在内存存放序列化后的数据

        + 序列化存储能减少内存开销，反序列化会增大 cpu 开销

    + `DISK_ONLY`

  + `SER`

    + 序列化保存

Checkpoint

  + 将 RDD 中间结果二进制形式写入磁盘

  + 使用

    + sc.setCheckpointDir("hdfs://hadoop102:9820/output/a")

    + rdd.checkpoint()

    + 手动释放`rddx.unpersist(true)`

## Question

  + RDD 持久化方式？ #card
    + `Cache()`


    + `persist()`


  + memory_only 如果内存存储不了，会怎么操作？ #card
    + 利用 [[LRU]] 的缓存策略把最老的分区从内存中移除

    + 下一次使用被移除的分区需要重新计算
