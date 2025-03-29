---
type: Paper
tags:
- Paper
- Algorithm
public: true
deck: being/FM
alias:
- 因子分解机
title: FM
date: NaN-NaN-NaN
lastMod: NaN-NaN-NaN
toc: "true"
---

自动特征交叉，解决特征稀疏
FM 与其他模型对比
可以模拟二阶多项式核的 [[SVM]]、MF、SVD++
[[SVM]] 训练和预测需要计算核矩阵，核矩阵的复杂度是 N 方
MF 扩展性没有 FM 好，只有 u 和 i 两类特征
与 [[SVM]] 对比
二阶多项式内核 SVM 二元交叉特征 wij 相互独立
fm 参数 nk，svm 参数 nn，更适合大规模稀疏特征，泛化能力更强
核方法需要计算核矩阵
样本 :-> FM 预测和训练样本独立，SVM 和支持向量有关
FM {{c1 在原始形式下}} 进行优化学习，非线性SVM通常需要在 {{c1 对偶形式}} 下进行
交叉项需不需要乘 value ？
eta 放到 xi 和 xj 泛化能力不好
FM 如何加入 index embedding？
对比 FM 和 SVM 有什么区别？
特征角度 :-> 二阶多项式内核 SVM 二元交叉特征 wij 相互独立
， ((6302f9ee-11be-4f7a-9cf9-26400d6d4601))
为什么要用 FTRL 优化 FM #card
FTRL 是 SGD 算法，离线调参，减少线上风险
稀疏特征， 自适应学习率效果最好(特征 i 在 t 轮迭代的学习率不同)

不同特征有不同的学习速度、收敛速度快
[[Ref]]
[深入FFM原理与实践 - 美团技术团队](https://tech.meituan.com/2016/03/03/deep-understanding-of-ffm-principles-and-practices.html)