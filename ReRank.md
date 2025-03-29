---
alias:
- 重排
public: true
categories: 随手记
toc: true
date:
- 2024/05/29
permalink: note/rerank
title: ReRank
tags:
updated: 2024-10-05
toc: true
mathjax: true
---

推荐系统中的一环，考虑上下文信息对推荐结果的影响。

<!--more-->

## 解决三大问题

  + 用户体验

    + 打散

    + 多样性

  + 算法效率

    + 多任务融合

    + 上下文感知

    + 实时性提升

  + 流量调控

    + 保量：流量扶持、生态建设

    + 调权：业务需求、实时干预

## 用户体验

  + ### 打散

    + 对同类目、同作者、相似封面图的 item 进行打散，有效防止用户疲劳和系统过度个性化

    + 打散常用的方法

      + 分桶打散法

        + 不同属性 item 放入不同的桶中，一次从各桶取出 item 即可。

          + 按高中低价格分桶，排序结果价格呈现多样性

        + 简单，效果好。末尾容易扎堆，对原始序列改变大，可能带来指标的下降。

      + 权重分配法

        + 对每一个 item 定义一个分数，计算 $f(x)=\sum_i W_i *$ Count $_i$

          + w 为每个属性的权重，代表打散需求的优先级

          + Count 为同属性 item 已经出现的次数

        + fx 为打散加权分数，从低到高对 item 进行排序，完成打散。

        + 实现简单，充分考虑多种属性的叠加，扩展性强，末尾容易扎堆

      + 滑动窗口

        + 在一个长度可控的滑动窗口内，同属性 item 超过一定次数后，交换出 session。

        + 考虑局部，计算量小，对原序的破坏比较低，最大限度保留相关性，也有末尾扎堆。

  + ### 多样性

    + 评估方法

      + 数据指标分析

        + user 和 item 角度，用户曝光一二级类目数，曝光item同属一个类目的概率

        + 类目、作者、标签多个维度分析

      + 人工评估

    + 发展里程

      + 规则约束

        + 硬规则约束

        + 规则引擎

        + 个性化约束

          + 不同类目、不同时段、不同活跃度用户配置不同

      + 启发式方法：结合多样性和相关性

        + [[MMR]] 最大边缘相关模型

          + [[@The use of MMR, diversity-based reranking for reordering documents and producing summaries]]

        + [[DPP]] 点行列式矩阵

          + [[@Fast Greedy MAP Inference for Determinantal Point Process to Improve Recommendation Diversity]]

        + [[Deep-DPP]] 结合深度神经网络

          + [[@Practical Diversified Recommendations on YouTube with Determinantal Point Processes]]

      + 深度模型，加入上下文感知

## 算法效率

  + ### 多任务融合

    + 精排输出多个任务的分数，在重排阶段融合。

    + 常用方法

      + 人工调权

      + Grid Search

      + 模型法

        + 轻量模型融合多个打分以及其他比较重要的特征

        + point-wise

        + 业务场景的最终指标必须单一，重排模型的监督目标必须是一个单一任务。

      + 强化学习

        + 根据用户在不同状态下的行为，利用强化学习建模状态转移过程，提升业务核心目标。

  + ### 上下文感知

    + context-aware Learning-To-Rank

      + 优化目标

        + $\min \frac{1}{|B|} \sum_{(S, Y) \in B i \in[1, S[]} \sum_{[} \operatorname{Loss}\left(Y_i, \mathrm{~F}_{\mathrm{r}}\left(S_i, \operatorname{Context}(S, i)\right)\right)$

          + S 是曝光的物料序列，Y 是用户对 S 的反馈序列

          + Yi 是对 Si 的反馈

          + Fr 重排模型，预测 Si 被用户交互的概率。

          + Loss 可以是普通的交叉熵损失函数。

        + 如何表达序列中的物料 Si

          + 用户针对 Si 的个性化信息，精排模型打分

          + Si 在整个候选集中的排名、位置信息，刻画Si和邻居之间的相对关系，价格排名，精排序列排名

        + Fr 是能对序列建模的模型

      + 如何生成序列

        + $\underset{S \in \text { Permute }(X)}{\operatorname{argmax}} \sum_{i \in[1, \mid S[]} \operatorname{Utility}\left(S_i, \mathrm{~F}_{\mathrm{n}}\left(S_i, \operatorname{Context}(S, i)\right)\right)$

          + permute 代表排列组合能够生成的所有序列

          + Utility 收益函数，Si 被购买的概率等

        + Greedy Search

          + 每次挑选剩下无聊中带来最大收益的那个。

      + pair-wise 类

        + 构建 pair 对比两个 item 之间的相对关系，仍然忽略全局信息。

          + 正样本好于负样本的概率，利用交叉熵来拟合目标

          + 对比学习loss，hinge loss， [[Triplet Loss]]

        + RankSVM、GBRank、RankNet、

        + LambdaRank

          + RankNet 基础上引入 NDCG 目标

      + [[List Wise]]

        + 直接对序列进行优化，建模 item 序列的整体信息和对比信息

          + 即是使用List-Wise方法得到的候选序列，可以从list维度考虑排序，但在最终得到序列时也是逐个使用贪心方法选择候选item，还是不能做到充分上下文感知以及从整体("长期")收益的序列生成。

          + 通过序列生成方法和强化重排解决。

        + 树模型：lambdaMart

        + RNN

          + 分别利用 rnn+attention 和 pointer-network 来构建 seq2seq 模型

          + 阿里巴巴 [[miRNN]]

          + [[DLCM]]

          + [[seq2slate]]

        + 两段式：PRS

          + PMatch 和 PRank 两个链路，通过两段式结构得到最终输出

        + self-attention：[[PRM]]、setRank

          + self-attention 解决长序列建模问题

        + Exact K

        + 强化学习：京东LIRO、阿里GRN

  + ### 实时性提升

    + 实时性分类

      + 系统响应实时性

        + 用户实时行为捕捉，端上重排

      + 特征实时性

        + 链路数据回收延迟，用户本身行为延迟反馈

      + 模型实时性

        + 在线学习，实时更新模型

    + 在线学习 ODL

      + 延迟反馈


        + 原因：链路数据回收延迟，用户本身行为延迟反馈

        + 解决方法

          + 负例校正法：先标记样本为负样本，真正转化后重新插入正样本。保证模型新鲜度，但假负例对模型有一定副作用。

            + Addressing delayed feedback for continuous training with neural networks in CTR prediction

          + 等待法：一定时间内等待真实的成交转化，没等到就不校正。label 置信度提升，模型新鲜度有折损。

            + [A Feedback Shift Correction in Predicting Conversion Rates under Delayed Feedback (arxiv.org)](https://arxiv.org/pdf/2002.02068)

          + 纠偏法：ES-DFM，对观测转化分布和真实转化分布之间的关系建模，降低假负例的权重和增加真正例的权重，来纠正样本不置信问题。

            + [Delayed Feedback (arxiv.org)](https://arxiv.org/pdf/2012.03245)

      + 数据稳定性

        + 电商 CVR 用户白天浏览点击，晚上下单。cvr 晚上比白天高，需要做修正。

  + ## 端上重排

    + 优点

      + **推荐响应实时性**：不用请求下一页，实现即时更新

      + **行为特征实时性**：端上即时计算，不用回传云端

      + **行为特征丰富度**：负反馈、滚动速度、曝光时长等多种用户行为都可以在模型中使用，基于云端的方式受限于数据传输和存储，一般只会选择点击等关键的用户行为。

    + 引擎

      + TF-lite

      + MNN

      + TNN

    + 基于双塔内积模型的实现方式

      + 服务端一次下发几十个item，包括item的embedding

      + 端上基于本地存储的user静态特征、统计特征，和实时行为特征，实时计算user embedding

      + user和item embedding进行内积计算，对list中未展现的剩余item做重排

      + 下次请求时，将更新后的user特征回传云端，方便云端模型实时更新。

    + 发展进程

      + 端上推理 EdgeRec

      + 端上训练 DCCL

## 流量调控

  + ### 保量：流量扶持、生态建设

    + 规则引擎

      + 冷启动、买卖家结构调整、曝光保量

    + 探索和利用：通过e-greedy、Thompson sampling、UCB等EE类的方法，可以有效探索冷启item，同时利用已有item，保障效率折损最低。

  + ### 调权：业务需求、实时干预

    + 规则引擎

      + 时效性要求高的场景，大促 item 加权

    + 样本加权

      + 命中调权规则的样本，增加其在 loss 中的权重。

      + 实现个性化，对效率折损较低。

      + 适合长期调权场景，大店和大 V

## Ref

  + [[@推荐算法架构4：重排]]

  + [[@互联网大厂推荐算法实战]] 6.2 重排

  + [搜索推荐广告排序艺术-重排序 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/359330317)

  + [搜推广生死判官：重排技术发展 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/699976339)
