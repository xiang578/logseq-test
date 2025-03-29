---
public: true
title: Web Traffic Time Series Forecasting 1st place solution
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[[Feature Engineering]]
局部特征
当发现有一个趋势，希望趋势持续。自回归模型
当发现一个流量高峰，高峰逐渐衰减。[[移动平均]]
当发现节假日流量高，期望未来的节假日流量都会高。季节性
全局特征
按年、按月有很强的 [[自相关]]
y轴是自相关系数，90 天和 365 天的系数比较大
![](https://media.xiang578.com/autoccorr.png)
具体实现：尽可能减少特征工程，通过模型发现和学习特征
浏览量
通过对数转换变成正态分布
day of week
year to year autocorrelation quarter-to-quarter autocorrelation
page popularity 区分高频页面和低频页面
This scale information is lost in a __pageviews__ feature, because each pageviews series independently normalized to zero mean and unit variance.
流量中位数
lagged pageviews
Feature preprocessing
数据采样(数据增强)
600 天数据，固定训练样本长度 200 天，有 400 天可以做为起点。
模型
为什么使用 RNN 模型
比统计学时间序列模型[[ARIMA]]更灵活有效
非参数化方法
DONE 为什么两个 GRU 不一样？
Encoder
cuDNN GRU
输入 256,284,267 batch,time,features
输出 283,256,267 time batch features
Decoder
GRUBlockCell
`tf.whil_loop()`
支持将上一步输入加入到当前步输入
![](https://media.xiang578.com//web-traffic-time-series-forecasting-model.png)
tags:: #[[Model Architecture]] [[Encoder-Decoder]] [[Seq2Seq]] [[GRU]]
解决长时间序列(700天)依赖
LSTM/GRU 预测限制：100-300 items
[[Attention]] 能带来远处过去信息。fixed-weight sliding-window attention
效果不稳定
![](https://media.xiang578.com//fix.png)
取过去重要节点的编码器输出，用 FC 压缩维度，加到解码器的输入特征中
减少 noise 进行平滑：`attn_365 = 0.25 * day_364 + 0.5 * day_365 + 0.25 * day_366`
利用 1D CNN 计算平滑的权重
^^lagged datapoint 滞后数据特征^^ [[lag feature]]
捕捉固定周期的历史信息
将每个日期对应前四个季度的数据输入到解码器中
![](https://media.xiang578.com//loged-datapoint.png)
Losses and regularization
[[SMAPE]] 解决预测值和真值都接近 0 的情况
```python
epsilon = 0.1
summ = tf.maximum(tf.abs(true) + tf.abs(predicted) + epsilon, 0.5 + epsilon)
smape = tf.abs(predicted - true) / summ * 2.0
```
[[RNN]] 如何正则化
Reducing model variance
使用不同种子训练 3  个模型，每次训练在 10500-11500 区间保存 10 个 checkpoints，最后预测合并。
无法知道如何 early stopping
SGD averaging (ASGD) SGD + 动量
相当于[[bagging]] 模型
Hyperparameter tuning
超参搜索 [SMAC3](https://automl.github.io/SMAC3/stable/)
Ref
[1st place solution | Kaggle](https://www.kaggle.com/c/web-traffic-time-series-forecasting/discussion/43795)