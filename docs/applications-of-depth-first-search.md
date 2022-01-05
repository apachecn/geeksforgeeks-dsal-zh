# 深度优先搜索的应用

> 原文:[https://www . geesforgeks . org/applications-of-depth-first-search/](https://www.geeksforgeeks.org/applications-of-depth-first-search/)

深度优先搜索是一种遍历图的算法(或技术)。

以下是使用 DFS 作为构造块的问题。

**1)检测图中的循环**
当且仅当我们在 DFS 期间看到后沿时，图才有循环。因此，我们可以运行图的 DFS 并检查后边缘。(详见[本](http://people.csail.mit.edu/thies/6.046-web/recitation9.txt)

**2)路径寻找**
我们可以专门化 DFS 算法来寻找两个给定顶点 u 和 z 之间的路径
i)调用以 u 为起始顶点的 DFS(G，u)。
ii)使用堆栈跟踪开始顶点和当前顶点之间的路径。
iii)一旦遇到目的顶点 z，就返回路径作为堆栈的
内容

详见[本](http://ww3.algorithmdesign.net/handouts/DFS.pdf)。

**3)** [**拓扑排序**](https://www.geeksforgeeks.org/topological-sorting/)
拓扑排序主要用于根据作业之间给定的依赖关系调度作业。在计算机科学中，这种类型的应用出现在指令调度、在电子表格中重新计算公式值时公式单元求值的顺序、逻辑综合、确定编译任务在 makefiles 中执行的顺序、数据序列化以及解决链接器中的符号依赖关系[2]。

**4)为了测试一个图是否是** [**二部图**](http://en.wikipedia.org/wiki/Bipartite_graph)
当我们第一次发现一个新的顶点时，我们可以扩充 BFS 或 DFS，给它加上与其父顶点相对的颜色，对于每个其他边，检查它是否没有链接两个颜色相同的顶点。任何连接组件中的第一个顶点可以是红色或黑色！详见[本](http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/LEC/LECTUR16/NODE16.HTM)。

**5)求图的强连通分支**有向图如果从图中的每个顶点到其他每个顶点都有一条路径，则称为强连通。(参见[本](https://www.geeksforgeeks.org/strongly-connected-components/)了解寻找强连接组件的基于离散傅立叶变换的算法)

**6)只用一个解**解谜，比如迷宫。(通过在访问集中仅包含当前路径上的节点，DFS 可以适用于寻找迷宫的所有解。)

**来源:**
[http://www 8 . cs . umu . se/kuser/TDBAfl/VT06/algorithms/LEC/lecture 16/node 16。HTM](http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/LEC/LECTUR16/NODE16.HTM)
[http://en.wikipedia.org/wiki/Depth-first_search](http://en.wikipedia.org/wiki/Depth-first_search)
[http://www . personal . Kent . edu/~ rmuhamma/Algorithms/myalgor/depthsearch . htm](http://www.personal.kent.edu/~rmuhamma/Algorithms/MyAlgorithms/GraphAlgor/depthSearch.htm)
[http://ww3.algorithmdesign.net/handouts/DFS.pdf](http://ww3.algorithmdesign.net/handouts/DFS.pdf)