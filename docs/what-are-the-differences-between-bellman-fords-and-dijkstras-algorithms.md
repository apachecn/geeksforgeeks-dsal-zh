# 贝尔曼·福特的算法和迪杰斯特拉的算法有什么区别？

> 原文:[https://www . geeksforgeeks . org/bellman-fords-and-dijkstras-algorithms/](https://www.geeksforgeeks.org/what-are-the-differences-between-bellman-fords-and-dijkstras-algorithms/)有何不同

[**贝尔曼福特算法**](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)
和其他[动态规划问题](https://www.geeksforgeeks.org/solve-dynamic-programming-problem/)一样，该算法采用自下而上的方式计算最短路径。它首先计算路径中最多有一条边的最短距离。然后，它计算最多有 2 条边的最短路径，依此类推。在外环的第 I 次迭代之后，计算最多有 I 条边的最短路径。在任何简单路径中可以有最大| V |–1 条边，这就是为什么外循环运行| V |–1 次。其思想是，假设如果我们计算了最多有 I 条边的最短路径，则不存在负权重循环，那么在所有边上的迭代保证给出最多有(i+1)条边的最短路径

[**迪杰斯特拉的算法**](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)
迪杰斯特拉的算法与 Prim 的最小生成树算法非常相似。像 Prim 的 MST 一样，我们生成一个给定源作为根的 SPT(最短路径树)。我们维护两个集合，一个集合包含包含在最短路径树中的顶点，另一个集合包含尚未包含在最短路径树中的顶点。在算法的每一步，我们找到一个顶点，它在另一个集合(尚未包括的集合)中，并且与源的距离最小。

**贝尔曼福特算法和迪杰斯特拉算法的区别:**

**Bellman Ford 的算法**和 **Dijkstra 的算法**都是单源最短路径算法，即都是确定图的每个顶点距离单源顶点的最短距离。然而，它们之间有一些关键的区别。我们遵循贝尔曼·福特算法中的动态规划方法和迪克斯特拉算法中的贪婪方法。让我们看看这两种技术的其他主要区别-

<figure class="table">

| 贝尔曼·福特算法 | 迪克斯特拉算法 |
| --- | --- |
| 贝尔曼·福特算法在有负权重边缘时工作，它也检测负权重周期。 | 当存在负权重边缘时，迪克斯特拉算法不起作用。 |
| 结果包含顶点，这些顶点包含与其相连的其他顶点的信息。 | 结果包含的顶点包含网络的全部信息，而不仅仅是它们所连接的顶点。 |
| 它可以很容易地以分布式方式实现。 | 它不容易以分布式方式实现。 |
| 它比 Dijkstra 的算法更耗时。它的时间复杂度是 O(VE)。 | 耗时更少。时间复杂度为 O(E logV)。 |
| 算法采用动态规划方法实现。 | 采用贪婪方法实现算法。 |

</figure>