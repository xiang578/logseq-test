---
links: [Local library](zotero://select/library/items/TQ8KGFHV), [Web library](https://www.zotero.org/users/4911197/items/TQ8KGFHV)
authors:
  - Xinyu Hu
  - Tanmay Binaykiya
  - Eric Frank
  - Olcay Cirit
tags:
  - Paper
  - 已读
  - 2023
date:
  - 2022/06/05
title: @DeeprETA: An ETA Post-processing System at Scale
public: true
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]]

  + Estimated Time of Arrival (ETA) plays an important role in delivery and ride-hailing platforms. For example, Uber uses ETAs to calculate fares, estimate pickup times, match riders to drivers, plan deliveries, and more.

  + Commonly used route planning algorithms predict an ETA conditioned on the best available route, but such ETA estimates can be unreliable when the actual route taken is not known in advance.

    + route eta 无法解决偏航问题

  + In this paper, we describe an ETA post-processing system in which a deep residual ETA network (DeeprETA) refines naive ETAs produced by a route planning algorithm.

  + Offline experiments and online tests demonstrate that post-processing by DeeprETA significantly improves upon the accuracy of naive ETAs as measured by mean and median absolute error. We further show that post-processing by DeeprETA attains lower error than competitive baseline regression models.

[[Attachments]]

  + [[hls__DeeprETA_2022_Hu]]

  + [DeeprETA_2022_Hu.pdf](zotero://select/library/items/UFP5FZCQ) {{zotero-linked-file "attachments:DeeprETA_2022_Hu.pdf"}}


