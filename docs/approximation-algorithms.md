# 近似算法

> 原文:[https://www.geeksforgeeks.org/approximation-algorithms/](https://www.geeksforgeeks.org/approximation-algorithms/)

**概述:**
近似算法是处理优化问题的 [NP 完全性](https://www.geeksforgeeks.org/np-completeness-set-1/)的一种方式。近似算法的目标是在多项式时间内尽可能接近最优解。

[**近似算法**](https://www.geeksforgeeks.org/vertex-cover-problem-set-1-introduction-approximate-algorithm-2/) **:**
的特点在这里，我们将讨论近似算法的特点如下。

*   近似算法保证在多项式时间内运行，尽管它不能保证最有效的解决方案。
*   近似算法保证寻找高精度和高质量的解决方案(比如在最佳方案的 1%以内)
*   近似算法用于在多项式时间内得到优化问题的(最优)解附近的答案

**近似算法的性能比:**
这里，我们将讨论近似算法的性能比如下。

**场景-1 :**

1.  假设我们正在研究一个优化问题，其中每个潜在的解决方案都有成本，我们希望找到一个接近最优的解决方案。根据问题的不同，我们可以将最优解定义为具有最大可能成本或最小可能成本的解，即问题可以是最大化问题，也可以是最小化问题。
2.  我们说，如果对于任何输入大小 n，由算法产生的解的成本 C 在最优解的成本 C*的因子 P(n)之内，则问题的算法具有适当的比率 P(n)，如下所示。

```
max(C/C*,C*/C)<=P(n)
```

**场景-2 :**
如果一个算法达到了 P(n)的逼近比，那么我们称之为 P(n)-逼近算法。

*   对于一个最大化问题，0< C < C×，C/C*的比值给出了一个最优解的代价大于近似算法的代价的因子。
*   对于最小化问题，0< C* < C，C/C*的比值给出了近似解的成本大于最优解的成本的因子。

**近似算法的一些例子:**
这里，我们将讨论近似算法的一些例子如下。

1.  [**顶点覆盖问题**](https://www.geeksforgeeks.org/vertex-cover-problem-set-1-introduction-approximate-algorithm-2/)**–**
    在顶点覆盖问题中，优化问题是选择应覆盖图中所有边的最小顶点数。

2.  [**旅行推销员问题**](https://www.geeksforgeeks.org/traveling-salesman-problem-tsp-implementation/)**—**
    在旅行推销员问题中，优化问题是推销员必须走成本最小的路线。

3.  [**集合覆盖问题**](https://www.geeksforgeeks.org/set-cover-problem-set-1-greedy-approximate-algorithm/)**–**
    这是一个优化问题，对很多需要分配资源的问题进行建模。这里，使用对数近似比。

4.  [**子集和问题**](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)**–**
    在子集和问题中，优化问题是寻找和尽可能大但不大于目标值 t 的{x1，×2，×3…xn}的子集。