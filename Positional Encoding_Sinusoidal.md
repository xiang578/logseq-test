---
public: true
title: Positional Encoding/Sinusoidal
tags:
date: 2025-03-29
lastMod: 2025-03-29
toc: true
mathjax: true
---

公式
$P E_{(p o s, 2 i)} =\sin \left(\operatorname{pos} / 10000^{2 i / d_{\text { model }}}\right)$
$P E_{(\text { pos, }, 2 i+1)} =\cos \left(\text { pos } / 10000^{2 i / d_{\text { model }}}\right)$
pos 代表位置编号，i 代表维度。不同维度对应不同波长的曲线，波长从 2pi 到 2000pi。选择这个看起来不是很直观的公式，主要是利用三角函数的特性实现 $PE_{pos}$ 线性表示 $PE_{pos+k}$。
波长比较长时，相邻字的位置编码之间的差异比较小
不同维度上应该用不同的函数表示位置编码
三角函数的周期性表示相对位置信息。位置 $$\alpha + \beta$$ 的向量可以表示成位置 $$\alpha$$ 和位置 $$\beta$$ 的组合
$P E(\text { pos }+k, 2 i)=P E(\text { pos, } 2 i) \times P E(k, 2 i+1)+P E(p o s, 2 i+1) \times P E(k, 2 i)$
$P E(\text { pos }+k, 2 i+1)=P E(\text { pos, } 2 i+1) \times P E(k, 2 i+1)-P E(p o s, 2 i) \times P E(k, 2 i)$
实现表达 relative position 的可能
使用sin+cos后，还需要有正向和反向吗？
为什么公式中有一个魔法值 10000？#card
2i = d_model = 512，周期为 2pi*10000
确保循环周期足够大，以便编码足够长的文本。