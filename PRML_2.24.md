---
public: true
title: PRML/2.24
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

$\operatorname{var}_\theta[\boldsymbol{\theta}]=\mathbb{E}_{\mathcal{D}}\left[\operatorname{var}_\theta[\boldsymbol{\theta} \mid \mathcal{D}]\right]+\operatorname{var}_{\mathcal{D}}\left[\mathbb{E}_{\boldsymbol{\theta}}[\boldsymbol{\theta} \mid \mathcal{D}]\right]$
左转根据方差定义拆开

  + $\operatorname{var}_\theta[\boldsymbol{\theta}]=\mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2\right]-\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta}]$

要证明 $\mathrm{E}_D\left[\operatorname{var}_{\boldsymbol{\theta}}[\boldsymbol{\theta} \mid \boldsymbol{D}]\right]+\operatorname{var}_D\left[\mathrm{E}_{\boldsymbol{\theta}}[\boldsymbol{\theta} \mid \boldsymbol{D}]\right]=\mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2\right]-\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta}]$

  + 左边第一项

    + $\begin{aligned} \mathrm{E}_D\left[\operatorname{var}_\theta[\boldsymbol{\theta} \mid D]\right] & =\int \operatorname{var}_\theta[\boldsymbol{\theta} \mid D] p(D) \mathrm{d} D \\ & =\int\left(\mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2 \mid D\right]-\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta} \mid D]\right) p(D) \mathrm{d} D \\ & =\int \mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2 \mid D\right] p(D) \mathrm{d} D-\int \mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta} \mid D] p(D) \mathrm{d} D \\ & =\iint \boldsymbol{\theta}^2 p(\boldsymbol{\theta} \mid D) \mathrm{d} \boldsymbol{\theta} p(D) \mathrm{d} D-\mathrm{E}_D\left[\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta} \mid D]\right] \\ & =\int \boldsymbol{\theta}^2 p(\boldsymbol{\theta}) \mathrm{d} \boldsymbol{\theta}-\mathrm{E}_D\left[\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta} \mid D]\right] \\ & =\mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2\right]-\mathrm{E}_D\left[\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta} \mid D]\right]\end{aligned}$

  + 左边第二项

    + $\begin{aligned} \operatorname{var}_D\left[\mathrm{E}_\theta[\boldsymbol{\theta} \mid D]\right] & =\mathrm{E}_D\left[\mathrm{E}_\theta^2[\theta \mid D]\right]-\mathrm{E}_D^2\left[\mathrm{E}_\theta[\theta \mid D]\right] \\ & =\mathrm{E}_D\left[\mathrm{E}_\theta^2[\theta \mid D]\right]-\mathrm{E}_\theta^2[\theta]\end{aligned}$

  + 两项相加

    + $\mathrm{E}_D\left[\operatorname{var}_{\boldsymbol{\theta}}[\boldsymbol{\theta} \mid \boldsymbol{D}]\right]+\operatorname{var}_D\left[\mathrm{E}_{\boldsymbol{\theta}}[\boldsymbol{\theta} \mid \boldsymbol{D}]\right]=\mathrm{E}_{\boldsymbol{\theta}}\left[\boldsymbol{\theta}^2\right]-\mathrm{E}_{\boldsymbol{\theta}}^2[\boldsymbol{\theta}]$


