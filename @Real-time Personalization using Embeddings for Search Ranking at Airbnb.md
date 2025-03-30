---
url: "http://dl.acm.org/citation.cfm?doid=3219819.3219885"
pages: "311-320"
library-catalog: "DOI.org (Crossref)"
authors:
  - "Mihajlo Grbovic"
  - "Haibin Cheng"
doi: "10.1145/3219819.3219885"
tags:
  - "Paper"
  - "Airbnb"
  - "KDD/2018"
  - "Algorithm"
conference-name: "the 24th ACM SIGKDD International Conference"
original-title: "Real-time Personalization using Embeddings for Search Ranking at Airbnb"
links: "[Local library](zotero://select/library/items/K4NZD22V), [Web library](https://www.zotero.org/users/4911197/items/K4NZD22V)"
title: "@Real-time Personalization using Embeddings for Search Ranking at Airbnb"
publisher: "ACM Press"
public: true
date: 2018
access-date: "2019-07-23T04:43:37Z"
language: "en"
proceedings-title: "Proceedings of the 24th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining  - KDD '18"
item-type:
  - "conferencePaper"
isbn: "978-1-4503-5552-0"
updated: "2025-03-30"
toc: true
mathjax: true
---

[[Abstract]]

  + Search Ranking and Recommendations are fundamental problems of crucial interest to major Internet companies, including web search engines, content publishing websites and marketplaces. However, despite sharing some common characteristics a one-size-fitsall solution does not exist in this space. Given a large difference in content that needs to be ranked, personalized and recommended, each marketplace has a somewhat unique challenge. Correspondingly, at Airbnb, a short-term rental marketplace, search and recommendation problems are quite unique, being a two-sided marketplace in which one needs to optimize for host and guest preferences, in a world where a user rarely consumes the same item twice and one listing can accept only one guest for a certain set of dates. In this paper we describe Listing and User Embedding techniques we developed and deployed for purposes of Real-time Personalization in Search Ranking and Similar Listing Recommendations, two channels that drive 99% of conversions. The embedding models were specifically tailored for Airbnb marketplace, and are able to capture guest’s short-term and long-term interests, delivering effective home listing recommendations. We conducted rigorous offline testing of the embedding models, followed by successful online tests before fully deploying them into production.

[[Attachments]]

  + [Real-time Personalization using Embeddings for Search Ranking at Airbnb-2018.pdf](zotero://select/library/items/PIUFF78T) 

论文解决问题：

  + 数据稀疏情况下如何进行训练？

    + 稀疏 id 聚类处理

  + 将 user id 和 listing id 聚合成 user type、listing type

  + word2vec 中加入 booked listing 作为 global context

目标函数

![image.png](/assets/image_1692286083236_0.png)

$$\underset{\theta}{\operatorname{argmax}} \sum_{(l, c) \in \mathcal{D}_{p}} \log \frac{1}{1+e^{-\mathbf{v}_{c}^{\prime} \mathbf{v}_{l}}}+\sum_{(l, c) \in \mathcal{D}_{n}} \log \frac{1}{1+e^{\mathbf{v}_{c}^{\prime} \mathbf{v}_{l}}}+\log \frac{1}{1+e^{-\mathbf{v}_{l}^{\prime} \mathbf{v}_{l}}}$$

booked listing 是正样本，所以有一个负号。由于只有一项，所以没有 sigma 符号。

原始负采样是在全体样本中随机选择，业务特殊性，在正样本同一市场的样本中负采样。更好能发现同一市场中内部 listing 的差异。

new listing 通过附近 3 个同类型、相似价格的 listing embedding 进行平均。



word2vec 方法本来是无监督的，通过引入 booked listing 以及 reject 信息传递部分监督信息

利用 booked 数据训练时，文章中提到 user type 和 listing type 要在同一个空间，不知道为什么下面要有两个公式，以及 c 的含义是什么？

$$\underset{\theta}{\operatorname{argmax}} \sum_{\left(u_{t}, c\right) \in \mathcal{D}_{b o o k}} \log \frac{1}{1+e^{-v_{c}^{\prime} v_{u_{t[[}}}}]]+\sum_{\left(u_{t}, c\right) \in \mathcal{D}_{n e g}} \log \frac{1}{1+e^{v_{c}^{\prime} v_{u_{t[[}}}}]]$$

$$\underset{\theta}{\operatorname{argmax}} \sum_{\left(l_{t}, c\right) \in \mathcal{D}_{b o o k}} \log \frac{1}{1+e^{-\mathrm{v}_{c}^{\prime} \mathrm{v}_{l_{t[[}}}}]]+\sum_{\left(l_{t}, c\right) \in \mathcal{D}_{\text {neg}}} \log \frac{1}{1+e^{v_{c}^{\prime} \mathrm{v}_{l_{t[[}}}}]]$$

embedding 之间直接对比需要在相同的向量空间。根据上面的计算可以生成一个特征 UserTypeListingTypeSim。

在如何在实时模型中引入 embedding 特征：根据一些规则收集一些 listing，计算这些 listing embedding 的平均值，再和当前排序的 lisitng 计算一个相似度，做为一个特征放到模型中。

如何评估按上面方法生成的 emb sim 特征重要性？利用 GBDT？

[[冷启动]] listing embeddings

  + 找方圆 10 英里之内的 3 个最相似的 listing，取 listing embedding 的平均

使用 Embedding 方法要考虑的问题：

  + 1. 希望Embedding表达什么，即选择哪一种方式构建语料

  + 2. 如何让Embedding向量学到东西

  + 3. 如何评估向量的效果

  + 4. 线上如何使用
