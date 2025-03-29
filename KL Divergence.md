---
title: KL Divergence
public: true
tags:
  - Mathematics
alias:
  - Kullback-Leibler Divergence
  - 相对熵
  - relative entropy
deck: being
date: 2024-10-05
updated: 2025-03-09
toc: true
mathjax: true
---

作用：衡量 {{c1 两个分布之间的距离}}
为什么不对称 :-> 计算两个分布之间的不同，从分布 A 的角度看分布 B 的相似程度
特点

  + 1．非负性：:<->  $\mathrm{KL}(\mathrm{P} \| \mathrm{Q}) \geq 0$
  + 2．非对称性 :<-> $K L(P \| Q) \neq K L(Q \| P)$
  + 3．当且仅当 $P=Q$ 时 :<-> $K L(P \| Q)=0$
一个分布相比于另外一个分布的信息损失。

$$D_{K L}(A \| B)=\sum_{i} P_{A}\left(x_{i}\right) \log \left(\frac{P_{A}\left(x_{i}\right)}{P_{B}\left(x_{i}\right)}\right)=\sum_{i} P_{A}\left(x_{i}\right) \log \left(P_{A}\left(x_{i}\right)\right)-P_{A}\left(x_{i}\right) \log \left(P_{B}\left(x_{i}\right)\right)$$
A和B的交叉熵 = A与B的KL散度 - A的熵。

  + ${D_{K L}(A \| B)=H(A, B)-H(A)}$
机器学习模型学到的分布和真实数据的分布越接近越好，但是现实中只能让模型学到的分布和训练数据的分布尽量相同，即 KL 散度最小。
  + 熵 H(A) 是不依赖 B 的常数，固定 A，根据上面的公式最小化 KL 相当于最小化 H(A, B)。

  + 由于训练数据是固定的，H(A) 不变。

  + 如果 A 是固定的，关于 B 的优化 KL 散度等于优化交叉熵。

P 真实样本的分布，Q模型预测样本的分布，如果 Q 越接近 P，散度就越小。散度的值非负。
  + P 是未知分布，Q 是已知分布

  + $D(p \| q)=\sum_{x} p(x) \log \frac{p(x)}{q(x)}=E_{p(x)}\left(\log \frac{p(x)}{q(x)}\right)$
[[@百面机器学习]]

  + KL 距离不是真正的距离，不满足 {{c1 三角形不等式}} 和 {{c1 交换律}}
[KL散度理解 - 知乎](https://zhuanlan.zhihu.com/p/39682125)

  + 如何证明 KL 散度大于等于 0 #card
    + $\begin{aligned} \mathrm{KL}(P \| Q) & =\int P(x) \ln \frac{P(x)}{Q(x)} d x \\ & =-\int P(x) \ln \frac{Q(x)}{P(x)} d x \\ & \geq-\int P(x)\left(\frac{Q(x)}{P(x)}-1\right) d x \\ & =-\int Q(x)-P(x) d x \\ & =0\end{aligned}$

    + 推导中第三行利用不等式 $ln(x) \le x-1$

    + 最后一行 $Q(x)$ 和 $P(x)$ 都是概率密度函数，所以积分值都等于1

  + 最小化 Kullback-Leibler 散度等价于最大化似然函数
