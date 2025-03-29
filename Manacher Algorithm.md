---
alias:
- 回文子串算法
public: true
tags:
- competitive programming
title: Manacher Algorithm
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

将在原串中加入特殊字符,比如`#`组成一个新的字符串,这样可以把所有奇数或偶数的字符串都变成奇数长度的字符串. 例如`abba`可以转化成`$#a#b#b#a`
用一个辅助数组`P[i]`,代表以`S[i]`为中心的最长回文串向左或向右扩展的长度.最后`max(P[i]-1)`为最长回文串的长度
当 mx - i > P[j] 的时候，以S[j]为中心的回文子串包含在以S[id]为中心的回文子串中，由于 i 和 j 对称，以S[i]为中心的回文子串必然包含在以S[id]为中心的回文子串中，所以必有 P[i] = P[j]，见下图。
![](https://media.xiang578.com/manacher-1.png)
当 P[j] > mx - i 的时候，以S[j]为中心的回文子串不完全包含于以S[id]为中心的回文子串中，但是基于对称性可知，下图中两个绿框所包围的部分是相同的，也就是说以S[i]为中心的回文子串，其向右至少会扩张到mx的位置，也就是说 P[i] >= mx - i。至于mx之后的部分是否对称，就只能一个一个匹配了。
![](https://media.xiang578.com/manacher-2.png)
对于 mx <= i 的情况，无法对 P[i]做更多的假设，只能P[i] = 1，然后再去匹配了