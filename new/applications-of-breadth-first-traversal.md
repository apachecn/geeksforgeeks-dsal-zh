# 广度优先遍历的应用

> 原文： [https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/](https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/)

我们之前已经讨论了[图的广度优先遍历算法](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)。 我们还讨论了[深度优先遍历](https://www.geeksforgeeks.org/applications-of-depth-first-search/)的应用。 本文讨论了广度优先搜索的应用。

1.  **未加权图的最短路径和最小生成树**在未加权图中，最短路径是边数最少的路径。 使用广度优先，我们总是使用最少的边数从给定的源到达顶点。 同样，在未加权图的情况下，任何生成树都是最小生成树，我们可以使用深度或广度优先遍历来查找生成树。

2.  **对等网络。** 在像 [BitTorrent](https://www.geeksforgeeks.org/how-bittorrent-works/) 这样的对等网络中，广度优先搜索用于查找所有邻居节点。

3.  **搜索引擎中的抓取工具**：抓取工具使用广度优先构建索引。 这个想法是从源页面开始，并遵循源中的所有链接并继续这样做。 深度优先遍历也可以用于爬虫，但是宽度优先遍历的优点是，可以限制所构建树的深度或级别。

4.  **社交网络网站**：在社交网络中，我们可以使用广度优先搜索找到距离某个人`k`级以内的人。

5.  **GPS 导航系统**：广度优先搜索用于查找所有邻近位置。

6.  **在网络中广播**：在网络中，广播数据包遵循广度优先搜索到达所有节点。

7.  **在垃圾收集中**：广度优先搜索用于使用 [Cheney 算法](http://en.wikipedia.org/wiki/Cheney%27s_algorithm)复制垃圾收集。 有关详情，请参见和。 广度优先搜索优于深度优先搜索，因为引用的位置更好：

8.  [**无向图中的循环检测**](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)：在无向图中，可以使用广度优先搜索或深度优先搜索来检测循环。 我们也可以使用 [BFS 来检测有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-directed-graph-using-bfs/)中的周期，

9.  [**Ford-Fulkerson 算法**](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/) 在 Ford-Fulkerson 算法中，我们可以使用广度优先或深度优先遍历来找到最大流量。 广度优先遍历是首选，因为它可以将最坏情况下的时间复杂度降低为`O(V E^2)`。

0.  [**要测试图是否为二分图**](https://www.geeksforgeeks.org/bipartite-graph/) ，我们可以使用广度优先或深度优先遍历。

1.  **路径查找**我们可以使用广度优先遍历或深度优先遍历来查找两个顶点之间是否存在路径。

2.  **查找一个连通组件内的所有节点**：我们可以使用广度优先或深度优先遍历来查找给定节点可到达的所有节点。

[Prim 的最小生成树](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)和 [Dijkstra 的单一源最短路径](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)等许多算法都使用类似于广度优先搜索的结构。

广度优先搜索是图的核心算法之一，因此可能会有更多的应用程序。

本文由 **Neeraj Jain** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

