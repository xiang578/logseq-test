---
public: true
title: Feature Engineering/Time Series Feature
alias:
- 时序特征
- 时间序列特征工程
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

时间戳衍生
时间特征：年月日、节假日、星期几、上午中午下午凌晨
布尔特征：是否周末
时间差特征
time encoding
周期特征循环编码
好处：相邻两天的 encoding 结果相似
[[sklearn]] functiontransformer

[[sklearn]] functiontransformer
```python
def sin_transformer(period):
    return FunctionTransformer(lambda x: np.sin(x / period * 2 * np.pi))
def cos_transformer(period):
    return FunctionTransformer(lambda x: np.cos(x / period * 2 * np.pi))
```
时序值衍生
寻找时间序列的趋势因素，季节性周期性因素
滞后值 [[lag feature]]
取过去 X 个时间步作为 feature
lag 之间的同比环比n阶差分
昨天、上周同一天等数据高度相关
滑动窗口统计 Rolling Window Statistics
先前时间观察值的统计信息做为特征
前 7 天数据的平均数、中位数、标准差、最大值、最小值
过去数据被聚合成标量，也可以做比例、差值之类的运算
滞后值 [[lag feature]]
 的滑动窗口为 1
扩展窗口统计 Expanding Window Statistics
统计整个序列的全部数据
序列属性衍生
连续变量衍生
其他连续变量特征
股票收盘佳之外还成交量、开盘价等
类别变量 Encoding
类别少时可以用 one-hot encoding
类别如果与顺序无关，放到树模型中会被当成是连续型处理
与 y 做特征交互
预测销量时，统计某个产品类别下的销量均值、标准差等
[[目标编码]]
Ref
[时间序列数据的特征工程总结 - 知乎](https://zhuanlan.zhihu.com/p/388551117)
[时序数据中的特征工程（待续） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/466773545)
tsfresh 自动提取各种时间特征