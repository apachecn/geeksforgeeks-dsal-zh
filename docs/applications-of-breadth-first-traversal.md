# 广度优先遍历的应用

> 原文:[https://www . geesforgeks . org/applications-of-width-first-遍历/](https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/)

我们之前讨论过图的[广度优先遍历算法](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)。我们还讨论了[深度优先遍历](https://www.geeksforgeeks.org/applications-of-depth-first-search/)的应用。本文讨论了广度优先搜索的应用。

**1)未加权图的最短路径和最小生成树**在未加权图中，最短路径是边数最少的路径。对于宽度优先，我们总是使用最小的边数从给定的源到达一个顶点。此外，在未加权图的情况下，任何生成树都是最小生成树，我们可以使用深度或广度优先遍历来寻找生成树。

**2)对等网络。**在像 [BitTorrent](https://www.geeksforgeeks.org/how-bittorrent-works/) 这样的对等网络中，广度优先搜索用于查找所有邻居节点。

**3)搜索引擎中的爬虫:**爬虫使用广度优先构建索引。这个想法是从源页面开始，跟随所有来自源的链接，并保持这样做。深度优先遍历也可以用于爬虫，但是广度优先遍历的优点是，构建的树的深度或层次可能是有限的。

**4)社交网络网站:**在社交网络中，我们可以使用广度优先搜索，直到“k”级，找到与一个人相距给定距离“k”以内的人。

**5) GPS 导航系统:**广度优先搜索用于查找所有邻近位置。

**6)网络中的广播:**在网络中，广播的分组跟随广度优先搜索到达所有节点。

**7)在垃圾收集中:**广度优先搜索用于使用[切尼算法](http://en.wikipedia.org/wiki/Cheney%27s_algorithm)复制垃圾收集。详见[本](https://lambda.uta.edu/cse5317/notes/node48.html)。广度优先搜索优于深度优先搜索，因为参考位置更好:

**8)** [**无向图中的循环检测:**](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/) 无向图中，广度优先搜索或深度优先搜索都可以用来检测循环。我们也可以使用 [BFS 检测有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-directed-graph-using-bfs/)中的循环，

**9)** [**福特–富尔克森算法**](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/) 在福特-富尔克森算法中，我们可以使用广度优先或深度优先遍历来寻找最大流量。广度优先遍历是首选，因为它将最坏情况下的时间复杂度降低到 0(VE<sup>2</sup>)。

**10)** [**为了测试一个图是否是二部图**](https://www.geeksforgeeks.org/bipartite-graph/) 我们可以使用广度优先或深度优先遍历。

**11)路径查找**我们可以使用广度优先或深度优先遍历来查找两个顶点之间是否有路径。

**12)查找一个连接组件内的所有节点:**我们可以使用广度优先或深度优先遍历来查找从给定节点可到达的所有节点。

许多算法，如 [Prim 的最小生成树](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)和 [Dijkstra 的单源最短路径](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)使用类似于广度优先搜索的结构。

由于广度优先搜索是图的核心算法之一，因此可以有更多的应用。

本文由**尼拉杰·贾恩**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论