# 最小生成树问题的应用

> 原文： [https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/](https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/)

最小生成树（MST）问题：给定连接图 G 具有正的边权重，找到连接所有顶点的边的最小权重集。

MST 是各种应用程序的基本问题。

**网络设计。**

*–电话，电气，液压，电视电缆，计算机，道路*

标准应用是针对类似于电话网络设计的问题。 您的公司有多个办事处； 您想租用电话线以将它们彼此连接； 电话公司则收取不同的费用以连接不同的城市对。 您需要一组线路以最低的总成本连接所有办公室。 它应该是一棵生成树，因为如果网络不是一棵树，您总是可以去除一些边并节省资金。

**NP 难题的近似算法。**

*– [旅行业务员问题](http://en.wikipedia.org/wiki/Travelling_salesman_problem)， [Steiner 树](http://en.wikipedia.org/wiki/Steiner_tree_problem)*

一个不太明显的应用是最小生成树可用于近似求解 旅行商问题。 定义此问题的简便正式方法是找到至少一次访问每个点的最短路径。

请注意，如果您有一条路径仅能一次访问所有点，则这是一种特殊的树。 例如，在上面的示例中，十六棵生成树中的十二棵实际上是路径。 如果您有一条路径不止一次访问某些顶点，则始终可以放下一些边以获得一棵树。 因此，一般来说，MST 的权重要比 TSP 的权重小，因为它是在严格的更大范围内最小化的。

另一方面，如果在最小生成树周围绘制路径跟踪，则每个边跟踪两次并访问所有点，因此 TSP 权重小于 MST 权重的两倍。 因此，此行程是最佳行程的两倍。

**间接应用程序。**

–最大瓶颈路径

–用于纠错的 LDPC 码

–具有 Renyi 熵的图像配准

–学习用于实时人脸验证的显着特征

–减少序列中的数据存储 蛋白质中的氨基酸

–模拟湍流中颗粒相互作用的局部性

–以太网桥接的自动配置协议，以避免网络中的循环

**聚类分析**

k 聚类问题可以看作是找到一个 MST 并删除了 k-1 个最昂贵的

边。

**来源**：

[http://www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/mst.pdf](http://www.cs.princeton.edu/courses/archive/spr07/cos226/lectures/mst.pdf)

[http： //www.ics.uci.edu/~eppstein/161/960206.html](http://www.ics.uci.edu/~eppstein/161/960206.html)

