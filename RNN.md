---
title: RNN
deck: being/deep_learning/RNN
public: true
tags:
- Algorithm
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

![image.png](/assets/image_1727101408189_0.png)
occlusion:: eyIuLi9hc3NldHMvaW1hZ2VfMTcyNzEwMTQwODE4OV8wLnBuZyI6eyJjb25maWciOnsiaGlkZUFsbFRlc3RPbmUiOnRydWV9LCJlbGVtZW50cyI6W3sibGVmdCI6MTU0NC4wNzUyNzMzNjA3MzQ0LCJ0b3AiOjUwMC42NTQzNTc4NTAwMzkxLCJ3aWR0aCI6NzIyLjE0MDMwMTkxMDIxMzEsImhlaWdodCI6MTA3LjMwMjU3NDYzMDExODY3LCJhbmdsZSI6MCwiY0lkIjoxfSx7ImxlZnQiOjE0NjUuNTcxNzQ2MTMzNjQ4NSwidG9wIjo2MTYuNjU1MTg4MjQ2MjkxNiwid2lkdGgiOjU1OS4xNDU3NzEwOTM3ODQ2LCJoZWlnaHQiOjk5LjMwMzA3NjczMDE3ODMsImFuZ2xlIjowLCJjSWQiOjJ9LHsibGVmdCI6NzAzLjQ4OTk5OTUyMTU3MjgsInRvcCI6Mzk2LjI5NzA3MzY4NDQxODI1LCJ3aWR0aCI6ODIuMDIwNTAzNjg3MzcxODQsImhlaWdodCI6NzEuNTY1NDQ4ODQ0OTE0MjMsImFuZ2xlIjowLCJjSWQiOjN9LHsibGVmdCI6ODI1LjUzMjQzMjk1ODM4MTMsInRvcCI6MTMxLjk4MTg1NjMyMTg0MjEsIndpZHRoIjoxNDcuODE2MDUxNjczNjU5MSwiaGVpZ2h0Ijo3MC44MDQyOTIyNzcyMjA3LCJhbmdsZSI6MCwiY0lkIjoyfV19fQ==
$h_{t}=\tanh \left(W x_{t}+U h_{t-1}+b\right)$
  + $\frac{d h_{t}}{d \theta}=\frac{\partial h_{t}}{\partial h_{t-1}} \frac{d h_{t-1}}{d \theta}+\frac{\partial h_{t}}{\partial \theta}$
    + $|\frac{\partial h_{t}}{\partial h_{t-1}}| >1$，导致 :<-> 梯度爆炸
      + 如何解决 :-> 梯度裁剪
    + $|\frac{\partial h_{t}}{\partial h_{t-1}}| < 1$，导致 :<-> 梯度消失
$\frac{\partial h_{t}}{\partial h_{t-1}}=\left(1-h_{t}^{2}\right) U$
  + 结合 $h_{t}=\tanh \left(W x_{t}+U h_{t-1}+b\right)$
 对应的曲线

  + 如果 U 很大，ht 会接近于 1，$$\frac{\partial h_{t}}{\partial h_{t-1}}$$ 反而会小
  + 为什么隐状态激活函数使用 [[Tanh]] 而不是 [[ReLU]]？
    + 为什么用 Tanh :-> $\frac{\partial h_{t}}{\partial h_{t-1}}$ 是有界的，可以缓减梯度爆炸的风险。
    + 为什么不用 ReLU  :-> 正半区没有上限
      + 将 U 初始化在单位矩阵附近 + 梯度裁剪也可以得到不错的效果

[[RNN/Backward]]

[[Ref]]

  + [[RNN/Question]]

  + [[LSTM]]

  + [[GRU]]

  + [6_RNN](http://www.huaxiaozhuan.com/%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0/chapters/6_RNN.html)

  + [也来谈谈RNN的梯度消失/爆炸问题 - 科学空间|Scientific Spaces](https://spaces.ac.cn/archives/7888/comment-page-1)
