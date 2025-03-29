---
title: GBDT/Loss
public: true
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

流程

[[Gaussian Distribution]]
损失函数 ${(y_i - f(x_i))^2}$
负梯度 ${y_i - f(x_i)}$
初始化 ${\frac {\sum y_i}{m}}$
叶节点估计
[[AdaBoost]]
损失函数 ${e^{-(2y-1)f(x)}, y\in \{1,0\}}$
也可以是 ${e^{-yf(x)}, y\in \{1,-1\}}$
负梯度 ${(2y-1)e^{-(2y-1)f(x)}}$
${g=-(2y-1)e^{-(2y-1)f(x)}}$, ${h=(2y-1)^2e^{-(2y-1)f(x)}=e^{-(2y-1)f(x)}}$
初始化 ${F_0=\frac{1}{2} \log \frac{\sum P(y=1|x)}{\sum P(y=-1|x)}}$
叶节点估计 ${-\frac{g}{h}=\frac{(2y-1)e^{-(2y-1)f(x)}}{e^{-(2y-1)f(x)}}=2y-1}$
[[Bernoulli Distribution]]
gbdt 代码中 ${y\in \{0,1\}}$
logistics Regression 与对数损失函数转化
${y^*=\frac{1}{2}, y^*\in \{0,1\}}$
${e^{yF(x)}+e^{-yF(x)}=e^{F(x)}+e^{-F(x)}, y\in \{-1,1\}}$
${y^*\log p(x)+(1-y^*) \log (1-p(x))=\frac{1+y}{2}\log \frac{e^{F(x)}}{e^{F(x)}+e^{-F(x)}}+\frac{1-y}{2}\log \frac{e^{-F(x)}}{e^{F(x)}+e^{-F(x)}}}$
${=\frac{1+y}{2}\log e^{F(x)}+\frac{1-y}{2}\log e^{-F(x)} +\frac{1+y}{2}\log \frac{1}{e^{F(x)}+e^{-F(x)}}+\frac{1-y}{2}\log \frac{1}{e^{F(x)}+e^{-F(x)}}=yF(x)+\log \frac{1}{e^{F(x)}+e^{-F(x)}}}$
${=\log \frac{e^{yF(x)}}{e^{yF(x)}+e^{-yF(x)}}=\log(1+e^{-2yF(x)})}$
对数损失函数 ${\log(1+e^{-2yf(x)})}, y\in \{-1,1\}, F(x)=\frac{1}{2} \log \frac{P(y=1|x)}{P(y=-1|x)}$
负梯度 ${\frac{2y}{1+e^{2yf(x)}}}$
初始化 ${F_0= \log \frac{\sum P(y=1|x)}{\sum P(y=-1|x)}}$
叶节点估计  ${\frac{\sum_{x_i \in R_{jm}}\tilde{y_i}}{\sum_{x_i \in R_{jm}}|\tilde{y_i}|(2-|\tilde{y_i}|)}}$
single Newton-Raphson
${log(1+e^{-2yf(x)})}$
一阶导数 ${g=-\frac{2y_i}{1+e^{2y_iF_{m-1}(x)}}}$
二阶导数 ${h=\frac{4y_i^2e^{2y_iF_{m-1}(x)}}{(1+e^{2y_iF_{m-1}(x)})^2}}$
${\theta = -\frac{g}{h}=\frac{\tilde{y_i}}{|\tilde{y_i}|(2-|\tilde{y_i}|)}}$
${|\tilde{y_i}|(2-|\tilde{y_i}|)=|\frac{2y_i}{1+e^{2y_iF_{m-1}(x)}}|(2-|\frac{2y_i}{1+e^{2y_iF_{m-1}(x)}}|)=\frac{|2y_i|(2|1+e^{2y_iF_{m-1}(x)}|-|2y_i|)}{(1+e^{2y_iF_{m-1}(x)})^2}=\frac{|4y_i+4y_ie^{2y_iF_{m-1}(x)}|-4y_i^2}{(1+e^{2y_iF_{m-1}(x)})^2}=\frac{4y_i^2e^{2y_iF_{m-1}(x)}}{(1+e^{2y_iF_{m-1}(x)})^2}}$
[[Poisson Distribution]]
概率密度函数：${f(y;\mu)=\frac{\mu ^y}{y!}e^{-\mu }}$
对数似然函数：${l(y;\mu) = \sum^{m}_{i=1} y_i\log \mu_i - \mu_i - \log(y_i!)}$
损失函数：${L(y_i, F(x_i)) = \sum^{m}_{i=1}e^{h_W(x)} - y_i\log (h_W(x_i))}$
负梯度：${ \tilde{y_i} = -[\frac{\partial L(y_i, F(x_i))}{\partial F(x)}]_{F(x)=F_{m-1}(x)} = y_i-e^{F_{m-1}(x_i)}}$
初始化 ${\log(\frac {\sum^{m}_{i=1} y_i}{m})}$
叶节点估计 ${\log(\frac {\sum^{m}_{i=1} \tilde{y_i}}{\sum^{m}_{i=1} e^{F_{m-1}(x_i)}})}$
[[Laplace Distribution]] MAE
损失函数 ${\sum^{m}_{i=1} |y_i-F(x_i)|}$
负梯度 ${ \tilde{y_i} = -[\frac{\partial L(y_i, F(x_i))}{\partial F(x)}]_{F(x)=F_{m-1}(x)} = sign(y_i-F(x_i))}$
初始化 ${median(y)}$
叶节点估计 ${median(\tilde{y_i})}$
MAPE
损失函数 ${\sum^{m}_{i=1} \frac{|y_i-F(x_i)|}{y_i}}$
负梯度 ${ \tilde{y_i} = -[\frac{\partial L(y_i, F(x_i))}{\partial F(x)}]_{F(x)=F_{m-1}(x)} = -\frac{sign(y_i-F(x_i))}{y_i}}$
初始化 ${median_w(y)}$
叶节点估计 ${median_w(\tilde{y_i})}$
证明：
对损失函数求完偏导之后的结果是
${\frac{\partial L(y_i, F(x_i))}{\partial F(x)}= \sum_{\tilde{y_i}<0} - \frac{1}{y_i} +\sum_{\tilde{y_i}>=0} \frac{1}{y_i}}$
叶节点要估计一个值 ${\lambda}$，使损失函数最小，即可以转化为
${\frac{\partial L(y_i, F(x_i)+\lambda)}{\partial F(x)}= \sum_{\tilde{y_i}+\lambda<0} - \frac{1}{y_i} +\sum_{\tilde{y_i+\lambda}\geqslant 0} \frac{1}{y_i}}=0$
对残差进行从小到大排序，找到一个 ${\tilde{y_p}}$ 值，满足
${\sum_{i=0}^{p} - \frac{1}{y_i} \geqslant \frac{1}{2}\sum_{i=0}^{m} \frac{1}{y_i}}$
[[SMAPE]]
解析解不好求，还是直接用 XGB 的二阶泰勒展开方便
损失函数 ${\sum^{m}_{i=1} \frac{|y_i-F(x_i)|}{\frac{y_i + F(x_i)}{2}}}$
负梯度 ${\tilde{y_i} = -[\frac{\partial L(y_i, F(x_i))}{\partial F(x)}]_{F(x)=F_{m-1}(x)} = -\frac{ 4 * y_i * sign(y_i - F(x_i))}{(y_i + F(x_i))^2}}$
Ref
[Generalized Boosted Models:A guide to the gbm package](https://cran.r-project.org/web/packages/gbm/vignettes/gbm.pdf)
