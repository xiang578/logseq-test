---
title: 区间 DP
public: true
tags:
  - Competitive Programming
  - Dynamic Programming
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

$dp[i][j]=max(dp[i][j], dp[i][k]+dp[k+1][j]+cost[i][j])$

从小到大枚举区间的长度

确定 i,j，枚举中间的点，由于先枚举的长度，i和j之间更小的区间都已经被计算过。
