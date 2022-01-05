# 伪多项式算法

> 原文:[https://www . geesforgeks . org/伪多项式算法/](https://www.geeksforgeeks.org/pseudo-polynomial-in-algorithms/)

**什么是伪多项式算法？**
伪多项式算法是一种算法，其最坏情况下的时间复杂度是输入数值(而不是输入数量)的多项式。
例如，考虑正数数组中所有元素的计数频率问题。对此的伪多项式时间解决方案是首先找到最大值，然后从 1 迭代到最大值，对于每个值，找到它在数组中的频率。根据输入数组中的最大值，该解决方案需要时间，因此是伪多项式。另一方面，时间复杂度在数组元素个数(不是值)上是多项式的算法被认为是多项式时间算法。

**伪多项式与 NP-完全性**
一些 NP-完全问题有伪多项式时间解。例如 [0-1 背包](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)、[子集和](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)、[划分](https://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)问题的动态规划解都是伪多项式。可以用伪多项式时间算法求解的 NP 完全问题称为弱 NP 完全问题。

**参考:**T2[https://en.wikipedia.org/wiki/Pseudo-polynomial_time](https://en.wikipedia.org/wiki/Pseudo-polynomial_time)

[StackOverflow–什么是伪多项式时间？它和多项式时间有什么不同？(顶部答案)](https://stackoverflow.com/a/19647659/9280098)

本文由 **Dheeraj Gupta** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息