---
public: true
title: long-tailed
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

常用解决方法

  + 重采样 re-sampling

    + 过采样 oversampling，增加数量少的类别样本

      + 增加正样本使得正负样本数目接近

      + 原始正类之间插值来生成额外的正类

    + 欠采样 undersampling，剔除一些数量多的类别样本

      + 去除负样本使得正负样本数目接近

      + 将负样本划分成多个集合供不同的学习器使用

  + 数据合成

    + 样本增加高斯噪声 data smoothing

    + SMOTE

      + 随机选取一个正样本，然后用 k 近邻选取一个与其最相似的样本，取两个样本中值或者均值，作为新样本。

  + 重加权 re-weighting

    + 通过样本权重或者 loss 权重给数量多的类别降权，给数量少的类别加权。

    + [[F1 Reweight Loss]] 调节二分类模型 recall/precision 相对权重的损失函数

      + [[F1 Score]]

      + F_beta

        + $F_\beta=\left(1+\beta^2\right) \cdot \frac{\text { precision } \cdot \text { recall }}{\left(\beta^2 \cdot \text { precision }\right)+\text { recall }}$

      + $\beta$ 大于 1，重 recall，小于 1 关注准确

  + 增加辅助任务

    + 引入自监督对比学习

  + 迁移学习 tranzsfer learning

  + 度量学习 metric learning

  + 阈值移动 threshold-moving

    + 二分类中将 0.1 当成是正样本

      + 模型倾向于样本多的部分

    + 再缩放 rescalling

  + 模型融合

    + 0.1 正样本，0.9 负样本，负样本拆成 9 份。利用负样本和正样本训练 9 个模型，加权得到最后的结果

[分类机器学习中，某一标签占比太大（标签稀疏），如何学习？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/372186043)

  + 难易样本不均衡还是正负样本不均衡

    + [[Focal Loss]] 针对困难样本，标签稀疏不一定是困难样本。


