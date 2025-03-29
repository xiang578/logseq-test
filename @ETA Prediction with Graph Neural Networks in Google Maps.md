---
tags:
- Google
- Paper
date:
- 2021/10/26
doi: 10.1145/3459637.3481916
title: @ETA Prediction with Graph Neural Networks in Google Maps
url: http://arxiv.org/abs/2108.11482
authors:
- Peter W. Battaglia
- Luis Perez
- Ang Li
- Petar Veličković
- Zhongwen Xu
- Vishal Gupta
- David Wong
- Austin Derrow-Pinion
- Xueying Guo
- Oliver Lange
- Brett Wiltshire
- Seongjae Lee
- Yujia Li
- Jennifer She
- Marc Nunkesser
- Alvaro Sanchez-Gonzalez
- Todd Hester
links: [Local library](zotero://select/library/items/5AUNTEZW), [Web library](https://www.zotero.org/users/4911197/items/5AUNTEZW)
public: true
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]]

  + Travel-time prediction constitutes a task of high importance in transportation networks, with web mapping services like Google Maps regularly serving vast quantities of travel time queries from users and enterprises alike. Further, such a task requires accounting for complex spatiotemporal interactions (modelling both the topological properties of the road network and anticipating events—such as rush hours—that may occur in the future). Hence, it is an ideal target for graph representation learning at scale. Here we present a graph neural network estimator for estimated time of arrival (ETA) which we have deployed in production at Google Maps. While our main architecture consists of standard GNN building blocks, we further detail the usage of training schedule methods such as MetaGradients in order to make our model robust and production-ready. We also provide prescriptive studies: ablating on various architectural decisions and training regimes, and qualitative analyses on real-world situations where our model provides a competitive edge. Our GNN proved powerful when deployed, significantly reducing negative ETA outcomes in several regions compared to the previous production baseline (40+% in cities like Sydney).

[[Attachments]]

  + [ETA Prediction with Graph Neural Networks in Google Maps_2021_Derrow-Pinion.pdf](zotero://select/library/items/XQ499E9L) {{zotero-linked-file "attachments:ETA Prediction with Graph Neural Networks in Google Maps_2021_Derrow-Pinion.pdf"}}
