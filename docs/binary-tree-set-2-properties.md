# 二叉树|集合 2(属性)

> 原文:[https://www.geeksforgeeks.org/binary-tree-set-2-properties/](https://www.geeksforgeeks.org/binary-tree-set-2-properties/)

我们已经讨论了第 1 集中的[二叉树介绍。在这篇文章中，讨论了二叉树的性质。](http://quiz.geeksforgeeks.org/binary-tree-set-1-introduction/)

***1)二叉树的‘l’级最大节点数为 2<sup>l</sup>**T5。
这里 level 是从根到节点(包括根和节点)的路径上的节点数。根的级别为 0。
这可以用归纳法证明。
对于根，l = 0，节点数= 2 <sup>0</sup> = 1
假设级别‘l’上的最大节点数为 2 <sup>l</sup>
因为在二叉树中每个节点最多有 2 个子节点，下一个级别将有两个节点，即 2 * 2 <sup>l</sup>*

***2)******高度为“h”的二叉树的最大节点数为 2<sup>h</sup>–1***。
这里树的高度是根到叶路径上的最大节点数。单个节点的树的高度被认为是 1。
这个结果可以从上面第 2 点推导出来。如果所有级别都有最大节点数，则树有最大节点数。所以高度为 h 的二叉树的最大节点数是 1 + 2 + 4 +..+ 2 <sup>h</sup> 。这是一个带有 h 项的简单几何级数，这个级数的和是 2<sup>h</sup>–1。
在一些书中，根的高度被认为是 0。在本惯例中，上述公式变为 2<sup>h+1</sup>–1

***3)在有 N 个节点的二叉树中，最小可能高度还是******的最小层数是？日志 <sub>2</sub> (N+1)？***
这个可以直接从上面第 2 点推导出来。如果我们考虑根节点的高度被认为是 0 的惯例，那么上述最小可能高度的公式变成| Log<sub>2</sub>(N+1)|–1

***4)叶子为 L 的二叉树至少有| Log <sub>2</sub> L？|+ 1 级***
当所有级别都被完全填充时，二叉树具有最大数量的叶子(和最小数量的级别)。假设所有的叶子都在 l 级，那么对于叶子的数量 l 来说，下面是正确的。

```
L   <=  2l-1  [From Point 1]
l =   | Log2L | + 1 
where l is the minimum number of levels.
```

***5)在每个节点有 0 或 2 个子节点的二叉树中，*** ***叶节点的数量总是比有两个子节点的节点多一个*** 。

```
L = T + 1
Where L = Number of leaf nodes
T = Number of internal nodes with two children
Proof:
No. of leaf nodes (L) i.e. total elements present at the bottom of tree = 
2h-1 (h is height of tree)
No. of internal nodes = {total no. of nodes} - {leaf nodes} = 
{ 2h - 1 } - {2h-1} = 2h-1 (2-1) - 1 = 2h-1 - 1
So , L = 2h-1
     T = 2h-1 - 1
Therefore L = T + 1
Hence proved
```

证明见[握手引理和树](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)。
在下一篇关于树系列的文章中，我们将讨论[不同类型的二叉树及其属性](http://quiz.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。