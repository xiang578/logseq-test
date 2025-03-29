---
public: true
type: Paper
title: AFM
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

AFM(Attentional Factorization Machine), 在 FM 的基础上将 Attention 机制引入到交叉项部分，用来区分不同特征组合的权重。


$$
\hat{y}_{A F M}(\mathbf{x})=w_{0}+\sum_{i=1}^{n} w_{i} x_{i}+\mathbf{p}^{T} \sum_{i=1}^{n} \sum_{j=i+1}^{n} a_{i j}\left(\mathbf{v}_{i} \odot \mathbf{v}_{j}\right) x_{i} x_{j}
$$

单独看上面公式中的第三项结构：

![](https://media.xiang578.com/15643076111641.jpg)
Embedding Layer 与 NFM 里面的作用一样，转化特征。
Pair-wise Interaction Layer 是将特征两两交叉，如果对这一步的结果求和就是 FM 中的交叉项。
Attention 机制在 Attention-based Pooling 层引入。将 Pair-wise Interaction Layer 中的结果输入到 Attention Net 中，得到特征组合的 score ${a_{i j}^{\prime} }$，然后利用 softmax 得到权重矩阵 ${a_{ij}}$。
$$
\begin{aligned} a_{i j}^{\prime} &=\mathbf{h}^{T} \operatorname{Re} L U\left(\mathbf{W}\left(\mathbf{v}_{i} \odot \mathbf{v}_{j}\right) x_{i} x_{j}+\mathbf{b}\right) \\ a_{i j} &=\frac{\exp \left(a_{i j}^{\prime}\right)}{\sum_{(i, j) \in \mathcal{R}_{x}} \exp \left(a_{i j}^{\prime}\right)} \end{aligned}
$$
最后将 Pair-wise Interaction Layer 中的二阶交叉结果和权重矩阵对应相乘求和得到 AFM 的交叉项。
![](https://media.xiang578.com/15643086043204.jpg)
## Question
AFM 如何引入 Attention 机制？
根据 $<v_i, v_j>x_i x_j$ 计算交叉特征的权重
