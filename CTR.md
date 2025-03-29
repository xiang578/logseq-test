---
public: true
tags:
  - Algorithm
title: CTR
date: 2024-10-05
updated: 2025-01-11
toc: true
mathjax: true
---

互联网广告的核心要素是: 媒体、素材、算法

意义

  + 用户角度：克服信息过载，推荐系统在信息过载的情况下，用户如何高效获得感兴趣信息的问题

  + 公司角度：推荐系统解决产品能够最大限度地吸引用户、留存用户、增加用户粘性、提高用户转化率的问题，从而达到公司商业目标连续增长的目的。

指标

  + CTR 点击率

  + CVR 转化率

    + SSB: Sample Selection Bias，训练时集合是点击的样本，正样本为转换的，负样本为未转化。预测时空间为全体样本，存在 bias
    + DS: Data Sparsity，点击样本原小于爆光样本

评估方法

  + 离线评估 [[AUC]]

  + AB 实验

技术方向

  + [[协同过滤]]：协同大家的反馈、评价和意见一起对海量的信息进行过滤，从中筛选出目标用户可能感兴趣的信息的推荐过程。

  + [[矩阵分解]]：使用更稠密的隐向量表示用户和物品，挖掘用户和物品的隐含兴趣和隐含特征。

    + [[Neural CF]] 利用 MLP 替代原来 MF 中的点击

  + [[CTR Model]]

    + [[大规模离散 Logistic Regression]]


      + 稀疏性

        + [[Lasso Regression]] L1

        + [[Ridge Regression]] L2

      + 非线性

        + 特征变换

          + [[GBDT+LR]] 利用 GBDT 产生高维非线性特征

            + 树模型很难学习高度稀疏数据的特征组合

            + 树的深度决定是几阶交叉

            + GBDT 的特征转化方式实际上失去了大量特征的数值信息，不一定就会比 FFM 效果好。

        + 离散化

        + 交叉特征

          + 全交叉 $x M x$

            + [[FM]] 模型自动学习组合特征

          + 细化 $x_i*x_j$ 前面的系数

            + [[FFM]] 相同的特征归于同一个 field，每一个特征 xi，针对其他特征的每一种 filed 都会学习一个 $v_{i,f_j}$。~~部分特征属于相同的领域，同一个领域使用同一个embedding，可以达到降维的作用。~~

            + [[AFM]] 根据 $<V_i, V_j>x_i x_j$ 计算交叉特征的权重
            + [[FiBiNET]] $\sum_{i=1}^n \sum_{j=i+1}^n\left(v_i W v_j\right) x_i x_j$

              + SENET Layer 和 Bilinear-Interaction Layer

            + hash trick lr

            + CGL

          + 全半交叉

            + LASER

        + [[MLR]] 通过多个局部 model 解决长尾问题

          + 端到端的非线性学习能力，模型稀疏性强。

    + Trees

      + TDM

      + [[TDM]]

      + [[Deep Retrieval]]

    + [DNN & Embedding](CTR-DNN)

      + 典型的深度CTR模型可以分成以下四个部分：输入、特征嵌入（Embedding）、特征交互（有时候也称为特征提取）和输出。

        + input->embedding

        + embedding：concatenate, product, weight sum, bi-interaction

        + embeding->output

          + 这一步中如果使用 mean pooling 会丢失部分信息

      + 通过 embedding 来对输入数据进行降维

      + [[POLY2]] 暴力组合交叉特征

      + [[FNN]] 解决 DNN 中输入的特征过多，利用 FM 预训练的隐向量做 embedding，然后接 MLP。没有端到端训练，降低深度学习模型复杂度和训练不稳定性。

      + [[Wide&Deep]] 模型两种能力，人工特征工程，联合训练

      + [[PNN]] 将特征交叉的结果输入到 DNN 中，在不同特征域之间进行特征交叉。左边 emb 层的线性部分，右边 emb 层的交叉部分 向量内积和外积。交叉方式多样化，但是对所有的特征进行无差别交叉。

      + [[NFM]] Deep 部分进行修改，引入特征交叉池化层。二阶交叉不去sum pooling，而是后接一个 MLP

      + [[Deep Crossing]] embedding + MLP 结构，摆脱人工特征工程，特征深度交叉。

      + [[ONN]]

      + [[Deep&Cross]] 二阶交叉到高阶交叉之间的特征交叉，bit-wise 特征交叉。

        + Cross网络 利用 Cross 网络替代原来的 Wide 部分。

      + [[DeepFM]] FM+Embedding+MLP

      + [[xDeepFM]] vector-wise 交叉

      + [[Attention]] 机制作用于深度神经网络，将原来的 pooling 改成加权求和或加权平均

        + [[AFM]] 二阶交叉部分引入 [[Attention]] ，后来没有接 MLP

          + 注意力网络：简单全连接层 + softmax 输出层

        + [[DIN]]

          + DICE 激活函数

          + GAUC

          + Adaptive 正则化方法

        + [[DIEN]] 关注序列信息，通过 AUGRU 机制模拟用户兴趣进化的过程。

      + [[DeepMCP]]

      + [[AutoInt]] 特征工程自动化

    + [[强化学习]]

      + [[DNR]]

  + 其他

    + EdgeRec

    + [[可解释性]]

    + 跨域/多模态推荐

    + 冷启动

    + Exploit&Explore

    + 隐私计算：联邦学习+安全多方计算+可信计算

    + [[CTR Bias]]

      + [[Calibration]]



[[ESMM]] CTR 和 CVR 多任务

[[MIMN]]

## Ref

  + [[DeepCTR]]

  + [[EasyRec]]

  + 
