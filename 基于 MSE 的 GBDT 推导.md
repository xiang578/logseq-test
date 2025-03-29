---
title: "基于 MSE 的 GBDT 推导"
public: true
tags:
date: "2024-10-05"
updated: "2024-10-05"
toc: true
mathjax: true
---

损失函数 MSE $${L(y, F(x))=\frac{1}{2}(y_i - f(x_i))^2}$$

通过调整 $${F(x_1), F(x_2), ..., F(x_n)}$$ 最小化 $${J=\sum_i L(y_i, F(x_i))}$$

将视为 $${F(x_1), F(x_2), ..., F(x_n)}$$ 数字，$${F(x_i)}$$ 当成是参数，并求导

$${ \frac{\partial J}{\partial F(x_i)} = \frac{\partial \sum_i L(y_i, F(x_i))}{\partial F(x_i)} = \frac{\partial L(y_i, F(x_i))}{\partial F(x_i)} = F(x_i)-y_i}$$

残差等于负梯度 $${y_i-F(x_i)=-\frac{\partial J}{\partial F(x_i)}}$$

$${F_{t+1}(x_i)=F_t(x_i)+h(x_i)=F(x_i)+y_i-F(x_i)=F_t(x_i)-1\frac{\partial J}{\partial F(x_i)}}$$

$${\theta ^t = \theta ^{t-1} + \alpha L^\prime(\theta ^{t-1})}$$
