# 了解竞争性编程的复杂性

> 原文:[https://www . geeksforgeeks . org/了解竞争编程的复杂性/](https://www.geeksforgeeks.org/knowing-the-complexity-in-competitive-programming/)

前提:[时间复杂度分析](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/)

一般来说，在各种网站上做竞争性编程问题时，面临的最困难的任务是在期望的复杂度下编写代码，否则程序会得到一个 TLE ( **时间限制超过**)。天真的解决方案几乎永远不会被接受。那么如何知道，什么样的复杂性是可以接受的呢？

这个问题的答案与一秒钟内允许执行的操作数量直接相关。目前大部分站点每秒允许 **10 <sup>8</sup> 操作**，只有少数站点仍然允许 10 <sup>7</sup> 操作。在计算出可以执行的操作数量后，通过查看问题中给出的约束来搜索合适的复杂性。

**示例:**
给定数组 A[]和数字 x，检查 A[]中的一对，其和为 x。
其中 N 为:

```
1) 1 <= N <= 103
2) 1 <= N <= 105
3) 1 <= N <= 108

```

**对于情况 1**
使用两个 For 循环的简单解决方案是可行的，因为它为我们提供了 O(N <sup>2</sup> 的复杂性，即使在最坏的情况下，它也将执行 10 <sup>6</sup> 操作，远低于 10 <sup>8</sup> 。当然 O(N)和 O(NlogN)在这种情况下也是可以接受的。

**对于情况 2**
我们要想一个比 O(N <sup>2</sup> 更好的解决方案，因为最坏的情况下，它会执行 10 <sup>10</sup> 操作，就像 N 是 10 <sup>5</sup> 一样。所以这种情况下可以接受的复杂度是 O(NlogN)或者 O(N)，O(nLogn)大约是 10 <sup>6</sup> (10 <sup>5</sup> * ~10)井在 10 <sup>8</sup> 井下作业。

**对于案例 3**
Even O(NlogN)在执行超过 10 <sup>8</sup> 的~10 <sup>9</sup> 操作时给我们 TLE。因此，唯一可接受的解决方案是 O(N ),在最坏的情况下，它将执行 10^8 操作。

给定问题的代码可以在以下网址找到:[https://www . geesforgeks . org/write-a-c-program-a-set-a-n-numbers-and-other-numbers-x-确定是否存在两个元素-in-s-其和正好是-x/](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)