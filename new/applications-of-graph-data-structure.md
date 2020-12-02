# 图形数据结构的应用

> 原文： [https://www.geeksforgeeks.org/applications-of-graph-data-structure/](https://www.geeksforgeeks.org/applications-of-graph-data-structure/)

图是一种非线性数据结构，由通过边（或弧）连接的顶点（或节点）组成，其中边可以是有向的或无向的。
![](img/188b73e8769b25bf88ff62af8e5d9699.png)

*   在**中，计算机科学**图形用于表示计算流程。
*   **Google 地图**使用图形来构建交通运输系统，其中两条（或多条）道路的交叉点被视为一个顶点，而连接两个顶点的道路被视为一条边，因此其导航系统基于 该算法可计算两个顶点之间的最短路径。
*   在 **Facebook** 中，用户被视为顶点，如果他们是朋友，那么它们之间就会有优势。 Facebook 的 Friend 推荐算法使用图论。 Facebook 是**无向图**的示例。
*   在**万维网**中，网页被视为顶点。 如果页面 u 上有页面 v 的链接，则从页面 u 到其他页面 v 会有一条边。 这是**有向图**的示例。 这是 [Google 页面排名算法](https://www.geeksforgeeks.org/page-rank-algorithm-implementation/)背后的基本思想。
*   在**操作系统**中，我们遇到了“资源分配图”，其中每个进程和资源都被视为顶点。 从资源到分配的进程，或者从请求进程到所请求的资源，都吸引了边缘。 如果这导致形成任何循环，则将发生死锁。

因此，用于处理图形的算法的开发是计算机科学领域中的主要兴趣。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。