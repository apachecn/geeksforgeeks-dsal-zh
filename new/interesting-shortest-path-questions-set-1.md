# 一些有趣的最短路径问题 | 系列 1

> 原文： [https://www.geeksforgeeks.org/interesting-shortest-path-questions-set-1/](https://www.geeksforgeeks.org/interesting-shortest-path-questions-set-1/)

**问题 1：*给定有向加权图。 从源顶点“ s”到目标顶点“ t”的最短路径也给了您。 如果每条边的权重增加 10 个单位，则最短路径在修改后的图中是否保持不变？***

最短路径可能会改变。 原因是，从 s 到 t 的不同路径中的边数可能不同。 例如，让最短路径的权重为 15，并具有 5​​条边。 假设有一条具有 2 条边且总权重为 25 的路径。最短路径的权重增加 5 * 10，变为 15 +50。另一条路径的权重增加 2 * 10，变为 25 + 20。 最短路径更改为权重为 45 的另一条路径。

****问题 2**：*与上述问题类似。 当所有边的权重乘以 10 时，最短路径会改变吗？***

如果将所有边权重乘以 10，则最短路径不会改变。 原因很简单，从 s 到 t 的所有路径的权重乘以相同的数量。 路径上的边数无关紧要。 就像改变重量单位一样。

****问题 3**：*给定一个有向图，其中每个边的权重为 1 或 2，找到从给定源顶点 s 到目标顶点 t 的最短路径。 。 预期时间复杂度为`O(V + E)`。***

如果应用 [Dijkstra 的最短路径算法](https://www.geeksforgeeks.org/greedy-algorithms-set-7-dijkstras-algorithm-for-adjacency-list-representation/)，我们可以获得 O（E + VLogV）时间中的最短路径。 如何在`O(V + E)`时间里做到？ 这个想法是使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。 关于 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的一个重要发现是，在 BFS 中使用的路径在任何两个顶点之间始终具有最少数量的边。 因此，如果所有边的权重相同，则可以使用 BFS 查找最短路径。 对于此问题，我们可以修改图形并将权重 2 的所有边均分成权重 1 的两个边。 在修改后的图中，我们可以使用 BFS 查找最短路径。`O(V + E)`如何处理？ 在最坏的情况下，所有边的权重为 2，我们需要执行 O（E）运算以拆分所有边，因此时间复杂度变为 O（E）+`O(V + E)`，即`O(V + E)`。

****问题 4**：*给定有向无环加权图，如何在`O(V + E)`的时间内找到从源 s 到目标 t 的最短路径 ？***

请参见：[有向无环图](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)中的最短路径

**更多问题**有关更多问题，请参见以下链接。

[http://algs4.cs.princeton.edu/44sp/](http://algs4.cs.princeton.edu/44sp/)

[https://www.geeksforgeeks.org/algorithms-gq/graph-shortest-paths-gq /](https://www.geeksforgeeks.org/algorithms-gq/graph-shortest-paths-gq/)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

