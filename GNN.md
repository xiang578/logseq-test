---
alias:
  - 图神经网络
  - GNN
  - Graph Neural Network
public: true
title: GNN
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

![](https://media.xiang578.com/gnn-arch.png)

任务分类

  + Graph-level task

  + Node-level task

  + Edge-level task

可以利用的信息

![](https://media.xiang578.com/graph-nets-layer.png)

  + nodes,

  + edges,

  + global-context

    + master node or context vector

      + 和全部的点或边相连接

      + 解决 node 和 edge 信息传递速度太慢

  + connectivity

无监督的节点表示学习

  + [[GraphSAGE]]

  + [[GAE]]

图分类

  + 同质图 Homogeneity

    + 图中的节点类型和关系类型都仅有一种

  + 异质图

    + 图中的节点类型或关系类型多于一种

  + 属性图

    + 异质图基础上增加了额外的属性信息

问题

  + oversmoothing

## Ref

  + [图神经网络从入门到入门 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/136521625)

  + [A Gentle Introduction to Graph Neural Networks (distill.pub)](https://distill.pub/2021/gnn-intro/)


    + GNN Predictions by Pooling Information

    + 箱线图 [[boxplot]]

![](https://media.xiang578.com/xiangxiantu.png)

    + [[inductive bias]]

      + graph symmetries 对称性 permutation invariance

        + 交换顶点或边顺序，gnn 保持不变

    + Edges and the Graph Dual

      + 点和边互换

    + Graph convolutions as matrix multiplications, and matrix multiplications as walks on a graph

      + 图上做卷积相当于顶点的邻接矩阵做矩阵乘法

    + [[GAT]] 对邻居的位置不敏感

      + 权重和两个顶点向量相关，和位置无关

  + [CS224W | Home (stanford.edu)](http://snap.stanford.edu/class/cs224w-2020/)
