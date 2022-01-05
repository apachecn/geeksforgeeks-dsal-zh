# 迪杰斯特拉算法和弗洛伊德-沃肖尔算法的比较

> 原文:[https://www . geeksforgeeks . org/comparison-dijkstras-Floyd-war shall-algorithms/](https://www.geeksforgeeks.org/comparison-dijkstras-floyd-warshall-algorithms/)

**主要目的:**

*   [Dykstra algorithm](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/) is an example of single-source shortest or SSSP algorithm, that is, given a source vertex, it finds the shortest path from the source to all other vertices.
*   [Freud Washer's algorithm](https://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/) is an example of all-pair shortest path algorithm, which means that it calculates the shortest path between all node pairs.

**时间复杂度:**

*   Time complexity of Dykstra algorithm: O(E log V)
*   Freud Washer's Time Complexity: O (v <sup>3</sup> )

**其他点:**

*   We can use Dijskstra's shortest path algorithm to find all pairs of shortest paths by running it on each vertex. But the time complexity of this one is O(VE Log V), which can reach (v <sup>3</sup> logv) in the worst case.
*   Another important difference between algorithms is that they work for distributed systems. Unlike Dijkstra's algorithm, Floyd Warshall can be implemented in a distributed system, which makes it suitable for data structures like Graph of Graphs.
*   Finally, Freud Washer is suitable for negative edges, but there is no [negative period](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/) , while Dykstra algorithm is not suitable for negative edges.

本文由**vinet Joshi**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。