# 多项式时间近似方案

> 原文:[https://www . geesforgeks . org/多项式时间近似方案/](https://www.geeksforgeeks.org/polynomial-time-approximation-scheme/)

[NP 完全问题](https://www.geeksforgeeks.org/np-completeness-set-1/)没有已知的多项式时间解是一个众所周知的事实，这些问题在现实世界中经常出现(比如见[这个](https://www.geeksforgeeks.org/graph-coloring-applications/)、[这个](https://www.geeksforgeeks.org/k-centers-problem-set-1-greedy-approximate-algorithm/)和[这个](https://www.geeksforgeeks.org/set-cover-problem-set-1-greedy-approximate-algorithm/))。所以一定有办法处理它们。我们已经看到了这些问题的近似算法(例如【旅行推销员】的 [2 近似](https://www.geeksforgeeks.org/travelling-salesman-problem-set-2-approximate-using-mst/))。我们能做得更好吗？

**P**olympical**T**ime**A**逼近 **S** cheme (PTAS)是一种近似算法，为用户提供对精度的控制，这是一个理想的特性。这些算法采用一个附加参数ε > 0，并提供一个近似(1 + ε)最小化和(1–ε)最大化的解。例如，考虑一个最小化问题，如果ε是 0.5，那么 PTAS 算法提供的解是 1.5 的近似值。就 n 而言，PTAS 的运行时间必须是多项式的，但是就ε而言，它可以是指数的。

在 PTAS 算法中，多项式的指数会随着ε的减少而急剧增加，例如，如果运行时间为 O(n <sup>(1/ε)！</sup>)这是一个问题。有一个更严格的方案， **F** 完全 **P** 奥运 **T** 时间 **A** 逼近 **S** 化学(FPTAS)。在 FPTAS 中，算法需要在问题大小 n 和 1/ε两者中进行多项式运算。

**示例(0-1 背包问题):**
我们知道 [0-1 背包](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)是 NP 完全的。对此有一个基于 DP 的[伪多项式解](https://www.geeksforgeeks.org/pseudo-polynomial-in-algorithms/)。但是如果输入值很高，那么解就变得不可行，需要近似解。一个近似的解决方案是使用贪婪方法(计算所有物品的每公斤价值，如果每公斤价值小于 W，则先把最高的每公斤价值放在第一位)，但是贪婪方法不是 PTAS，所以我们无法控制准确性。

以下是 0-1 背包问题的 FPTAS 解法:
输入:
T2【W】T3【背包容量】
T5】val【0..n-1] (项目值)
**wt【0..n-1]** (项目重量)

1.  查找最大值项目，即在 val[]中查找最大值。让这个最大值为 maxVal。
2.  计算所有值的调整系数 k

    ```
          k  = (maxVal * ε) / n
    ```

3.  调整所有值，即创建一个值除以 k 的新数组值'[]。

    ```
          val'[i] = floor(val[i] / k)
    ```

4.  运行[基于差压的解决方案](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)以获得减小的值，即，值“[0..n-1]和所有其他参数相同。

根据 n 和ε，上述解决方案在多项式时间内有效。该 FPTAS 提供的解决方案是(1–ε)近似的。这个想法是舍入一些值的最低有效数字，然后它们将由多项式和 1/ε界定。

示例:

```
val[] = {12, 16, 4, 8}
wt[]  = {3, 4, 5, 2}
W = 10
ε = 0.5

maxVal = 16 [maximum value in val[]]
Adjustment factor, k = (16 * 0.5)/4 = 2.0

Now we apply DP based solution on below modified 
instance of problem.

val'[] = {6, 8, 2, 4}  [ val'[i] = floor(val[i]/k) ]
wt[] = {3, 4, 5, 2}
W = 10

```

**解(1–ε)* OPT 如何？**
这里 **OPT** 是最优值。设 **S** 为上述 FPTAS 算法产生的集合，S 的总值为值(S)。我们需要证明这一点

```
       val(S) >= (1 - ε)*OPT 
```

设 **O** 为最优解(总值为 OPT 的解)产生的集合，即 val(O) = OPT。

```
       val(O) - k*val'(O) <= n*k 
       [Because val'[i] = floor(val[i]/k) ] 
```

在动态编程步骤之后，我们得到了一个对于缩放实例
来说是最优的集合，因此必须至少与选择利润较小的集合 O 一样好。由此，我们可以得出结论，

```
      val'(S) >= k . val'(O)
              >= val(O) - nk
              >= OPT - ε * maxVal
              >= OPT - ε * OPT [OPT >= maxVal]
              >= (1 - ε) * OPT 
```

**来源:**
[http://math . MIT . edu/~ GoE mans/18434 s06/backpack-Katherine . pdf](http://math.mit.edu/~goemans/18434S06/knapsack-katherine.pdf)
[https://en . Wikipedia . org/wiki/多项式-时间 _ 近似值 _scheme](https://en.wikipedia.org/wiki/Polynomial-time_approximation_scheme)

本文由 Dheeraj Gupta 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论