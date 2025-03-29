---
file: [PRML Note 前十一章_2023_淡蓝小点.pdf](file:///Users/xry/Documents/syncthing/zotero-lib/PRML Note 前十一章_2023_淡蓝小点.pdf)
public: true
file-path: file:///Users/xry/Documents/syncthing/zotero-lib/PRML Note 前十一章_2023_淡蓝小点.pdf
title: hls__PRML Note 前十一章_2023_淡蓝小点
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

[:span]
ls-type:: annotation
hl-page:: 59
hl-color:: yellow
如果先验和似然相乘得到的后验与先验有相同的函数形式，我们就说该先验是似然的共轭先验，也说后验分布和先验分布是共轭分布。
ls-type:: annotation
hl-page:: 61
hl-color:: yellow
是否共轭看的是后验是否和先验有相同的函数形式。
ls-type:: annotation
hl-page:: 61
hl-color:: yellow
在某些情况下，存在先验、后验、似然三者函数形式均相同的情况。
ls-type:: annotation
hl-page:: 61
hl-color:: green
x服从高斯分布时似然是高斯的，其均值的共轭先验也是高斯的，由共轭先验得到的后验也是高斯的，此时三者的函数形式都相同。
ls-type:: annotation
hl-page:: 61
hl-color:: green
我们说“伯努利分布的共轭先验是Beta 分布”
ls-type:: annotation
hl-page:: 62
hl-color:: green
我们一般不说“伯努利分布参数µ的后验分布和Beta共轭”
ls-type:: annotation
hl-page:: 62
hl-color:: green
我们倒是可以说“由Beta分布导致的伯努利分布参数µ的后验分布和Beta先验是共轭分布”
ls-type:: annotation
hl-page:: 62
hl-color:: green
ls-type:: annotation
hl-page:: 62
hl-color:: yellow
ls-type:: annotation
hl-page:: 62
hl-color:: yellow
理论上，我们应该从问题的实际出发，为参数引入最合理的先验，也就是我们应该从建模的合理性而不是从计算的方便性和可解释性出发选择先验。
ls-type:: annotation
hl-page:: 62
hl-color:: yellow
2-006
ls-type:: annotation
hl-page:: 62
hl-color:: purple
2-007
ls-type:: annotation
hl-page:: 63
hl-color:: purple
2-008
ls-type:: annotation
hl-page:: 63
hl-color:: purple
随着试验次数的增加，后验分布的不确定性会越来越小？
ls-type:: annotation
hl-page:: 63
hl-color:: yellow
随着试验次数的增加（数据集的变大），未知参数的取值越来越集中？
ls-type:: annotation
hl-page:: 63
hl-color:: yellow
答案是：在一般情况下，理论上的确有这样的趋势，但对于某些特定的数据集则不一定。
ls-type:: annotation
hl-page:: 63
hl-color:: yellow
在考虑了全部的数据集后，后验方差的均值总是小于等于先验方差。
ls-type:: annotation
hl-page:: 65
hl-color:: yellow
[:span]
ls-type:: annotation
hl-page:: 67
hl-color:: yellow