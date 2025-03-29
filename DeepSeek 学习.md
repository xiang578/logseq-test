---
public: true
title: DeepSeek 学习
tags:
date: 2025-02-15
lastMod: 2025-03-12
toc: "true"
---


原始论文
[[DeepSeekMath]] [[2024/04]] 提出GRPO算法和RL统一视角的讨论
[[DeepSeekMoE]] 在tfm的FFN层做了更细粒度的多专家DeepSeekMoE结构。
[[DeepSeek-V2]] 中提出了高效经济的语言模型。结构上主要有两点，
一个是提出了MLA，由于应用旋转矩阵相对位置编码，在MLA中额外采用一定维度的向量单独作为位置信息拼接起来。
另一个是沿用DeepSeekMoE，v2及之后的文章也用到了GRPO。
[[DeepSeek V3]] 依然采用了v2中的MLA和DeepSeekMoE结构，并且采用了多token预测(MTP:multi-token prediction)。此外v3还采用了FP8混合精度训练，介绍了ds的训练框架，甚至对AI硬件供应商(计算硬件和通信硬件)提了一些改进建议。
[[@DeepSeek-V3参数详细计算]]
[[DeepSeek R1]] 力推RL在增强LLM推理能力的作用。在r1中首先介绍了r1-zero，即没有经过SFT直接进行一个大规模强化学习训练，r1-zero展示出强大有趣的推理行为，但也遇到了一些问题比如可读性差、语言混淆等。继而ds提出了r1：在经过RL学习之前，先进行多阶段训练和冷启数据学习，并且进行模型蒸馏来提升小模型的推理能力。
[[@DeepSeek-R1技术笔记 (含图解和技术点介绍)]]
[[@温故而知新之：图解DeepSeek-R1]]
[[LLM  中强化学习讨论]]

DONE [[@LLM强化学习算法演进之路：MC->TD->Q-Learning->DQN->PG->AC->TRPO->PPO->DPO->GRPO]]
DONE  [[@LLM中的强化学习：从RLHF到DPO]]
DONE  [[@DeepSeek中的强化学习：GRPO与RL统一视角]]
DONE [[@【LLM理论】 DPO算法推导——逐步精讲]]
[[LLM的PPO模型]]
[[RFT]]
[[GPPO]]
MTP [[Better & Faster Large Language Models via Multi-token Prediction]]

[[为什么要做MTP]]
[[MTP 损失函数]]
[[MTP 节省内存实现]]
[[为什么 MTP 是 work 的？]] 从两个角度进行了说明MTP向前多预估几个token有助于学习序列中的"关键决策点"。
[[Multi-token prediction loss assigns higher implicit weights to consequential tokens]]
[[DeepSeek MTP]]
[[DeepSeek MTP 模型推理过程]]
[[Deepseek MTP 训练前向推理例子]]
参考文章
[[@Multi-token prediction 多词预测]]
[[@deepseek技术解读(2)-MTP（Multi-Token Prediction）的前世今生]]
DONE  [[@DeepSeek中的Multi-Token Prediction]]
[[@Deepseek-v3技术报告-图的逐步解析-3-不容易看懂的MTP-公式有拼写错误]]
[[LLM 中的 Attention]]
发展历史
2018 [[Multi-Head Attention]]、2019 [[Multi-Query Attention]]、[[Grouped-Query Attention]]、
[[Multi-head Latent Attention]]
[[从GQA视角如何看MLA]]
[[MLA 引入 RoPE]]
[[MLA 将 Q 输入也改为了投影形式]]
[[推理阶段的MLA]]
[[KV Cache]]
[[为什么降低KV Cache的大小如此重要？]]
[分析 GPT 模型自回归生成过程中的 KV Cache 优化技术 - 知乎](https://zhuanlan.zhihu.com/p/668931470)
[大模型推理性能优化之KV Cache解读 - 知乎](https://zhuanlan.zhihu.com/p/630832593)
[为什么加速LLM推断有KV Cache而没有Q Cache？ - 知乎](https://www.zhihu.com/question/653658936)
参考
[[@对deepseek v3中MLA的详细分析（对比MHA的计算量、缓存量、参数量）]]
[[@Deepseek-v3技术报告-图的逐步解析-1-MLA]]
[DeepSeek-V2 高性能推理 (1)：通过矩阵吸收十倍提速 MLA 算子 - 知乎](https://zhuanlan.zhihu.com/p/700214123)
[DeepSeek-V2 MLA KV Cache 真的省了吗？ - 知乎](https://zhuanlan.zhihu.com/p/714761319)
DONE  [[@MHA->MQA->GQA->MLA的演进之路]]
DONE  [[@DeepSeek：KV cache压缩—MLA与FFN的MoE结构]]
DONE [[@缓存与效果的极限拉扯：从MHA、MQA、GQA到MLA]]
[[MoE]]
[[DeepSeekMoE]] 架构
[[@MOE介绍及其LLM方案整理]]
其他
[ai by hand deepseek](https://www.youtube.com/watch?v=idF6TiTGYsE)
