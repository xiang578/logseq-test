---
public: true
tags:
- Algorithm
title: teacher forcing
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

seq2seq使用teacher forcing有一个问题，就是模型训练和预测行为的不一致会导致模型的泛化性能下降
[[Transformer]] 训练阶段使用这种方式，旨在提升序列模型训练稳定性、加速模型收敛。
一次性输入全部目标序列，可以并行的方式一次性输出完整的目标序列，提高训练效率