---
title: Beam Search
public: true
tags:
- Algorithm
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[[NLP]] 中比较常用
参数 B 控制 beam width
翻译任务中：第一次选取概率最高的 B 个词语。第二次在这 B 个词语上进行扩展下一个单词，然后选取概率最高的 B 个词组，以此类推，直到结束。B=1 时相当于贪心。
![image.png](/assets/image_1689661944807_0.png)
在 [[Seq2Seq]] 中应用在 decode 部分
[[Transformer]] 解决实际预测环节如何构造一个理想输出
[[Ref]]
[Seq2Seq中的beam search算法 - 知乎](https://zhuanlan.zhihu.com/p/36029811?group_id=972420376412762112)
[seq2seq 中的 beam search 算法过程是怎样的？ - 知乎](https://www.zhihu.com/question/54356960)