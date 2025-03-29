---
title: LightGBM/Question
public: true
deck: being/ML/LightGBM
tags:
date: 2024-10-05
updated: 2025-02-06
toc: true
mathjax: true
---

id:: 63137188-e688-40b0-82ea-1623abcdf2fe

[[Exclusive Feature Bundling]] 中如何确定绑定特征的特征值？ #card
  + 模型可以通过值的范围来辨别不同特征


  + histogram-based 算法会将连续值保存为离散的 bins，将不同特征的值分到 buddle中不同的 bin 中。如果原始值存在相同，可以通过增加偏移量来解决。


分裂方法 :-> [[Histogram-based Algorithm]]
 的优点有那些？ #card
  + 减少特征排序后位置索引的内存占用
，

  + 减少预排序计算量，从 `#data* #features` 到 `#k* #features`


对比 LightGBM 和 XGBoost 的分裂策略区别？
  + XGBoost :-> level-wise 分裂策略
    + 缺点 :-> 对每一层所有节点做无差别分裂，可能有些节点增益非常小，对结果影响不大，但是 xgb 也进行分裂，带来无必要的开销。
  + LightGBM :-> leaf-wise 分裂策略
    + 缺点？ :-> 在当前所有叶子节点选择分裂收益最大的节点进行分裂，一直递归，容易过拟合。
类别特征最优分割
 的原理是什么？ #card
  + 每一次切分尽可能分成两个数量接近的集合


类别特征最优分割
 如何实现？ #card
  + [[目标编码]] 枚举分割点前，直方图按每个类别的label均值进行排序，然后按均值的结果依次枚举最优分割点


histogram 算法相对于 exact 算法有什么内存优势？
  + 排序后对梯度是顺序访问，可以进行 cache 优化

  + 直方图算法的内存消耗 :-> ( `#data* #features * 1Bytes` )

    + 不需要额外存储排序的结果，可以只保存特征离散化后的值。一般用 8 位整型存储。


  + xgboost 的 exact 算法内存消耗为 :-> (`2 * #data * #features* 4Bytes`)
    + 既要保存原始feature的值，也要保存这个值的顺序索引，这些值需要32位的浮点数来保存。

[[Histogram-based Algorithm]] 在 {{c1 选择好分裂特征后，计算分裂收益时}} 相比于 exact 算法有计算优势
  + 预排序算法需要 {{c1 遍历所有样本的特征值}}，时间为 {{c1 #data}}
  + [[Histogram-based Algorithm]] 需要 {{c1 遍历分桶桶}}，时间为 {{c1 #bin}}
lgb 相对于 xgb 有什么改进 #card
  + 内存需求小，xgb pre-sorted 决策树，lgb 基于 histogram 的决策树算法

  + 计算速度快，决策树算法主要包括寻找分割点与数据分割两步。pre-sorted 算法和 histogram 算法在寻找分割点上的时间复杂度是一致的。histogram 所有特征共享一张索引，pre-sorted 一个特征对应一张索引。histogram 随机访问性能好。

  + 通信代价小，适用于分布式计算
