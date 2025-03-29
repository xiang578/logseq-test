---
alias:
- miRNN
public: true
date:
- 2024/05/31
permalink: note/alibaba_mirnn
categories: 随手记
tags:
- Alibaba
- ReRank
- IJCA/2018
title: mutual influence RNN
lastMod: 2024-10-05
toc: "true"
---

论文 Globally Optimized Mutual Influence Aware Ranking in E-Commerce Search
<!--more-->
## 背景
淘宝搜索重排场景，如何生成序列最大化 GMV，vi 是价格
$o^*=\arg \max _{o \in O} \sum_{i=1}^N v(i) p(i \mid c(o, i))$
拆解成两个小问题：
问题一：$p(i \mid c(o, i))$ 估计每个商品在 topk列表中成交的概率
问题二：$O^*$ 如何找到最优 topk 序列
## 问题一：通过 RNN 建模前面已选取物品对后面商品成交的影响
通过  `global feature` 建模 context 信息
原始特征 f 是 `local feature`，将 f 在候选集合下进行归一化即成为 `global feature`
$f_g(i) =\frac{f_l(i)-f_{\min }}{f_{\max }-f_{\min }}, f_{\max } =\max _{1 \leq j \leq N} f_l(j), f_{\min } =\min _{1 \leq j \leq N} f_l(j)$
通过 RNN 预估 p
$\begin{aligned} p\left(o_i \mid o_{1, \ldots, i-1}\right) & =\operatorname{sigmoid}\left(W_h h_i+W_c c_i\right) \\ h_i & =\operatorname{RNN}\left(h_{i-1}, f\left(o_i\right)\right) \\ c_i & =\sum_{j=1}^{i-1} \alpha_{i j} h_j\end{aligned}$
## 问题二：RNN + Beam Search 生成序列

