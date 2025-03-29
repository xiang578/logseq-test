---
public: true
alias:
- 拉普拉斯矩阵
title: Laplacian matrix
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

图的矩阵表示
$L=D-A$
L 是 Laplacian 矩阵
D 是顶点的度矩阵，对角线上的元素依次是各个顶点的度
A 是图的邻接矩阵
![](https://media.xiang578.com//laplacian-matrix.png)
常用拉普拉斯矩阵
Combinatorial Laplacian
$L=D-A$

方阵，主对角线出度，-1 代表两点一阶连通
$D^{-1}$ 顶点是度的倒数
$D^{-1} A$ 归一化，最后每行和为 1
$\tilde{D} ^ {-\frac{1}{2}} \tilde{A} \tilde{D} ^ {-\frac{1}{2}}$ 利用对称矩阵的形式归一化 renormalization
对称归一化的拉普拉斯矩阵（Symmetric normalized Laplacian）
$L^{s y s}=D^{-1 / 2} L D^{-1 / 2}$
随机游走归一化拉普拉斯矩阵（Random walk normalized Laplacian）
$L^{r w}=D^{-1} L$
无向图的拉普拉斯矩阵性质
[[半正定]]
只在中心顶点与一阶相连的顶点上有非0元素
对称，可以进行特征分解 $L=U \Lambda U^{-1}$
$\Lambda$ 是 n 个特征值构成的对角阵
[[特征值]]
可以写成 $L=U \Lambda U^{T}$
