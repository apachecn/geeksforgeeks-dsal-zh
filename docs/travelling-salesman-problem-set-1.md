# 旅行推销员问题|集合 1(朴素动态规划)

> 原文:[https://www . geesforgeks . org/travel-Salman-problem-set-1/](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)

**旅行商问题(TSP):** 给定一组城市和每对城市之间的距离，问题是找到恰好访问每个城市一次并返回起点的最短可能路线。
注意[哈密顿圈](https://www.geeksforgeeks.org/backtracking-set-7-hamiltonian-cycle/)和 TSP 的区别。哈密尔顿循环问题是找出是否存在一个每座城市都只参观一次的旅游。这里我们知道哈密顿圈是存在的(因为图是完整的)，事实上很多这样的圈是存在的，问题是找到一个最小权重的哈密顿圈。

[![Euler1](img/f13c11b6b6abf6bde87d85db87cd09b6.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Euler12.png)

例如，考虑右侧图中所示的图表。图中的 TSP 游是 1-2-4-3-1。旅游费用是 10+25+30+15 也就是 80。

问题是一个著名的 [NP 难](https://www.geeksforgeeks.org/np-completeness-set-1/)问题。这个问题没有多项式时间的已知解。

以下是旅行推销员问题的不同解决方案。

**天真的解决方案:**
1)考虑城市 1 作为起点和终点。
2)全部生成(n-1)！[城市的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)。
3)计算每个置换的成本，并跟踪最小成本置换。
4)以最小代价返回置换。

时间复杂度:θ(n！)

**动态规划:**
让给定的顶点集为{1，2，3，4，…。n}。让我们考虑 1 作为输出的起点和终点。对于每隔一个顶点 I(除了 1)，我们找到以 1 为起点，I 为终点，所有顶点恰好出现一次的最小代价路径。假设这条路径的成本是成本(I)，相应周期的成本将是成本(i) +距离(I，1)，其中距离(I，1)是从 I 到 1 的距离。最后，我们返回所有[成本(i) +距离(I，1)]值中的最小值。到目前为止，这看起来很简单。现在的问题是如何获得成本(I)？
为了使用动态规划计算成本(I)，我们需要在子问题方面有一些递归关系。让我们定义一个术语 *C(S，I)是访问集合 S 中每个顶点一次的最小代价路径的代价，从 1 开始，到 i* 结束。
我们从大小为 2 的所有子集开始，计算所有子集的 C(S，I)，其中 S 是子集，然后我们计算大小为 3 的所有子集 S 的 C(S，I)以此类推。请注意，每个子集都必须有 1。

```
If size of S is 2, then S must be {1, i},
 C(S, i) = dist(1, i) 
Else if size of S is greater than 2.
 C(S, i) = min { C(S-{i}, j) + dis(j, i)} where j belongs to S, j != i and j != 1.

```

对于大小为 n 的集合，我们考虑 n-2 个子集，每个子集的大小为 n-1，这样所有的子集都不会有 n 个。
利用上述递推关系，我们可以写出基于动态规划的解。最多有 O(n*2 <sup>n</sup> 个子问题，每一个都需要线性时间求解。因此总运行时间为 0(n<sup>2</sup>* 2<sup>n</sup>)。时间复杂度比 O(n！)，但仍然是指数级的。所需空间也是指数级的。因此，这种方法也是不可行的，即使是稍微高一些的顶点。

我们将很快讨论旅行推销员问题的近似算法。

下一篇:[旅行推销员问题|第二集](https://www.geeksforgeeks.org/travelling-salesman-problem-set-2-approximate-using-mst/)

**参考文献:**
[http://www . LSI . UPC . edu/~ mjserna/docencia/algo fib/P07/dynprog . pdf](http://www.lsi.upc.edu/~mjserna/docencia/algofib/P07/dynprog.pdf)
T6】http://www.cs.berkeley.edu/~vazirani/algorithms/chap6.pdf

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论