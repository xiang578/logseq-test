---
public: true
deck: being/ML/Optimization
title: Optimization/Question
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

不等式约束优化问题中局部最小值的必要条件是什么？

  + $\mu_{1} \geq 0, \quad \mu_{2} \geq 0$


  + $\nabla f\left(x^{*}\right)+\mu_{1} \nabla g_{1}\left(x^{*}\right)+\mu_{2} \nabla g_{2}\left(x^{*}\right)=0$


  + $\mu_{1} g_{1}\left(x^{*}\right)+\mu_{2} g_{2}\left(x^{*}\right)=0$


是否所有的优化问题都可以转化为对偶问题？ #[[incremental]]
  + 

为什么深度学习不用二阶优化 #card
  + 计算复杂度，二阶导数计算是平方复杂度

  + 小批量的情况下，牛顿法对与二阶导数的估计噪音太大

梯度下降找到的一定是下降最快的方法？ #card
  + 梯度目标函数在当前点的切平面上函数值变化最快的方向

对所有优化问题来说，有没有可能找到比现在已知算法更好的算法？ #card
  + 没有免费的午餐定理


