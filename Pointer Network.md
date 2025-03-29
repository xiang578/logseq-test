---
tags:
- Algorithm
public: true
categories: 随手记
toc: true
date:
- 2024/06/09
permalink: note/pointer_network
alias:
- Pointer Net
title: Pointer Network
lastMod: 2024-10-05
toc: "true"
---

求解凸包、TSP 等问题有一个特点：输出是输入的子集。由于输入序列就是词表（不定长），无法使用传统的 seq2seq 模型去建模。
<!--more-->
基于对 attention 注意力机制进行修改和简化，得到新的公式：
$u_j^i =v^T \tanh \left(W_1 e_j+W_2 d_i\right) \quad j \in(1, \ldots, n)$
ej 是 encoder 第 j 步输出
di 是 decoder 第 i 步输出
vT，w1，w2 是固定维度的可训练参数
$p\left(C_i \mid C_1, \ldots, C_{i-1}, \mathcal{P}\right) =\operatorname{softmax}\left(u^i\right)$
考虑第 i 步的选择，先分别计算 uij，然后对 ui 求 softmax，最大值对应的 j 是这一步的输出。
![image.png](/assets/image_1715266443443_0.png)
## Ref
[什么是Pointer Network？ - 知乎](https://www.zhihu.com/question/59480186/answer/257145419)
[李宏毅 Pointer Network - YouTube](https://www.youtube.com/watch?v=VdOyqNQ9aww)