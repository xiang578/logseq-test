---
title: LSTM
deck: being/machine_learning/LSTM
public: true
tags:
  - Algorithm
date: 2024-10-05
updated: 2025-03-20
toc: true
mathjax: true
---

结构

  + 遗忘门 forget gate :<-> $\Gamma_f^{\langle t\rangle}=\sigma\left(W_f\left[a^{\langle t-1\rangle}, x^{\langle t\rangle}\right]+b_f\right)$
    + 取值范围在 0 到 1

    + 功能 :-> 控制上一个 `cell` 的状态 $c^{t-1}$，有多少信息进入当前状态 $c^{t}$
  + 更新门 update gate :<->  $\Gamma_u^{\langle t\rangle}=\sigma\left(W_u\left[a^{\langle t-1\rangle}, x^{\langle t\rangle}\right]+b_u\right)$
    + 功能 :-> 控制输入 $x$，有多少信息进入当前状态 $c^{t}$
  + $\tilde{c}^{(t)}$ :-> $\tilde{c}^{(t)}=\tanh \left(W_C\left[a^{\langle t-1\rangle}, x^{\langle t\rangle}\right]+b_C\right)$
  + $c^{\langle t\rangle}=\Gamma_f^{\langle t\rangle} \circ c^{(t-1\rangle}+\Gamma_u^{\langle t\rangle} \circ \tilde{c}^{\langle t\rangle}$
  + 输出门 output gate :<->  $\Gamma_o^{(t)}=\sigma\left(W_o\left[a^{\langle t-1\rangle}, x^{\langle t\rangle}\right]+b_o\right)$
    + 作用 :-> 控制当前状态 $c^{t}$ 有多少信息进入 `cell` 的输出
  + 新的 $a^{\langle t\rangle}$ 计算方式:-> $a^{\langle t\rangle}=\Gamma_o^{\langle t\rangle} \circ \tanh \left(c^{\langle t \rangle}\right)$
![image.png](/assets/image_1723990419974_0.png)
occlusion:: eyIuLi9hc3NldHMvaW1hZ2VfMTcyMzk5MDQxOTk3NF8wLnBuZyI6eyJjb25maWciOnsiaGlkZUFsbFRlc3RPbmUiOnRydWV9LCJlbGVtZW50cyI6W3sibGVmdCI6MzQwLjM5MDM4Mjc3MTYxMjA1LCJ0b3AiOjUxMS4yNzA4NDgyMjA0NTgsIndpZHRoIjoxMjYuNjQzNDg4NDM3ODk3MDIsImhlaWdodCI6NjAuMDcwNzg4OTk5NzMzMzk1LCJhbmdsZSI6MCwiY0lkIjoxfSx7ImxlZnQiOjY5Mi40NDI4NTY5OTEyMDIsInRvcCI6NTE3LjU3MDYzMjMyMDcxMzgsIndpZHRoIjoxMjcuNDkxNDkxMTY5MTE0NDEsImhlaWdodCI6NDQuOTcyNzM1NDkzOTk5MzksImFuZ2xlIjowLCJjSWQiOjV9LHsibGVmdCI6NDc2LjQ4NTUyNjQ2MDQ5OTU2LCJ0b3AiOjUxNi42NjU2NTUyNzI5MSwid2lkdGgiOjEzNC40MzQ1MTUwMDAxMzgwNSwiaGVpZ2h0Ijo1MS43Nzk2NjAyMDAwNTE0NywiYW5nbGUiOjAsImNJZCI6Mn0seyJsZWZ0Ijo3OTUuODU2NzMwODU0NTY1NiwidG9wIjoxMzUuNjE0NDIxMjgxNjY2ODYsIndpZHRoIjoxNTUuNjQ4MDYwNDk5MTg2MzksImhlaWdodCI6NjkuMzMzNTA3MjI2MzI1MiwiYW5nbGUiOjAsImNJZCI6M30seyJsZWZ0Ijo1ODEuNzEzNzUzODYzODIxOSwidG9wIjo1MTQuMDExODM4MzkxMzAwOSwid2lkdGgiOjY2LjQ2ODU1MDMyMzY3OTc4LCJoZWlnaHQiOjQ5LjU5MTgzODA0NzYwMzIzLCJhbmdsZSI6MCwiY0lkIjo0fSx7ImxlZnQiOjMwNy4zNzU3NTA1OTQxOTE5LCJ0b3AiOjQzOS45ODU2NzIyMjU1NTMsIndpZHRoIjo4MC4xODAyNjA1ODQ2OTQ5NSwiaGVpZ2h0Ijo1NS4yMzA1MDc5ODE0MzQwNywiYW5nbGUiOjAsImNJZCI6Nn0seyJsZWZ0Ijo0NTguMTE3ODI1NzAyNjgwOTMsInRvcCI6NDUyLjQyNTUwMDc4ODk2NTgsIndpZHRoIjo1MS4xNzc5MjQ4MjcxOTY5OSwiaGVpZ2h0Ijo0Ny44NDAyNDc5OTExNjM4MzUsImFuZ2xlIjowLCJjSWQiOjd9LHsibGVmdCI6NTk1LjIzNDc3NTY4MTMwMzYsInRvcCI6NDQ0Ljg2NzUyNjAzMjg4MzgsIndpZHRoIjo1NC40MjU1MDU2NDk3ODg4NywiaGVpZ2h0Ijo0Ny45NjUyODU2NzE5OTQ3MSwiYW5nbGUiOjAsImNJZCI6OH0seyJsZWZ0Ijo2NjMuOTgyNTIzMzQzNzE2NSwidG9wIjo0NzEuNzA1MDM3MzM3MTMyODYsIndpZHRoIjo2Ni45MTk5OTk5MzU2ODU4NCwiaGVpZ2h0IjozNi43NjQ1MTMyNTIyNzM3OSwiYW5nbGUiOjAsImNJZCI6OX0seyJsZWZ0IjoxNDM0LjY2MTY5OTgzOTU4MDcsInRvcCI6NDMxLjg4MjY3Mjk4MDY2MTgsIndpZHRoIjo1MTAuNDI5MTc2MTI1ODU3MSwiaGVpZ2h0Ijo1ODEuMTI3NTA4NzM2NTQyOCwiYW5nbGUiOjAsImNJZCI6M31dfX0=
使用饱和的非线性函数

  + 为什么 :-> 在输入达到一定值后，输出就不会发生明显变化
  + [[sigmoid]] 阈值 0-1 :-> 模拟开关的关闭程度，用于各种门
    + 现代神经网络中门控的选择

  + [[Tanh]] 阈值 -1 到 1，梯度的阈值为 0~1 :-> 生成记忆
    + 0 中心

    + 输入在 0 附近相比 Sigmoid 函数有更大的梯度

  + 为什么不使用 relu :-> 只能输出大于 0 的部分，前向传播容易发生信息爆炸性增长。


## Ref

  + [[LSTM/Backward]]

  + [[LSTM/Question]]

  + [为什么LSTM没有办法处理等差数列？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/552189862)


