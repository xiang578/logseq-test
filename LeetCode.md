---
public: true
title: LeetCode
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

注意事项
统计单词数直接 `int a[300]` 这样可以省去 `- 'a'` 这一步操作。
代码中的 printf 不会影响最后的结果，猜测是去比较返回值。
上一条提到的不会影响结果，但是会影响耗时，所以还是要删除中间的输出。
函数里面定义数组，需要初始化。
`vector<int>v(10, 0)`
`vector<vector<int>> dp(k, vector<int>(1 << n));` 二维 vector
sort 手动传入 cmp 需要是 static 类型
`sort(a.begin(), a.end(), [](vector<int>&x, vector<int>&y){return x[0]<y[0];});`
lambda 里面的参数需要是引用，如果是拷贝构造，在 `n=1e5` 时会超时。
[枚举子集 | CP Wiki](https://cp-wiki.vercel.app/basic/enumerate/#%E6%9E%9A%E4%B8%BE%E5%AD%90%E9%9B%86)  n 个元素的子集枚举 $$O(3^n)$$ 复杂度
枚举 i 的子集
`(j - 1)` 将 j 最右边的 1 变成 0，得到小于 j 最大的一个二进制数
`(j - 1) & i` 保证一定是 i 的子集
```c++
for (int i = 1; i < (1 << n); ++i) {
    for (int j = i; j; j = (j - 1) & i) {
   // ...
    }
}
```
`0x3f3f3f3f` 的十进制是1061109567，是10^9级别的，自身相加不会超过 int 范围，可以 memset 初始化
[[vector]] 取指定位置的迭代器
```c++
vector<int>::iterator it;
it = a.begin()+4;
it = advance(a.begin(), 4);
it = next(a.begin(), 4);
```
位运算的优先级
`a+b^c` 
先算 `a+b`
`?=:` 运算符优先级
`(a[i]^b[k]) + i==0?0:dp[i-1][j]` 
加法优先级大于 `?=:` 
`__builtin_popcount`
统计一个 int 中 1 的个数
二进制表示中最低位
`n & (n - 1)`
该位运算技巧可以直接将 n 二进制表示的最低位 1 移除
`n & (-n)`
该位运算技巧可以直接获取 __n__ 二进制表示的最低位的 1
set、tuple、map 一起使用
```c++
set<tuple<int, int, int>>use;

// 插入元素
use.emplace({1, 2, 3});

// 删除第一个元素
use.erase(use.begin());

//访问
auto p = *use.begin();
int x = std::get<0>(p);
```
复盘
[🐱 第 55 场夜喵双周赛 - 力扣（LeetCode）](https://leetcode-cn.com/circle/discuss/SwtoM2/)
每一道题目还是要掌握最优的解法，似乎自己都是靠运气好，暴力过的题目。
[设计电影租借系统 - 力扣 (LeetCode) 竞赛](https://leetcode-cn.com/contest/biweekly-contest-55/problems/design-movie-rental-system/) 自己使用优先队列 + map
数据结构需要做到有序 + 增删，其实 set 更好，不像自己原来写的那么复杂。
模仿其他人的写，逻辑真的清晰好多
补题
ok
[730. 统计不同回文子序列 - 力扣（LeetCode）](https://leetcode.cn/problems/count-different-palindromic-subsequences/) ^^DP，注意题目中只有 4 个字符^^
DONE [5482. 二维网格图中探测环 - 力扣（LeetCode）](https://leetcode-cn.com/problems/detect-cycles-in-2d-grid/) ^^考虑到特殊条件减少减枝^^
DONE [1687. 从仓库到码头运输箱子 - 力扣（LeetCode）](https://leetcode-cn.com/problems/delivering-boxes-from-storage-to-ports/) 
需要维护之前的状态，然后观察到，每考虑一个新的箱子，需要淘汰非法的状态。
考虑到  n 的大小，状态用优先队列来维护。
DONE [1686. 石子游戏 VI - 力扣（LeetCode）](https://leetcode-cn.com/problems/stone-game-vi/) AB 博弈，取石子，同一个石子两个人得分不同，问谁能赢。^^得分相加，然后贪心去最大^^
DONE [5638. 吃苹果的最大数目 - 力扣（LeetCode）](https://leetcode-cn.com/problems/maximum-number-of-eaten-apples/) 有什么简单的方法 ^^优先队列也没有错到哪里去，用 map 可能会方便一些^^
map 变量是有序的
维护 a[i], d[i]+i，按第二个从大到小排序，贪心，倒推能吃多少苹果
DONE [5640. 与数组中元素的最大异或值 - 力扣（LeetCode）](https://leetcode-cn.com/problems/maximum-xor-with-an-element-from-array/) ^^利用数组的元素建立二叉树，然后查询时在树上遍历^^
^^注意计算内存细节^^
DONE [377. 组合总和 Ⅳ - 力扣（LeetCode）](https://leetcode-cn.com/problems/combination-sum-iv/)  题目给答案做了一个假设小于 int，但是直接 dp 会超过 int，记忆化搜索可以保障计算的都是需要 dp 值。^^题目给 sb 假设，就直接暴力加上这个条件^^
如何 dp ？
[第 214 场周赛 - 力扣（LeetCode）](https://leetcode-cn.com/contest/weekly-contest-214) [[2020/11/08]]
[[2020/11/29]] 周赛补题
DONE [5615. 使数组互补的最少操作次数 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-moves-to-make-array-complementary/)
DONE [5616. 数组的最小偏移量 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimize-deviation-in-array/) 排序和尺取
[[2020/12/06]] 补题
DONE [5619. 最小不兼容性 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-incompatibility/)
TODO [石子游戏 V - 力扣 (LeetCode) 竞赛](https://leetcode-cn.com/contest/weekly-contest-203/problems/stone-game-v/) 这个题目下周之前需要做出来。
[[2020/08/23]] 第一想法背包？500 和 100w。看起来要超时。
晚上躺在床上一想，这是不是应该绝对不能写？爬起来一看题目，又是自己想错了，不是随机将石头分成两堆。看起来只要记忆化搜索就可以了。
TODO [1531. 压缩字符串 II - 力扣（LeetCode）](https://leetcode-cn.com/problems/string-compression-ii/description/)
TODO [5644. 得到子序列的最少操作次数 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-operations-to-make-a-subsequence/)
TODO [146. LRU 缓存机制 - 力扣（LeetCode）](https://leetcode-cn.com/problems/lru-cache/)
TODO [序列中不同最大公约数的数目 - 力扣 (LeetCode) 竞赛](https://leetcode-cn.com/contest/weekly-contest-235/problems/number-of-different-subsequences-gcds/)
TODO [664. 奇怪的打印机 - 力扣（LeetCode）](https://leetcode-cn.com/problems/strange-printer/) 100
DONE [1787. 使所有区间的异或结果为零 - 力扣（LeetCode）](https://leetcode-cn.com/problems/make-the-xor-of-all-segments-equal-to-zero/) 所有长度为 k 的子区间异或为 0，最小需要调整多少个 ^^最后答案是按 k 循环的数组，另外还有一个异或相关的优化。没有找到规律，看到 1024 直接想着按位考虑，不过后来发现太复杂了，也没有优化^^
DONE [5779. 装包裹的最小浪费空间 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-space-wasted-from-packaging/) 如果对最后返回结果取模，答案正确，但是中间过程取模就会出错
[1896. 反转表达式值的最少操作次数 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-cost-to-change-the-final-value-of-expression/)
表达式解析，至少先要考虑表达式怎么解析？
`auto [x, y] = make_pair(a, b)`
[1916. 统计为蚁群构筑房间的不同顺序 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/count-ways-to-build-rooms-in-an-ant-colony/) 以及 [1830. 使字符串有序的最少操作次数 - 力扣（LeetCode）](https://leetcode-cn.com/problems/minimum-number-of-operations-to-make-string-sorted/) [[乘法逆元]]
TODO [[乘法逆元]]
TODO [[费马小定理]]
