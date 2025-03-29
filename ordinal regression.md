---
public: true
alias:
- 序数回归
title: ordinal regression
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---


五分类例子
模型输出 z 后经过 sigmoid $f(z)=\frac{1}{1+exp(-z)} \in (0, 1.0)$

五分类相当于在 fz 的空间上找到 4 个切分点，用 $P\left(x<\theta_{1}\right), P\left(\theta_{1}<x<\theta_{2}\right), P\left(\theta_{2}<x<\theta_{3}\right), P\left(\theta_{3}<x<\theta_{4}\right), P\left(\theta_{4}<x<+\infty\right)$ 表示 x分别属于 5 个级的概率
```python
class OrdinalRegressionLoss(nn.Module):

    def __init__(self, num_class, train_cutpoints=False, scale=20.0):
        super().__init__()
        self.num_classes = num_class
        num_cutpoints = self.num_classes - 1
        self.cutpoints = torch.arange(num_cutpoints).float()*scale/(num_class-2) - scale / 2
        self.cutpoints = nn.Parameter(self.cutpoints)
        if not train_cutpoints:
            self.cutpoints.requires_grad_(False)

    def forward(self, pred, label):
        sigmoids = torch.sigmoid(self.cutpoints - pred)
        link_mat = sigmoids[:, 1:] - sigmoids[:, :-1]
        link_mat = torch.cat((
                sigmoids[:, [0]],
                link_mat,
                (1 - sigmoids[:, [-1]])
            ),
            dim=1
        )

        eps = 1e-15
        likelihoods = torch.clamp(link_mat, eps, 1 - eps)

        neg_log_likelihood = torch.log(likelihoods)
        if label is None:
            loss = 0
        else:
            loss = -torch.gather(neg_log_likelihood, 1, label).mean()
            
        return loss, likelihoods
```
Ref
[处理分级问题的利器Ordinal Regression - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/482153702)