---
title: SGD
alias:
- 随机梯度下降法
public: true
tags:
- Algorithm
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

每次迭代只采样一个样本
优化 learn-rate，自适应学习率
自适应学习率的方法：对不同的参数使用不同的学习率，参数更新频率和更新步长负相关
[[Annealing]]，全局共享learn_rate 所有的参数以相同的幅度进行更新
随步衰减
指数衰减
1/t衰减
[[AdaGrad]]，参数独立 learn_rate 更新幅度取决于参数本身
$\theta_{t+1}=\theta_t-\frac{\eta}{\sqrt{G_t+\epsilon}} \odot g_t$
$n_t=n_{t-1}+g^2_t$

$\Delta \theta _t = -\frac{\eta}{\sqrt{n_t+\epsilon}}$

计算一个时间区间内的梯度值累积和 [[移动平均]]
AdaDelta 分母滑动区间 + 单位矫正
$E\left[g^2\right]_t=\gamma E\left[g^2\right]_{t-1}+(1-\gamma) g_t^2$
$E\left[\Delta \theta^2\right]_t=\gamma E\left[\Delta \theta^2\right]_{t-1}+(1-\gamma) E\left[\Delta \theta^2\right]_t$
$\Delta \theta_t=-\frac{R M S[\Delta \theta]_{t-1}}{R M S[g]_t} g_t$
[[RMSProp]] 分子滑动区间
`cache =  decay_rate * cache + (1 - decay_rate) * dx**2`

`x += - learning_rate * dx / (sqrt(cache) + eps)`

$E\left[g^2\right]_t=0.9 E\left(g^2\right)_{t-1}+0.1 g_t^2$
$\theta_{t+1}=\theta_t-\frac{\eta}{\sqrt{E\left[g^2\right]_t+\epsilon}}$
[[Adam]] 分子动量版
$v_t=\beta_2 v_{t-1}+\left(1-\beta_2\right) g_t^2$
$m_t=\beta_1 m_{t-1}+\left(1-\beta_1\right) g_t$
$\theta_{t+1}=\theta_t-\frac{\eta}{\sqrt{\hat{v}_t+\epsilon}} \hat{m}_t$
[[AdamW]] 和 [[LazyAdam]]
优化梯度方向，减小震荡
[[Momentum]]：强化相关方向的训练和弱化无关方向的震荡来加速 SGD 收敛
$v_t=\gamma v_{t-1}+\eta \nabla_\theta J(\theta)$
`V[t+1] = rho * v[t] + dx;`

`x[t+1] = x[t] - learningRate * V[t+1]`

Nesterov 梯度加速法
预判前方地形
$v_t=\gamma v_{t-1}+\eta \nabla_\theta J\left(\theta-\gamma v_{t-1}\right)$
梯度下降法 [[SGD]]
并行化，Scalable
Downpour SGD
Hogwild!
