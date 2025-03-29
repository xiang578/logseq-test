---
title: Seq2Seq
tags:
- Algorithm
public: true
date: 2024-10-05
lastMod: 2025-03-23
toc: "true"
---

TODO [[Sequence to Sequence Learning with Neural Networks]]
[[Massive Exploration of Neural Machine Translation Architectures]]
TODO [google/seq2seq: A general-purpose encoder-decoder framework for Tensorflow](https://github.com/google/seq2seq)
Encoder - Decoder

Decoder
decoder 涉及输入是正确的单词还是预测的单词
Free Running :-> 使用 Decoder 上一步的预测结果作为当前步的输入
错误累积 :-> 每次输入预测单词，某个单词预测错，后面会跟着错，模型很难收敛
[[Teacher Forcing]] :-> 使用目标文本的“标准答案”作为Decoder的输入
缺点 #card
每次输入正确单词，会导致 overcorrect
exposure bias 误差爆炸/曝光误差 (训练环节和预测环节存在行为差异)
Scheduled sampling 计划采样 #card
1-p 的概率用 teacher forcing
以一定概率随机选择用模型输出还是用真值，选择概率随着训练的推进不断调整
[[Beam Search]] 每一步，多选几个作为候选，最后综合考虑，选出最优的组合。
[[Transformer]] 不适用 RNN
CNN Seq2Seq  [[Convolutional Sequence to Sequence Learning]]