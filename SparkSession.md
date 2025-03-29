---
tags:
- Spark
public: true
title: SparkSession
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

Spark 2.0 引入概念，为用户提供统一的切入点来使用 Spark
[[pyspark]] 例子
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName("Word Count") \
	.config(conf=c) \
    .getOrCreate()
```
Scala 例子
创建
`val sparkSession = SparkSession.builder().appName(appName).enableHiveSupport().getOrCreate()`
sql
`sparkSession.sql(sqlStr)`
HiveContext
spark sql 支持 hive 读写
`new HiveContext(SparkSession)`
SparkContext
`sparkSession.sparkContext`
