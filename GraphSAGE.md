---
title: GraphSAGE
type: Paper
public: true
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

Inductive Representation Learning on Large Graphs
[[Inductive Learning]]
GraphSAGE 是一种 inductive 的顶点 embedding 方法
之前的顶点 embedding 基于矩阵分解学习
训练一组聚合函数，从顶点的局部领域中聚合信息特征
降低计算新增节点的复杂度
[[Semi-Supervised Classification with Graph Convolutional Networks]] 框架的 inductive 扩展
aggregator functions 融合目标节点领域的特征，需要具有对称性
mean-aggregator 邻居先求平均，然后 concat 当前节点过全连接
$\mathbf{h}_{\mathcal{N}(v)}^{k} \leftarrow MEAN _{k}\left(\left\{\mathbf{h}_{u}^{k-1}, \forall u \in \mathcal{N}(v)\right\}\right)$
$\mathbf{h}_{v}^{k} \leftarrow \sigma\left(\mathbf{W}^{k} \cdot \operatorname{CONCAT}\left(\mathbf{h}_{v}^{k-1}, \mathbf{h}_{\mathcal{N}(v)}^{k}\right)\right)$
将领域融合的特征和节点本身的特征进行拼接，通过神经网络更新每个节点的特征。
局部频域卷积的一个线性近似
gcn aggregator 结点和邻居先求平均，然后过全连接
$$\mathbf{h}_{v}^{k} \leftarrow \sigma\left(\mathbf{W} \cdot \operatorname{MEAN}\left(\left\{\mathbf{h}_{v}^{k-1}\right\} \cup\left\{\mathbf{h}_{u}^{k-1}, \forall u \in \mathcal{N}(v)\right\}\right)\right.$$
和上一个区别在于当前节点信息什么时候和邻居节点融合，mean 是在 nn 层融合，gcn 是先求平均。
lstm
非对称，通过邻居随机排列来调整对无序集的支持
pooling aggregator
$\overrightarrow{\mathbf{h}}_{\mathcal{N}(v)}^{(k)}=\max \left(\left\{\sigma\left(\mathbf{W}_{\text {pool }} \overrightarrow{\mathbf{h}}_{u}^{(k-1)}+\overrightarrow{\mathbf{b}}_{\text {pool }}\right) \mid u \in \mathcal{N}(v)\right\}\right)$
领域内每个顶点的特征向量通过全链接神经网络独立计算，然脏通过一个逐元素的最大池化来聚合领域信息
如何定义损失函数？
监督学习 [[Cross Entropy]]
无监督学习
$$J_{\mathcal{G}}\left(\mathbf{z}_{u}\right)=-\log \left(\sigma\left(\mathbf{z}_{u}^{\top} \mathbf{z}_{v}\right)\right)-Q \cdot \mathbb{E}_{v_{n} \sim P_{n}(v)} \log \left(\sigma\left(-\mathbf{z}_{u}^{\top} \mathbf{z}_{v_{n}}\right)\right)$$
顶点 u 和顶点 v 是在长度为 l 的 random walk 上共现的顶点。
相邻顶点的表示类似，负采样不类似
$P_n(v)$ 负采样的分布函数
邻域
均匀采样得到固定大小的领域 $\mathcal{N}(v)$, 确保每个 batch 的计算代价是固定的。
顶点 v 在每一层采样不同的领域，在不同层的领域大小都不同。
实验中 2 层，且两次领域数乘积小于 500
[[Ref]]
Weisfeiler-Lehman Isomorphism Test
判断给定两个 Graph 是否同构
[GraphSAGE+FM+Transformer强强联手：评微信的GraphTR模型 - 知乎](https://zhuanlan.zhihu.com/p/279287735)
[【Code】GraphSAGE 源码解析 - 知乎](https://zhuanlan.zhihu.com/p/142205899)