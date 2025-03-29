---
public: true
tags:
  - 负采样
title: Word2Vec/Negative Sampling
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

NEG：负向样本太多，选取部分负样本来更新。可以作为 HS 的一种替代。
  + 词在集合中的频率，带权采样

    + 权重计算 :-> $\operatorname{len}(w)=\frac{\operatorname{count}(w)}{\sum_{u \in \operatorname{vocab}} \operatorname{count}(u)}$
    + 权重计算经验值 :-> $\operatorname{len}(w)=\frac{\operatorname{count}(w)^{3 / 4}}{\sum_{u \in \text {vocab}} \operatorname{count}(u)^{3 / 4}}$
  + 具体采样实现 #card
    + 负采样概率*1亿=单词在表中出现的次数。

    + 生成 0-1亿范围内的一个随机数，然后上面对应的序号

负采样的目标函数是一个经验公式。

$$E=-\log \sigma\left(\overrightarrow{\mathbf{w}}^{\prime}_{w_{O}} \cdot \overrightarrow{\mathbf{h}}\right)-\sum_{w_{j} \in \mathcal{W}_{n e g}} \log \sigma\left(-\overrightarrow{\mathbf{w}}^{\prime}_{w_{j}} \cdot \overrightarrow{\mathbf{h}}\right)$$

$\overrightarrow{\mathbf{w}}^{\prime}_{w_{O}}$：为真实的输出单词对应的输出向量

$\overrightarrow{\mathbf{w}}^{\prime}_{w_{j}}$`：为负采样的单词对应的输出向量

作用：

  + 1. 加快模型计算

  + 2. 保证了模型训练的效果，其一模型每次只需要更新采样的词的权重，不用更新所有的权重，那样会很慢，其二中心词其实只跟它周围的词有关系，位置离着很远的词没有关系，也没必要同时训练更新。
