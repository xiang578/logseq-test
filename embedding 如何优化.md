---
public: true
title: embedding 如何优化
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[[@Applying Deep Learning To Airbnb Search]]
Learning rate 默认参数 [[Adam]] 效果不太好，使用 [[LazyAdam]] 在较大 embedding 场景下训练速度更快

[[DIN]] Adam + [[exponential decay]]
learning rate 0,001
decay rate 0.9
[[DIEN]] 没有特别提到优化器
