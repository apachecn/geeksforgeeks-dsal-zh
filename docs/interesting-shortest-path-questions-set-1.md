# 一些有趣的最短路径问题|第 1 集

> 原文:[https://www . geesforgeks . org/interest-最短路径-问题-set-1/](https://www.geeksforgeeks.org/interesting-shortest-path-questions-set-1/)

**问题 1: *给定一个有向加权图。还会给出从源顶点到目标顶点的最短路径。如果每条边的权重增加 10 个单位，修改后的图中最短路径是否保持不变？***
最短的路径可能会改变。原因是，从 s 到 t 的不同路径中可能有不同数量的边，例如，让最短路径权重为 15，有 5 条边。假设有另一条路径有 2 条边，总重量为 25。最短路径的权重增加 5*10，变成 15 + 50。另一条路径的权重增加 2*10，变成 25 + 20。因此最短路径变为另一条路径，权重为 45。

****问题 2:** *这个和上面的问题差不多。当所有边的权重乘以 10 时，最短路径会改变吗？***
如果我们将所有边权重乘以 10，最短路径不会改变。原因很简单，从 s 到 t 的所有路径的权重都乘以相同的数量。路径上的边数并不重要。这就像改变重量单位。

****问题 3:** *给定一个有向图，其中每条边的权重为 1 或 2，找到从给定源顶点到给定目的顶点的最短路径。预期时间复杂度为 O(V+E)。***
如果应用[迪克斯特拉最短路径算法](https://www.geeksforgeeks.org/greedy-algorithms-set-7-dijkstras-algorithm-for-adjacency-list-representation/)，可以在 O(E + VLogV)时间内得到一条最短路径。O(V+E)时间怎么做？想法是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。关于 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的一个重要观察是，BFS 使用的路径在任意两个顶点之间的边数总是最少的。所以如果所有边的权重相同，我们可以用 BFS 来寻找最短路径。对于这个问题，我们可以修改图，将权重 2 的所有边分成权重 1 的两条边。在修改后的图中，我们可以使用 BFS 来寻找最短路径。这种做法是如何 O(V+E)的？最坏的情况，所有边的权重都是 2，我们需要做 O(E)运算来拆分所有边，所以时间复杂度变成 O(E) + O(V+E)，也就是 O(V+E)。

****问题 4:** *给定一个有向无环加权图，如何在 O(V+E)时间内找到从源 s 到目的地 t 的最短路径？***
参见:[有向无环图中的最短路径](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)

**更多问题**更多问题见以下链接。
[http://algs4.cs.princeton.edu/44sp/](http://algs4.cs.princeton.edu/44sp/)
[https://www . geeksforgeeks . org/algorithms-GQ/graph-最短路径-gq/](https://www.geeksforgeeks.org/algorithms-gq/graph-shortest-paths-gq/)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。