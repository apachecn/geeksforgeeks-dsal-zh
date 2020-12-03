# 深度优先搜索的应用

> 原文： [https://www.geeksforgeeks.org/applications-of-depth-first-search/](https://www.geeksforgeeks.org/applications-of-depth-first-search/)

深度优先搜索（DFS）是用于遍历图形的算法（或技术）。

以下是使用 DFS 作为构建块的问题。

**1）**对于加权图，图的 DFS 遍历将生成最小生成树和所有对最短路径树。

**2）检测图形中的周期**

当且仅当我们在 DFS 期间看到后边时，图形才具有周期。 因此，我们可以为图形运行 DFS 并检查后边。 （有关详细信息，请参见[此](http://people.csail.mit.edu/thies/6.046-web/recitation9.txt)）

**3）路径查找**

我们可以专门研究 DFS 算法，以找到两个给定顶点 u 和 z 之间的路径。

i）以 u 为起始顶点调用 DFS（G，u）。

ii）使用堆栈 S 跟踪起始顶点和当前顶点之间的路径。

iii）一旦遇到目标顶点 z，就将路径作为堆栈的

内容返回

有关详细信息，请参见此的[。](http://ww3.algorithmdesign.net/handouts/DFS.pdf)

**4）[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)**

拓扑排序主要用于根据作业之间的给定依赖性来调度作业。 在计算机科学中，这种类型的应用出现在指令调度，重新计算电子表格中的公式值时公式单元格评估的顺序，逻辑综合，确定要在 makefile 中执行的编译任务的顺序，数据序列化以及解析链接器中的符号依存关系[2]。 ]。

**5）测试图是否为[二分图](http://en.wikipedia.org/wiki/Bipartite_graph)**

当我们第一次发现新顶点时，可以对 BFS 或 DFS 进行扩充，对它的父对面着色，并为彼此的边 ，检查它是否未链接相同颜色的两个顶点。 任何连接的组件中的第一个顶点可以是红色或黑色！ 有关详细信息，请参见此的[。](http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/LEC/LECTUR16/NODE16.HTM)

**6）查找图的强连通组件**如果存在从图的每个顶点到每个其他顶点的路径，则有向图称为强连接。 （请参阅[此](https://www.geeksforgeeks.org/strongly-connected-components/)，这是基于 DFS 的算法，用于查找强连接的组件）

 **7）仅使用一种解决方案**解决难题，例如迷宫。 （通过仅在访问集中的当前路径上包括节点，DFS 可以适用于找到迷宫的所有解决方案。）

 **来源：

[http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/LEC/LECTUR16/NODE16.HTM](http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/LEC/LECTUR16/NODE16.HTM)

[http：// en。 wikipedia.org/wiki/深度优先搜索](http://en.wikipedia.org/wiki/Depth-first_search)

[http://www.personal.kent.edu/~rmuhamma/Algorithms/MyAlgorithms/GraphAlgor/depthSearch.htm](http://www.personal.kent.edu/~rmuhamma/Algorithms/MyAlgorithms/GraphAlgor/depthSearch.htm)

[http://ww3.algorithmdesign.net/handouts/DFS.pdf](http://ww3.algorithmdesign.net/handouts/DFS.pdf)

