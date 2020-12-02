# Dijkstra 算法与 Floyd-Warshall 算法的比较

> 原文： [https://www.geeksforgeeks.org/comparison-dijkstras-floyd-warshall-algorithms/](https://www.geeksforgeeks.org/comparison-dijkstras-floyd-warshall-algorithms/)

**主要用途**：

*   [Dijkstra 的算法](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)是单源最短算法或 SSSP 算法的一个示例，即，给定一个源顶点，它将找到从源到所有其他顶点的最短路径。
*   [Floyd Warshall 算法](https://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/)是全对最短路径算法的一个示例，这意味着它计算所有节点对之间的最短路径。

**时间复杂度**：

*   Dijkstra 算法的时间复杂度：O（E log V）
*   Floyd Warshall 的时间复杂度：O（V <sup>3</sup> ）

**其他要点**：

*   我们可以使用 Dijskstra 的最短路径算法，通过为每个顶点运行所有对最短路径，来查找所有对最短路径。 但是，此方法的时间复杂度为 O（VE Log V），在最坏的情况下可以变为（V <sup>3</sup> Log V）。
*   算法之间的另一个重要区别因素是它们致力于分布式系统。 与 Dijkstra 的算法不同，Floyd Warshall 可以在分布式系统中实现，使其适用于诸如 Graph Graphs（在地图中使用）之类的数据结构。
*   最后，弗洛伊德·沃沙（Floyd Warshall）适用于负边缘，但没有[负周期](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/)，而 Dijkstra 的算法不适用于负边缘。

本文由 **Vineet Joshi** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

