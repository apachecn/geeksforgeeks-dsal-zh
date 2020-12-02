# 用于最大匹配的 Hopcroft-Karp 算法| 第 1 组（简介）

> 原文： [https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-1-introduction/](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-1-introduction/)

[二分图](https://www.geeksforgeeks.org/bipartite-graph)中的匹配项是一组边，它们的选择方式是没有两个边共享端点。 最大匹配是最大大小（最大边数）的匹配。 在最大匹配中，如果添加了任何边，则不再是匹配。 给定的二分图可能有多个以上的最大匹配项。

在[的先前文章](https://www.geeksforgeeks.org/maximum-bipartite-matching/)中，我们讨论了最大匹配和[基于福特福尔克森方法的最大二分匹配](https://www.geeksforgeeks.org/maximum-bipartite-matching/)的重要性。 基于福特福尔克森算法的时间复杂度为 O（V x E）。

Hopcroft Karp 算法是对 O（√Vx E）时间的改进。 在讨论算法之前，让我们定义几个术语

***自由节点或顶点：*** 给定匹配 M，不属于匹配部分的节点称为自由节点。 最初，所有顶点都是免费的（请参见下图的第一个图）。 在第二张图中，u2 和 v2 是空闲的。 在第三张图中，没有顶点是自由的。

***匹配边缘和非匹配边缘：*** 给定匹配 M，则称为匹配边缘的边缘称为匹配边缘，不属于 M 的边缘（或连接自由节点）称为边缘 边缘不匹配。 在第一个图中，所有边都不匹配。 在第二张图中，（u0，v1），（u1，v0）和（u3，v3）匹配，其他不匹配。

***备用路径：*** 给定匹配 M，备用路径是其中边交替属于匹配和不匹配的路径。 所有单边路径均为交替路径。 中间图中交替路径的示例是 u0-v1-u2 和 u2-v1-u0-v2。

***增强路径：*** 给定匹配 M，增强路径是从自由顶点开始并在自由顶点结束的交替路径。 以自由顶点开始和结束的所有单边路径都是扩充路径。 在下图中，增强路径以蓝色突出显示。 请注意，扩展路径始终具有一个额外的匹配边。

Hopcroft Karp 算法基于以下概念。

*如果存在扩展路径，则匹配 M 不是最大值。 其他方法也是如此，即如果不存在扩展路径，则匹配为最大值*

因此，想法是一一寻找扩展路径。 并将找到的路径添加到当前匹配项。

**Hopcroft Karp 算法**

```
1) Initialize Maximal Matching M as empty.
2) While there exists an Augmenting Path p
     Remove matching edges of p from M and add not-matching edges of p to M
     (This increases size of M by 1 as p starts and ends with a free vertex)
3) Return M. 
```

下图显示了该算法的工作。

[![HopcroftKarp](img/490698ef44d99035f19fee5c18d91ef1.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/HopcroftKarp1.png)

在初始图中，所有单个边都是增加路径，我们可以按任意顺序进行选择。 在中间阶段，只有一条扩展路径。 我们从 M 中删除此路径的匹配边，并添加不匹配边。 在最终匹配中，没有扩展路径，因此匹配最大。

集合 2 中讨论了 Hopcroft Karp 算法的实现。

[用于最大匹配的 Hopcroft-Karp 算法| 第 2 组（实施）](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-2-implementation/)

 **参考：**
[https://en.wikipedia.org/wiki/Hopcroft%E2%80%93Karp_algorithm](https://en.wikipedia.org/wiki/Hopcroft%E2%80%93Karp_algorithm)
[http：// www .dis.uniroma1.it /〜leon / tcs / lecture2.pdf](http://www.dis.uniroma1.it/~leon/tcs/lecture2.pdf)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

