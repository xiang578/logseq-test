---
public: true
tags:
- Spark
title: spark-submit
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

`spark-submit --queue root.queue_name  --executor-cores 2 --num-executors 400`
num-executors：多少个 Executor 节点来执行
executor-memory
executor-cores：executor CPU 核心数
core 同一时间执行一个 task
同一个 executor 中的 core 共享 executor-memory
如果任务占用内存比较多，调小 cores 数，可以使用更多内存
driver-memory
collect 算子将 RDD 拉取到 Driver 处理需要避免 OOM
spark.yarn.executor.memoryOverhead executor 额外预留的内存
spark.default.parallelism
每个 stage 默认 task 数量 500-1000
设置该参数为`num-executors * executor-cores`的2~3倍较为合适
`spark.dynamicAllocation.minExecutors` 以及 `spark.dynamicAllocation.maxExecutors`
运行时动态分配 core 数
`spark.driver.maxResultSize`设置 Executor 端发回数据量 

降低 spark.memory.fraction
