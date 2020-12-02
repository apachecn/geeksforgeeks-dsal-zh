# 旅行商问题| 设置 1（天真和动态编程）

> 原文： [https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)

**旅行商问题（TSP）**：给定一组城市以及每对城市之间的距离，问题在于找到最短的 p 条可行路线，该路线只对每个城市进行一次访问并返回起点 点。
注意[哈密顿循环](https://www.geeksforgeeks.org/backtracking-set-7-hamiltonian-cycle/)和 TSP 之间的差异。 汉密尔顿循环问题是要找出是否存在一次游览每个城市一次的旅行。 在这里，我们知道存在汉密尔顿游历（因为该图是完整的），并且实际上存在许多此类游历，问题是找到最小权重的汉密尔顿环。

![Euler1](img/f13c11b6b6abf6bde87d85db87cd09b6.png)

例如，考虑右侧图所示的图形。 图中的 TSP 巡视是 1-2-4-3-1。 游览费用为 10 + 25 + 30 + 15，即 80。

该问题是著名的 [NP 硬](https://www.geeksforgeeks.org/np-completeness-set-1/)问题。 没有多项式时间已知的解决方案来解决此问题。

以下是旅行商问题的不同解决方案。

**天真的解决方案**：
1）将城市 1 作为起点和终点。
2）生成所有（n-1）个！ [城市的排列[H​​TG5]。
3）计算每个排列的成本，并跟踪最小成本排列。
4）以最小的成本返回排列。](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

时间复杂度：Θ（n！）

**动态编程**：
令给定的顶点集为{1,2,3,4，.... n}。 让我们考虑 1 作为输出的起点和终点。 对于每个其他顶点 i（非 1），我们找到以 1 为起点，i 为终点且所有顶点仅出现一次的最小成本路径。 假设这条路径的成本为 cost（i），相应的 Cycle 的成本为 cost（i）+ dist（i，1），其中 dist（i，1）是从 i 到 1 的距离。最后，我们返回 所有[cost（i）+ dist（i，1）]值中的最小值。 到目前为止，这看起来很简单。 现在的问题是如何获得成本（i）？
要使用动态规划计算 cost（i），我们需要就子问题具有某种递归关系。 让我们定义项 *C（S，i）为从集 1 开始到 i* 为止，恰好一次访问集合 S 中每个顶点的最小成本路径的成本。
我们从大小为 2 的所有子集开始，为所有子集计算 C（S，i），其中 S 为子集，然后为大小为 3 的所有子集 S 计算 C（S，i），依此类推。 请注意，每个子集中必须存在 1。

```
If size of S is 2, then S must be {1, i},
 C(S, i) = dist(1, i) 
Else if size of S is greater than 2.
 C(S, i) = min { C(S-{i}, j) + dis(j, i)} where j belongs to S, j != i and j != 1.

```

对于大小为 n 的集合，我们考虑 n-2 个子集，每个子​​集的大小为 n-1，因此所有子集中的第 n 个都不是。
使用上述递归关系，我们可以编写基于动态编程的解决方案。 最多有 O（n * 2 <sup>n</sup> ）个子问题，每个子问题都需要线性时间来求解。 因此，总运行时间为 O（n <sup>2</sup> * 2 <sup>n</sup> ）。 时间复杂度远小于 O（n！），但仍然是指数级的。 所需空间也是指数的。 因此，即使顶点数量稍多，此方法也不可行。

我们将很快讨论旅行商问题的近似算法。

下一篇文章：[旅行商问题| 设置 2](https://www.geeksforgeeks.org/travelling-salesman-problem-set-2-approximate-using-mst/)

**参考**：
[http://www.lsi.upc.edu/~mjserna/docencia/algofib/P07/dynprog.pdf](http://www.lsi.upc.edu/~mjserna/docencia/algofib/P07/dynprog.pdf)
[http：/ /www.cs.berkeley.edu/~vazirani/algorithms/chap6.pdf](http://www.cs.berkeley.edu/~vazirani/algorithms/chap6.pdf)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

