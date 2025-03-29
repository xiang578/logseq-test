---
title: Semi-Supervised Classification with Graph Convolutional Networks
type: Paper
public: true
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---


$H^{(l+1)}=\sigma ( \tilde{D} ^ {-\frac{1}{2}} \tilde{A} \tilde{D} ^ {-\frac{1}{2}} H^{(l)} W^{(l)})$
$\tilde{D} ^ {-\frac{1}{2}} \tilde{A} \tilde{D} ^ {-\frac{1}{2}}$ 利用对称矩阵的形式归一化 renormalization

避免顶点的度越大，学到的表示越大
A 是图的邻接矩阵

D 是顶点的度矩阵，对角线上的元素依次是各个顶点的度

$\tilde{A}=A+I_N$
$H^{(l+1)}=\sigma\left(\tilde{A} H^{(l)} W^{(l)}\right)$
$\tilde{A}$ 矩阵 nn，$H^{(l)}$ 矩阵 nm，$W$ 矩阵 mu，$H^{(l+1)}$ 矩阵 nu
$\tilde{A} H^{(l)}$ 考虑节点本身和邻居的信息
![](https://media.xiang578.com/gcn-example.png)
