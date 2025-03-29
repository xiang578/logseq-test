---
public: true
tags:
- 时间序列预测
- Time Series Transformer
title: Transformer 是否适合时间序列预测
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[Transformer是否真的适合解决时序预测问题 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/452528235)
[[Autoformer]]
一类方法是否适用于某个问题，主要取决于两者的[[归纳偏置]]是否相匹配
标准 Transformer 实现的是点到点的特征融合，这种离散的方式其实是忽略了时间序列连续性。
基于自相关理论将 Transformer 扩展到序列到序列的特征融合
[[MTGNN]]
[[TPA-LSTM]]
[Transformer是否适合用于做非NLP领域的时间序列预测问题？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/493821601) [[2023/03/05]]
吴海旭
一类方法是否适用于某个问题，主要取决于两者的[[归纳偏置]]是否相匹配

RNN
对序列依赖马尔可夫假设
序列维度参数共享，天然可以处理变长数据
Transfomr
注意力机制处理变长数据
点点时序链接建模长期依赖
线性模型
不具备处理变长数据的能力
模型参数量随着长度增加而增加
[[@Non-stationary Transformers: Exploring the Stationarity in Time Series Forecasting]] 非平稳时间序列预测
科研汪老徐 [[@Are Transformers Effective for Time Series Forecasting?]] transformer 类方法短时预测效果差，所以强调长时预测，然后对比的 baseline 是自回归模型，由于错误累积，长时预测效果差。
**我们不相信如果一个模型对短时预测都做不好，对长时预测却得心应手**，毕竟这两个问题都是从同一段历史数据里提取时序特征来做的预测。
此外，我们也并不认为时序预测这个问题有必要考虑变长数据，也因此应该使用Transformer这类支持对变长数据进行建模的架构。反过来想一下，如果一个模型能同时处理各种长度的历史数据，至少说明这些不同长度之间的时序信息在建模过程中是丢失的。
SCINet CNN 提取时序特征
self-attention 机制上是 anti-ordering 的，与时间序列建模的目的恰好是矛盾的。
[[Informer]] 从实验结果来看，原生Informer的效果最差，原因也很简单，raw data除了大小没有什么时序的语义信息，对原始数据通过self-attention提取点对点的所谓correlation毫无意义。Informer中真正起了点儿作用的是对时间直接做些编码的部分，不过也作用有限。
[[PatchTST]] 我们一直质疑的是attention对于提取时序信息的意义，文中的Patch内部使用linear来提取feature，这部分跟我们的做法类似。直觉上来讲，学习不同patch之间的关系对大多数时间序列意义不大，可以做个ablation study看看attention是否真的起到了作用，i.e.，跟去掉attention后的两层Linear结构比较一下。此外，文中缺省使用了RIN来降低distribution shift带来的影响，跟NLinear的结果比较会相对合理一些。
RIN 对抗distribution shift的normalization方法 [[@Reversible Instance Normalization for Accurate Time-Series Forecasting against Distribution Shift]]
[的泼墨佛给克呢 - 知乎 (zhihu.com)](https://www.zhihu.com/people/ddz-73)
是真的，informer设计了一大堆花里胡哨的，看起来很有道理，实际上用起来真的不太行。而且我发现，他们这些transformer的模型，在ETT数据集(只有7个变量)上，d_model设置为512，都快赶上nlp领域常设的768了，这也太离谱了。按理说，只有7个变量，用这么大的模型(虽然层数较少)太扯了
而且那个pyraformer是真的没啥特别突出的地方，不知道咋能中oral。。。我做过实验，就是在输出的时候把变量维度和时间维度统一拼接经过线性层，这样确实能效果好，我觉得他的效果有提升就是因为这个，但这样得到的线性层是非常非常大的，参数甚至比transformer本身都多，不知道有啥意义。。。最近他的代码开源了，可以看看他是怎么实现的
