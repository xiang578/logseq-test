---
public: true
title: Problems
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

我的力扣主页： [算法花园](https://leetcode-cn.com/u/ryenxx/)，代码仓库：[xiang578/acm-icpc](https://github.com/xiang578/acm-icpc)

[[2023/07]]

  + [[LC2679. 矩阵中的和]]

[[2023/03]]

  + [[LC1630. 等差子数组]] #[[Brute Force]]

  + [[LC887. 鸡蛋掉落]] #二分搜索 #动态规划 挺好一个题目，刚开始以为是一个简单的二分，然后找了几个小时都没有找到规律。然后想用 dfs 去解，又发现超时。

    + 几年前碰到过类似的题目，求最小满足题目条件的答案。很难直接计算，转化成二分结果+检验结果的方法去求解。

[[2022/01]]

  + [2045. 到达目的地的第二短时间](https://leetcode-cn.com/problems/second-minimum-time-to-reach-destination/)

    + 记录一个第二次访问终点需要经过多少个点

    + 点数确定通过时间和等待时间都能算出来。

  + [2034. 股票价格波动](https://leetcode-cn.com/problems/stock-price-fluctuation/#/) 模拟 + 有限队列

  + [1332. 删除回文子序列](https://leetcode-cn.com/problems/remove-palindromic-subsequences/) 多读几遍题意，每次产出的是子序列而不是子串

    + 刚开始没有仔细读题，还整理了[[Manacher Algorithm]]……

  + [1345. 跳跃游戏](https://leetcode-cn.com/problems/jump-game-iv/) BFS

    + 简单题，写了快半个小时，先想清楚流程再写，不要边写变想。

    + 按 arr[i] 聚合数字，然后每个点只能访问一次，访问后删除。

  + [2029. 石子游戏 IX](https://leetcode-cn.com/problems/stone-game-ix/){{< logseq/mark >}}推荐{{< / logseq/mark >}} 博弈论

    + 找规律，反正是类似于 `1-(1-2)-...` 和 `2-(2-1)-...` 形式

    + 写不出简洁的规律，直接上了模拟……

  + [219. 存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

    + hash

    + 效率更高一些，滑动窗口内 hash

  + [539. 最小时间差](https://leetcode-cn.com/problems/minimum-time-difference/)

    + 按题意模拟，坑点在于时间是一个环，需要考虑左边和右边最近的时间。

  + [1220. 统计元音字母序列的数目](https://leetcode-cn.com/problems/count-vowels-permutation/) 简单 DP

    + 数据忘记初始化导致浪费十多分钟看问题。

  + [382. 链表随机节点](https://leetcode-cn.com/problems/linked-list-random-node/)

    + python `random.randint(st, ed)`

    + 蓄水池抽样：遍历链表，假设当前遍历到第 i 个节点，以 $1/i$ 的概率选择第 i 个节点作为最后的答案。

  + [1716. 计算力扣银行的钱](https://leetcode-cn.com/problems/calculate-money-in-leetcode-bank/) 简单模拟或求等差数列通项公式

  + [373. 查找和最小的K对数字](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/)

    + 暴力：两个数组最多前 1000 个数字组合，然后排序取前 k 个

    + 看题解

      + 使用优先队列，每次取出最小的数字 $(a_i, b_j)$ 后，往队列中 push $(a_{i + 1}, b_j)$ 和 $(a_i, b_{j+})$

  + [334. 递增的三元子序列](https://leetcode-cn.com/problems/increasing-triplet-subsequence/)

    + 第一反应是用最长上升子序列的方法。

    + 仔细想了一下，对一个位置 i 维护之前最小的结果 $$min(nums[0...i-1])$$ 和之后最大的结果$$max(nums[i+1...n-1])$$。如果这三个数不相同，就是一个可行解。

  + [1036. 逃离大迷宫](https://leetcode-cn.com/problems/escape-a-large-maze/) 搜索 + 优化剪枝

    + 19 年就尝试过这题，然后当时暴力写了一个搜索，第一个样例就超时了……

    + 坐标范围是 1e6，所以暴力搜索的空间可能是 1e12。题目关键是 `blocked.length <= 200` 这些 blocked 形成包围圈最大是 100*100？(在一个角上借助两条边围成封闭的正方形)。从起点和终点开始搜索，如果可以访问到超过 1e4 个空间，那么代表没有被包围住。

  + [306. 累加数](https://leetcode-cn.com/problems/additive-number/) DFS

    + 枚举最开始两个数字，然后check之后的数据是否合法。

    + 字符串最长长度等于 35，这个数字会超过 long long 的范围。但是观察一下可以发现 a + b = c 情况下，三个数字的长度不会超过字符串长度的 1/2，大概是 18 位，枚举时一个数字最大18位，这样就不会超出 long long 范围。

    + 反思：没有考虑字符串长度小于 3 的特殊情况

  + [238. 除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self/)

    + 空间复杂度 $O(n)$ 写法：维护后缀乘积结果。

    + 空间复杂度  $O(1)$ 写法：用返回数组保存前 $0...i$ 的乘积，然后逆序用一个变量保存 $i+1..n-1$ 的乘积，然后可以根据这两个信息得到结果。

[[2021/09]]

  + [5847. 找到所有的农场组](https://leetcode-cn.com/problems/find-all-groups-of-farmland/) 暴力，一个格子是不是起点可以通过判断上边格子和左边格子得知。

  + [5848. 树上的操作](https://leetcode-cn.com/problems/operations-on-tree/) 模拟，先想清楚然后再写

  + [5849. 好子集的数目](https://leetcode-cn.com/problems/the-number-of-good-subsets/) 枚举所有合法组合的个数

  + [5866. 数组的最大公因数排序](https://leetcode-cn.com/problems/gcd-sort-of-an-array/) [[并查集]] + [[素数筛]]，有相同因子的数会在同一个集合中。

  + [5865. 访问完所有房间的第一天](https://leetcode-cn.com/problems/first-day-where-you-have-been-in-all-the-rooms/) 漏看一个条件，实际上是傻逼题，还是错了好几次，1e9 相加会爆 int 以及返回答案前也需要取模。

  + [1977. 划分数字的方案数](https://leetcode-cn.com/problems/number-of-ways-to-separate-numbers/) 挺复杂的，写了好几个小时，看题解才过…… n=3500，暗示是 $O(n^2)$ 的算法

    + 设以 nums[i...j] 为结尾的方案数是 $dp_{i,j}$

    + 可以发现 $dp_{i,j}=\sum_{k=2*i-j-1}^{i-1}dp[k][i-1], dp_{i,j+1}=dp_{i,j} + dp_{2*i-j-2,i-1}$，维护一个前缀和。

    + 比较 nums[i...j] 和 nums[2*i-j-1...i-1]  大小，可以先预处理出以 i 和 j 开始的字符串的最大相同长度 lcp[i][j]。

  + [LCP 42. 玩具套圈](https://leetcode-cn.com/problems/vFjcfV/)：r 比较小，可以暴力枚举，被抬一手还是没有写出来。。。需要注意细节。不要提交 debug。

  + [LCP 43. 十字路口的交通](https://leetcode-cn.com/problems/Y1VbOX/)

  + [36. 有效的数独](https://leetcode-cn.com/problems/valid-sudoku/)：判断数独当前局面是否合法。

  + [37. 解数独](https://leetcode-cn.com/problems/sudoku-solver/)：求解数独，上一题的进阶。

[[2021/08]]

  + [[LC5832. 构造元素不等于两相邻元素平均值的数组]] 排序 + 贪心

  + [[LC526. 优美的排列]] DP + 状态压缩

  + [[LC1969. 数组元素的最小非零乘积]] 快速幂

  + [[LC552. 学生出勤记录 II]] DP

  + [5856. 完成任务的最少工作时间段](https://leetcode-cn.com/problems/minimum-number-of-work-sessions-to-finish-the-tasks/)：DP + 子集合枚举

  + [5857. 不同的好子序列数目](https://leetcode-cn.com/problems/number-of-unique-good-subsequences/)：不重复的 01 子序列个数，DP

  + [940. 不同的子序列 II](https://leetcode-cn.com/problems/distinct-subsequences-ii/)：和 5857 类似，字符串包含小写字母

2019 WF

  + [Problem - J - Codeforces](https://codeforces.com/gym/102511/problem/J) 500 个洞，50 个人。a[500][50]，可以将 a[i][j] 用 l 替代，然后对 a[i] 求和，再从小到达排序，得到 i 的名次。问每个 i 最小的排名是多少？
