---
pages: 10
library-catalog: Zotero
authors:
- Scott M Lundberg
- Su-In Lee
original-title: A Unified Approach to Interpreting Model Predictions
links: [Local library](zotero://select/library/items/6PRXLT8R), [Web library](https://www.zotero.org/users/4911197/items/6PRXLT8R)
title: @A Unified Approach to Interpreting Model Predictions
public: true
alias:
- SHAP
language: en
item-type:
- journalArticle
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[[Abstract]]
Understanding why a model makes a certain prediction can be as crucial as the prediction’s accuracy in many applications. However, the highest accuracy for large modern datasets is often achieved by complex models that even experts struggle to interpret, such as ensemble or deep learning models, creating a tension between accuracy and interpretability. In response, various methods have recently been proposed to help users interpret the predictions of complex models, but it is often unclear how these methods are related and when one method is preferable over another. To address this problem, we present a uniﬁed framework for interpreting predictions, SHAP (SHapley Additive exPlanations). SHAP assigns each feature an importance value for a particular prediction. Its novel components include: (1) the identiﬁcation of a new class of additive feature importance measures, and (2) theoretical results showing there is a unique solution in this class with a set of desirable properties. The new class uniﬁes six existing methods, notable because several recent methods in the class lack the proposed desirable properties. Based on insights from this uniﬁcation, we present new methods that show improved computational performance and/or better consistency with human intuition than previous approaches.
[[Attachments]]
[A Unified Approach to Interpreting Model Predictions_Lundberg.pdf](zotero://select/library/items/A6C4WJ3W) {{zotero-linked-file "A Unified Approach to Interpreting Model Predictions_Lundberg.pdf"}}
$\operatorname{SHAP}_{\text {feature }}(x)=\sum_{\text {set:feature } \in \text { set }}\left[\mid \text { set } \mid \times\left(\begin{array}{c}F \\ \mid \text { set } \mid\end{array}\right)\right]^{-1}\left[\operatorname{Predict}_{\text {set }}(x)-\operatorname{Predict}_{\text {set } \backslash \text { feature }}(x)\right]$
特征 Shap 值
给定当前的一组特征值，特征值对实际预测值与平均预测值之差的贡献就是估计的 Shapley 值。
不是从模型训练中删除特征后的预测值之差
n 个特征对应 $2^n$ 个模型
缺失
在所有特征中采样，预测时使用一个随机值，观察模型输出如何。
引入
预测时使用这个特征的值，模型输出如何。
按不同顺序引入特征，计算边际贡献。
Ref
[高效的ShapValue计算 - TreeShap分析 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/299337859)
[slundberg/shap: A game theoretic approach to explain the output of any machine learning model. (github.com)](https://github.com/slundberg/shap/)