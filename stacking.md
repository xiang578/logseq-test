---
public: true
title: stacking
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

![](https://media.xiang578.com/202301302016555-stacking.png)
将一系列模型的输出结果作为新特征输入到其他模型，从而实现模型的层叠。
数据不能泄漏，否则会出现过拟合。
方法
训练集数据分成 k 份，每次使用 k-1 份数据训练 k 个模型
利用上面的模型预测没有训练的数据，预测结果做为一个新的特征A
用label+新的特征训练模型训练一个新的模型
测试集先过上面的 k 个模型得到预测结果，结果求平均做为特征A，在经过最后的模型得到结果

[[Ref]]
[Kaggle机器学习之模型融合（stacking）心得 - 知乎](https://zhuanlan.zhihu.com/p/26890738)