---
title: GCN
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

核心思想

  + GCN 本质用来提取拓扑图的空间特征

  + 利用『边的信息』对『节点信息』进行『聚合』从而生成新的『节点表示』。

Non Euclidean Structure 拓扑图

为什么需要图卷积神经网络？

  + CNN 研究对象是具备 Euclidean Domains 的数据，特征是他们具有规则的空间结构，可以用一维或二维矩阵来表示。

  + CNN 的平移不变性在非矩阵结构数据不适用

    + 平移不变性

      + 输入怎么变形输出都不变

    + 平移可变性

      + 目标检测，物体从图片左侧移到右侧，坐标发生改变。

      + R-FCN，网络变深平移可变性变差。物体在输入上的小偏移，经过多层 pooling 后在小的 feature map 上感知不到。

将 [[CNN]] 扩展到图上，如何在图上实现卷积的各个特性？

  + 权重共享

  + 局部性
    + 第一代 GCN 没有 local 性质，卷积核的运算矩阵在所有位置上都有非 0 元素

    + 第二代的运算矩阵在和当前顶点邻接的位置都是非 0 元素

  + 多尺度

为什么需要 [[Laplacian matrix]]

  + 对称矩阵，可以进行特征分解

  + 拉普拉斯矩阵只在中心顶点和一阶相连的顶点上有非 0 元素

  + 由于卷积在傅里叶域的计算相对简单，为了在graph上做傅里叶变换，需要找到graph的连续的正交基对应于傅里叶变换的基，因此要使用拉普拉斯矩阵的特征向量。

    + 为什么 Laplacian 矩阵的特征向量可以作为[[傅里叶变换]]的基？

如何把卷积推广到 Graph 上

  + $(f * h)_{G}=U\left(\begin{array}{lll}\hat{h}\left(\lambda_{1}\right) & & \\ & \ddots & \\ & & \hat{h}\left(\lambda_{n}\right)\end{array}\right) U^{T} f$
  + [[Laplacian matrix]]分解 可以写成 $L=U \Lambda U^{T}$


[[Spectral Networks and Deep Locally Connected Networks on Graphs]] 图上扩展卷积

  + 基于空域的卷积构建 `Spatial Construction`


  + 基于谱域的卷积构建 `Spectral Construction`


    + 第一代 GCN

      + $y_{\text {output }}=\sigma\left(U g_{\theta}(\Lambda) U^{T} x\right)$


        + $g_{\theta}(\Lambda)=\left(\begin{array}{lll}\theta_{1} & & \\ & \ddots & \\ & & \theta_{n}\end{array}\right)$

    + Spectral graph theory 借助于图的拉普拉斯矩阵的特征值和特征向量来研究图的性质

[[Convolutional neural networks on graphs with fast localized spectral filtering]]

  + 第二代 GCN

  + 把 $\hat{h}\left(\lambda_{i}\right)$ 设计成 $\sum_{j=0}^{K} \alpha_{j} \lambda_{l}^{j}$

  + $y_{\text {output }}=\sigma\left(U g_{\theta}(\Lambda) U^{T} x\right)$


    + $g_{\theta}(\Lambda)=\left(\begin{array}{llll}\sum_{j=0}^{K} \alpha_{j} \lambda_{1}^{j} & & \\ & \ddots & \\ & & \sum_{j=0}^{K} \alpha_{j} \lambda_{n}^{j}\end{array}\right) =\sum_{j=0}^{K} \alpha_{j} \Lambda^{j}$

    + $U \sum_{j=0}^{K} \alpha_{j} \Lambda^{j} U^{T}=\sum_{j=0}^{K} \alpha_{j} U \Lambda^{j} U^{T}=\sum_{j=0}^{K} \alpha_{j} L^{j}$

  + 最终

    + $y_{\text {output }}=\sigma\left(\sum_{j=0}^{K-1} \alpha_{j} L^{j} x\right)$

[[Semi-Supervised Classification with Graph Convolutional Networks]] 利用 Chebyshev 多项式作为卷积核

  + $H^{(l+1)}=\sigma ( \tilde{D} ^ {-\frac{1}{2}} \tilde{A} \tilde{D} ^ {-\frac{1}{2}} H^{(l)} W^{(l)})$


GCN 缺点

  + 训练时需要整个图的结构信息，因此是 transductive 的(训练阶段与预测阶段都是基于同样的图结构)。无法处理 inductive 任务(动态图问题，训练在子图上进行，测试阶段需要处理未知的顶点)

    + [[GraphSAGE]]

  + 不能处理有向图，不容易实现分配不通的学习权重给不通的 neighbor

    + 拉普拉斯举证的特征分解需要拉普拉斯矩阵是对称矩阵

[[Ref]]

  + [图卷积网络 GCN Graph Convolutional Network（谱域GCN）的理解和详细推导-持续更新_无知人生，记录点滴-CSDN博客](https://blog.csdn.net/yyl424525/article/details/100058264) 这个很详细，有 renormaliztion 具体的例子

  + [如何理解 Graph Convolutional Network（GCN）？ - 知乎](https://www.zhihu.com/question/54504471)

  + [论文阅读 (22)图神经网络及认知推理总结和普及-清华唐杰老师_Eastmount的博客-CSDN博客](https://blog.csdn.net/Eastmount/article/details/125016409)

  + [我们真的需要深度图神经网络吗？ - 知乎](https://zhuanlan.zhihu.com/p/278190415)

    + [Do we need deep graph neural networks? | by Michael Bronstein | Towards Data Science](https://towardsdatascience.com/do-we-need-deep-graph-neural-networks-be62d3ec5c59)

    + 图神经网络很难做深？

      + 过度平滑：经过多个卷积层，结点特征趋向于收敛到相同或相似的向量

      + 过度压缩：多层之后，相关的信息压缩到一个结点上，造成瓶颈。
