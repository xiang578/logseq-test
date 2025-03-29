---
url: https://dl.acm.org/doi/10.1145/3534678.3539185
pages: 4041-4049
place: Washington DC USA
library-catalog: DOI.org (Crossref)
authors:
- Mudan Wang
- Huan Yan
- Hongjie Sui
- Fan Zuo
- Yue Liu
- Yong Li
doi: 10.1145/3534678.3539185
tags:
- _tablet
conference-name: KDD '22: The 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining
original-title: Learning to Discover Causes of Traffic Congestion with Limited Labeled Data
links: [Local library](zotero://select/library/items/BRNQFBNS), [Web library](https://www.zotero.org/users/4911197/items/BRNQFBNS)
title: @Learning to Discover Causes of Traffic Congestion with Limited Labeled Data
publisher: ACM
public: true
date:
- 2022/08/14
access-date: 2022-10-12T07:43:44Z
language: en
proceedings-title: Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining
item-type:
- conferencePaper
isbn: 978-1-4503-9385-0
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]] 拥堵成因解释

  + traffic congestion

  + Traffic congestion incurs long delay in travel time, which seriously affects our daily travel experiences. Exploring why traffic congestion occurs is significantly important to effectively address the problem of traffic congestion and improve user experience. 
  + Traditional approaches to mine the congestion causes depend on human efforts, which is time consuming and cost-intensive.

  + Hence, we aim to discover the known and unknown causes of traffic congestion in a systematic way. However, to achieve it, there are three challenges:

    + 1) traffic congestion is affected by several factors with complex spatio-temporal relations;

    + 2) the amount of congestion data with known causes is small due to the limitation of human label;

      + 有拥堵原因的数据很少

    + 3) more unknown congestion causes are unexplored since several factors contribute to traffic congestion.

  + To address above challenges, we design a ^^congestion cause discovery system^^ consisting of two modules:

    + 1) congestion feature extraction, which extracts the important features influencing congestion;

      + 拥堵特征提取

    + 2) congestion cause discovery, which utilize a deep semi-supervised learning based method to discover the causes of traffic congestion with limited labeled causes.

      + 拥堵成因发现

  + Specifically, it first leverages a few labeled data as prior knowledge to pre-train the model. Then, the deep embedded clustering method is performed to produce the clusters under the supervision of the data reconstruction loss and Kullback-Leibler divergence loss.

  + Extensive experiments show that the performance of our proposed method is superior to the baselines. Additionally, our system is deployed and used in the practical production environment at Amap.

[[Attachments]]

  + [Learning to Discover Causes of Traffic Congestion with Limited Labeled Data_2022_Wang.pdf](zotero://select/library/items/WFD7TC8A) {{zotero-linked-file "Learning to Discover Causes of Traffic Congestion with Limited Labeled Data_2022_Wang.pdf"}}
