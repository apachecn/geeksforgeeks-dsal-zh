# 优先级队列的应用

> 原文:[https://www.geeksforgeeks.org/applications-priority-queue/](https://www.geeksforgeeks.org/applications-priority-queue/)

一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)不同于一个普通的[队列](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)，因为不是一个“先进先出”的队列，而是值按照优先级的顺序出现。这是一种抽象的数据类型，它抓住了容器的思想，容器的元素都有“优先级”。优先级最高的元素总是出现在队列的前面。如果该元素被删除，下一个最高优先级的元素将前进到前面。

优先级队列通常使用[堆数据结构](https://www.geeksforgeeks.org/heap-data-structure/)来实现。

<center>**应用:**</center>

[利用优先级队列的 Dijkstra 最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/):当图以邻接表或矩阵的形式存储时，在实现 Dijkstra 算法时，可以利用优先级队列高效提取最小值。

[Prim 算法](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/):用于实现 Prim 算法存储节点的密钥，每一步提取最小密钥节点。

[数据压缩](https://en.wikipedia.org/wiki/Data_compression):用在[霍夫曼码](https://www.geeksforgeeks.org/tag/huffman-coding/)中，用来压缩数据。

**人工智能** : [A*搜索算法](https://www.geeksforgeeks.org/a-search-algorithm/):a*搜索算法找到一个加权图的两个顶点之间的最短路径，先尝试出最有前途的路线。优先级队列(也称为边缘)用于跟踪未探索的路由，总路径长度下限最小的路由被赋予最高优先级。

[堆排序](https://www.geeksforgeeks.org/heap-sort/):堆排序通常使用堆来实现，堆是优先级队列的实现。

[操作系统](https://en.wikipedia.org/wiki/Operating_system):也用于操作系统[负载均衡](https://en.wikipedia.org/wiki/Load_balancing_(computing)) ( [服务器](https://www.geeksforgeeks.org/load-balancing-on-servers-random-algorithm/)负载均衡)[中断处理](https://practice.geeksforgeeks.org/problems/interrupt-handlers)。

本文由**萨赫勒拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。