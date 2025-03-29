---
public: true
title: Informer/Code
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

encoder 输入

  + feature 特征张量 (336,7) + 时间特征张量 (336,4)

decoder 输入

  + feature 特征张量 (336+168,7) + 时间特征张量 (336+168,4)

  + 168 是一次需要预测的长度

Encoder

  + forward

ProbAttention

```python
def forward(self, queries, keys, values, attn_mask):
        import ipdb; ipdb.set_trace()
        B, L_Q, H, D = queries.shape # [32, 336, 8, 64]
        _, L_K, _, _ = keys.shape # [32, 336, 8, 64]

        queries = queries.transpose(2,1) # [32, 8, 336, 64]
        keys = keys.transpose(2,1) # [32, 8, 336, 64]
        values = values.transpose(2,1) # [32, 8, 336, 64]

        U_part = self.factor * np.ceil(np.log(L_K)).astype('int').item() # c*ln(L_k)
        # self.factor=5 and np.log(L_K)=5.82 -> 6
        # so, U_part = 5 * 6 = 30

        u = self.factor * np.ceil(np.log(L_Q)).astype('int').item() # c*ln(L_q)
        # u = 30

        U_part = U_part if U_part<L_K else L_K # 30
        u = u if u<L_Q else L_Q # 30

        scores_top, index = self._prob_QK(queries, keys, sample_k=U_part, n_top=u)
        # 上面这个方法最重要！
        # [32, 8, 30, 336] and [32, 8, 30] 这是8个heads，每个head下都是选择了前30的query tokens（各自选择的）
        # 含义：(1) scores_top, i.e., Q_K是类似原始transformer中的Q*K^T
        #       (2) index, i.e., M_top则是说，是32个序列，每个序列下8个heads，
        #               每个head下M得分靠前的top-30的query的indices（索引）

        # add scale factor
        scale = self.scale or 1./sqrt(D) # 1./sqrt(64) = 1./8 = 0.125
        if scale is not None:
            scores_top = scores_top * scale # Q*K^T/sqrt(D)

        # get the context
        context = self._get_initial_context(values, L_Q)
        # [32, 8, 336, 64]

        # update the context with selected top_k queries
        context, attn = self._update_context(context, values, scores_top, index, L_Q, attn_mask)
        # [32, 8, 336, 64], None (如果attn!=None,那么其shape为：[32, 8, 336, 336])

        import ipdb; ipdb.set_trace()
        return context.transpose(2,1).contiguous(), attn
        # [32, 336, 8, 64]
```

`_get_initial_context`

  + V(B,H,L,E) 求平均变成 V(B,H,E)，然后再复制成和原来大小相同的矩阵

`_update_context`

  + 更新 index 指定 30 个位置的值，其他值是 `_get_initial_context` 初始化的平均结果

`_prob_QK`

```python
def _prob_QK(self, Q, K, sample_k, n_top): # n_top: c*ln(L_q)
        # Q [B, H, L, D]
        B, H, L_K, E = K.shape # torch.Size([32, 8, 336, 64])
        _, _, L_Q, _ = Q.shape # torch.Size([32, 8, 336, 64])

        # calculate the sampled Q_K
        K_expand = K.unsqueeze(-3).expand(B, H, L_Q, L_K, E)
        # [32, 8, 336, 64] -> [32, 8, 1, 336, 64] -> [32, 8, 336, 336, 64]
        # expand之后，K_expand[0][0][0][0] = K_expand[0][0][1][0] 都是64维度的向量了

        index_sample = torch.randint(L_K, (L_Q, sample_k)) # real U = U_part(factor*ln(L_k))*L_q
        # sample_k=30, 这相当于从336里面选择30个
        # index_sample.shape = [336, 30], 
        # L_K是指定最大值(exclusive)，最小值default=0(inclusive), 形状为(L_Q, sample_k)

        K_sample = K_expand[:, :, torch.arange(L_Q).unsqueeze(1), index_sample, :]
        # 起初的K_expand的shape为：[32, 8, 336, 336, 64]
        # :, :, [336, 1], [336, 30], : [why???]
        # K_sample.shape = [32, 8, 336, 30, 64]

        Q_K_sample = torch.matmul(Q.unsqueeze(-2), K_sample.transpose(-2, -1)).squeeze(-2)
        # [32, 8, 336, 1, 64] * [32, 8, 336, 64, 30] -> [32, 8, 336, 1, 30] -> [32, 8, 336, 30]

        # find the Top_k query with sparisty measurement
        M = Q_K_sample.max(-1)[0] - torch.div(Q_K_sample.sum(-1), L_K)
        # 上面这个实现的就是论文中的那个非常nb的关于query的重要度的公式了，Equation (4)
        # M.shape = [32, 8, 336]

        M_top = M.topk(n_top, sorted=False)[1]
        # [0]=values, [1]=indices
        # M_top.shape = [32, 8, 30]，相当于336个queries里面选择了30个top-k query tokens

        # use the reduced Q to calculate Q_K
        Q_reduce = Q[torch.arange(B)[:, None, None], # [32, 1, 1]
                     torch.arange(H)[None, :, None],  # [1, 8, 1]
                     M_top, :] # factor*ln(L_q)
        # 起初Q.shape = [32, 8, 336, 64], reduce之后，就是
        # Q_reduce.shape = [32, 8, 30, 64]

        Q_K = torch.matmul(Q_reduce, K.transpose(-2, -1)) # factor*ln(L_q)*L_k
        # [32, 8, 30, 64] * [32, 8, 64, 336] -> [32, 8, 30, 336]
        # 30个query tokens，和336个key tokens的dot product values

        return Q_K, M_top
        # [32, 8, 30, 336] and [32, 8, 30] 这是8个heads，每个head下都是选择了前30的query tokens（各自选择的）
        # 含义：Q_K是类似原始transformer中的Q*K^T
        #       M_top则是说，是32个序列，每个序列下8个heads，每个head下M得分靠前的top-30的query的indices（索引）
```

## Ref

  + [Informer主要代码解读 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/374936725)

  + [细读经典AAAI2021最佳论文-informer1 主要思想和代码 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/467523291) 讲解很详细
