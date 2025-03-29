---
title: XGBoost/Loss
public: true
deck: being/machine_learning/XGBoost
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

训练损失

正则化损失包括 #card
  + 叶子节点个数 + 叶子节点权重的 L2 正则化
为什么不用更高阶的正则约束 #card
card-last-score:: 5
card-repeats:: 1
card-next-schedule:: 2023-08-26T01:53:50.014Z
card-last-interval:: 4
  + 计算复杂度增加

  + 欠拟合

目标函数分裂推导

  + 优化目标、损失函数 :-> ${Obj = L = \sum^{n}_{i=1}l(y_i,\hat y_i) }$
    + 第 t 轮迭代目标 :-> ${Obj^{(t)} = \sum^{n}_{i=1}l(y_i,\hat y_i^{t-1} + f_t(x_i))}$
  + 二阶泰勒展开公式 :->  ${f(x+\Delta x) \approx f(x)+f'(x)\Delta x + \frac{1}{2}f''(x)\Delta x^2}$
  + 带入化解：${Obj^{(t)}=\sum^n_{i=1}[l(y_i,\hat y_i^{t-1})+ g_if_t(x_i) + \frac{1}{2} h_i f_t(x_i)^2]}$

    + 树的维度，带入 ${f_t(x_i)=w_j}$：${Obj^{(t)} = \sum^T_{j=1}[ (\sum_{i \in I_j} g_i)w_j + \frac{1}{2} (\sum_{i \in I_j}h_i) w_i^2]}$

    + 设 ${G_j = \sum_{i \in I_j} g_i, H_j = \sum_{i \in I_j}h_i}$，可以得到 ${w_j = -\frac{G_j}{H_j}}$

    + 目标函数化简为 ${Obj^{(t)} = - \frac{1}{2} \sum^T_{j=1} \frac{G_j^2}{H_j}}$

    + 树分裂 ${Gain = \frac{1}{2} [\frac{G_L^2}{H_L} + \frac{G_R^2}{H_R} - \frac{(G_L+G_R)^2}{H_L+H_R}]}$

![image.png](/assets/image_1742390004556_0.png)
occlusion:: eyIuLi9hc3NldHMvaW1hZ2VfMTc0MjM5MDAwNDU1Nl8wLnBuZyI6eyJjb25maWciOnsiaGlkZUFsbFRlc3RPbmUiOnRydWV9LCJlbGVtZW50cyI6W3sibGVmdCI6NTIwLjA5OTAxMDQyMTM3MDQsInRvcCI6NTI4LjgwOTM4MTM3NTUxMSwid2lkdGgiOjc4NC4yMDM5MTU5NzM5MjIyLCJoZWlnaHQiOjc3LjYxODczOTYzNzExNDIzLCJhbmdsZSI6MCwiY0lkIjoxfSx7ImxlZnQiOjUwMy42MDA0ODQyMDQxNjU4NywidG9wIjo2NDMuMzA5Mzk4MTA5MDE3NSwid2lkdGgiOjY1My4xOTk4NzQ3NDE0NjA1LCJoZWlnaHQiOjg0LjYxODczNDU4MDk0NjQ3LCJhbmdsZSI6MCwiY0lkIjoyfSx7ImxlZnQiOjUwNS41OTkyNjM4MzE5ODY4LCJ0b3AiOjc3Ni4zMDkzOTM3NzUxNTk3LCJ3aWR0aCI6NjkzLjIwMjYwODkwODYzNzgsImhlaWdodCI6ODYuNjE4Nzc1NTExODI1NTYsImFuZ2xlIjowLCJjSWQiOjN9LHsibGVmdCI6NTA2LjE5ODI2MDkxNTk1NjE1LCJ0b3AiOjg5OC42MTg3OTEwNDE0ODI2LCJ3aWR0aCI6NjMyLjAwNDIxNDYxODY3MywiaGVpZ2h0Ijo3NC4wMDAwMDg5MDg0ODU0OCwiYW5nbGUiOjAsImNJZCI6NH0seyJsZWZ0Ijo2MTYuNjAwNDMwODU0NTYyMSwidG9wIjoyMTQuODA5MzYwNjY5MzAxNzgsIndpZHRoIjo0MTUuMTk5OTAxNDE2MjYyNywiaGVpZ2h0Ijo4NS42MTg3MDY0MTA4NzEwMywiYW5nbGUiOjAsImNJZCI6NX1dfX0=
[xgboost如何使用MAE或MAPE作为目标函数? - 知乎](https://zhuanlan.zhihu.com/p/34373008)

  + 利用可导函数逼近 #card
    + mse 在初始误差比较大时，loss 是平方会偏离目标

    + ln(cosh(x))以及 log(exp(-x) + exp(x))进行逼近

    + 利用 huber loss 逼近 mae

      + 使用可导逼近形式 Pseudo-Huber loss function 做为目标函数

        + $$L_{\delta}\left(y_{i}, \tilde{y}_{i}\right)=\delta^{2}\left(\sqrt{1+\left(\frac{\tilde{y}_{i}-y_{i}}{\delta}\right)^{2}}-1\right)$$

```python
def huber_approx_obj(dtrain, preds):
    d = preds -dtrain
    h = 1  #h is delta in the formula
    scale = 1 + (d / h) ** 2
    scale_sqrt = np.sqrt(scale)
    grad = d / scale_sqrt
    hess = 1 / scale / scale_sqrt
    return grad, hess
```

![](https://media.xiang578.com/huber-mae.png)

  + 自定义一个二阶导数值
