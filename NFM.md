---
title: NFM
public: true
tags:
- Algorithm
- Paper
deck: being/paper/NFM
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---


$\hat{y}_{N F M}(\mathbf{x})$ :-> $w_{0}+\sum_{i=1}^{n} w_{i} x_{i}+f(\mathbf{x})$
第一项和第二项是线性回归
引入第三项神经网络学习 :-> 数据之间的高阶特征
网络输入 :-> FM 模型的二阶特征交叉结果
与直接使用高阶 FM 模型相比 :-> 可以降低模型的训练复杂度，加快训练速度。
NFM 的神经网络部分包含 4 层，分别是 Embedding Layer、Bi-Interaction Layer、Hidden Layers、Prediction Score。
![](https://media.xiang578.com/nfm-arch.png)
tags:: #[[Model Architecture]]
Embedding Layer 层对输入的稀疏数据进行 Embedding 操作。最常见的 Embedding 操作是在一张权值表中进行 lookup ，论文中作者强调他们这一步会将 Input Feture Vector 中的值与 Embedding 向量相乘。
Bi-Interaction Layer 层是这篇论文的创新，对 embedding 之后的特征两两之间做 element-wise product，并将结果相加得到一个 k 维（Embeding 大小）向量。这一步相当于对特征的二阶交叉，与 FM 类似，这个公式也能进行化简：
$f_{B I}\left(\mathcal{V}_{x}\right)=\sum_{i=1}^{n} \sum_{j=i+1}^{n} x_{i} \mathbf{v}_{i} \odot x_{j} \mathbf{v}_{j} =\frac{1}{2}\left[\left(\sum_{i=1}^{n} x_{i} \mathbf{v}_{i}\right)^{2}-\sum_{i=1}^{n}\left(x_{i} \mathbf{v}_{i}\right)^{2}\right]$
Hidden Layers 层利用常规的 DNN 学习高阶特征交叉
Prdiction Layer 层输出最终的结果：
$$
\begin{aligned} \hat{y}_{N F M}(\mathbf{x}) &=w_{0}+\sum_{i=1}^{n} w_{i} x_{i} +\mathbf{h}^{T} \sigma_{L}\left(\mathbf{W}_{L}\left(\ldots \sigma_{1}\left(\mathbf{W}_{1} f_{B I}\left(\mathcal{V}_{x}\right)+\mathbf{b}_{1}\right) \ldots\right)+\mathbf{b}_{L}\right) \end{aligned}
$$
实验结果：
![](https://media.xiang578.com/15643059963915.jpg)
tags:: #HOFM
