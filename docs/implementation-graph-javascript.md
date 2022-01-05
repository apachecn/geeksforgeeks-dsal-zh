# 图形在 JavaScript 中的实现

> 原文:[https://www . geesforgeks . org/implementation-graph-JavaScript/](https://www.geeksforgeeks.org/implementation-graph-javascript/)

在本文中，我们将在 JavaScript 中实现[图形数据结构](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)。图形是一种非线性数据结构。图形 **G** 包含一组顶点 **V** 和一组边 **E** 。图在计算机科学中有许多应用。
**图形基本上分为两大类:**

*   **有向图(双向图)**–其中边有方向。
*   **无向图**–其中边不代表任何有向

有多种方法来表示图形:-

*   **邻接矩阵**
*   **邻接表**

还有其他几种方法，如关联矩阵等。但这两个是最常用的。邻接矩阵和列表的说明参见[图及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)。
在本文中，我们将使用**邻接表**来表示一个图，因为在大多数情况下，它比其他表示有一定的优势。
现在让我们看一个图形类的例子-

## Java Script 语言

```
// create a graph class
class Graph {
    // defining vertex array and
    // adjacent list
    constructor(noOfVertices)
    {
        this.noOfVertices = noOfVertices;
        this.AdjList = new Map();
    }

    // functions to be implemented

    // addVertex(v)
    // addEdge(v, w)
    // printGraph()

    // bfs(v)
    // dfs(v)
}
```