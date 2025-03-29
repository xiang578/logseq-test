---
url: https://openreview.net/forum?id=0EXmFzUn5I
library-catalog: openreview.net
tags:
- ICLR/2022
- Paper
original-title: Pyraformer: Low-Complexity Pyramidal Attention for Long-Range Time Series Modeling and Forecasting
links: [Local library](zotero://select/library/items/35ENHCF5), [Web library](https://www.zotero.org/users/4911197/items/35ENHCF5)
title: @Pyraformer: Low-Complexity Pyramidal Attention for Long-Range Time Series Modeling and Forecasting
public: true
date:
- 2022/03/16
alias:
- Pyraformer
language: en
updated: 2024-10-05
toc: true
mathjax: true
---

[[Abstract]]

  + Accurate prediction of the future given the past based on time series data is of paramount importance, since it opens the door for decision making and risk management ahead of time. In practice, the challenge is to build a flexible but parsimonious model that can capture a wide range of temporal dependencies.

  + In this paper, we propose Pyraformer by exploring the [[multiresolution representation]] of the time series.

    + Specifically, we introduce the [[pyramidal attention module]] (PAM) in which

      + the inter-scale tree structure summarizes features at different resolutions

      + and the intra-scale neighboring connections model the temporal dependencies of different ranges.

    + Under mild conditions, the maximum length of the signal traversing path in Pyraformer is a constant (i.e., $\mathcal O(1)$) with regard to the sequence length $L$, while its time and space complexity scale linearly with $L$.

  + Extensive numerical results show that Pyraformer typically achieves the highest prediction accuracy in both single-step and long-range forecasting tasks with the least amount of time and memory consumption, especially when the sequence is long.

[[Attachments]]

  + [Pyraformer_2022_Liu.pdf](zotero://select/library/items/MRMAD8N8) {{zotero-linked-file "attachments:Pyraformer_2022_Liu.pdf"}}

## [[Summary]]


