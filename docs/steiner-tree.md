# 斯坦纳树问题

> 原文： [https://www.geeksforgeeks.org/steiner-tree/](https://www.geeksforgeeks.org/steiner-tree/)

**什么是斯坦纳树？**

给定一个图形和图形中顶点的一个**子集**，一棵斯坦纳树跨越该给定子集。 Steiner 树可能包含一些不在给定子集中的顶点，但用于连接子集的顶点。

给定的顶点集称为 ***终端顶点*** ，而用于构造 Steiner 树的其他顶点称为 ***Steiner 顶点*** 。

 **斯坦纳树问题**是寻找成本最低的斯坦纳树。 参见以下示例。

![steiner](img/304ba7c024b1cd8f9362d64978cf3fde.png)

**生成树与 Steiner 树**

[最小生成树](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)是跨越**所有**顶点的最小权重树。

如果给定的子集（或终端）顶点等于斯坦纳树问题中所有顶点的集合，则该问题变为最小生成树问题。 如果给定的子集只包含两个顶点，则它在两个顶点之间的最短路径问题。

找出最小生成树是多项式时间可解的，但是最小斯坦纳树问题是 NP Hard，相关决策问题是 NP-Complete。

**Steiner Tree**

的应用任务是将某些重要位置（例如 VLSI 设计，计算机网络等）之间的连接成本降至最低的任何情况。

**基于最短路径的近似算法**

由于 Steiner Tree 问题是 NP-Hard，因此没有多项式时间解总是提供最佳成本。 因此，存在解决该问题的近似算法。 以下是一种简单的近似算法。

```
1) Start with a subtree T consisting of 
   one given terminal vertex
2) While T does not span all terminals
   a) Select a terminal x not in T that is closest 
      to a vertex in T.
   b) Add to T the shortest path that connects x with T

```

上面的算法是近似的（2-2 / n），即对于给定的 n 个顶点图，它保证了该算法产生的解不超过优化解的比率。 还有更好的算法可以提供更好的比率。 有关更多详细信息，请参考以下参考。

**参考**：

[www.cs.uu.nl/docs/vakken/an/teoud/an-steiner.ppt](http://www.cs.uu.nl/docs/vakken/an/teoud/an-steiner.ppt)

本文由 **Shivam Gupta** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

