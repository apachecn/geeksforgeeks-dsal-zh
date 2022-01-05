# 二叉树的 BFS vs DFS

> 原文:[https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/](https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/)

**什么是二叉树的 BFS 和 DFS？**
一棵树通常有两种穿越方式:

*   [广度优先遍历(或水平顺序遍历)](https://www.geeksforgeeks.org/level-order-tree-traversal/)
*   [深度首次穿越](https://www.geeksforgeeks.org/618/)
    *   有序遍历(左根右)
    *   前序遍历(根-左-右)
    *   后序遍历(左-右-根)

![Example Tree](img/34a0f18bcfea93de93a6282740c0a4b6.png "tree12")

```
BFS and DFSs of above Tree

Breadth First Traversal : 1 2 3 4 5

Depth First Traversals:
      Preorder Traversal : 1 2 4 5 3 
      Inorder Traversal  :  4 2 5 1 3 
      Postorder Traversal : 4 5 2 3 1

```

**我们为什么在乎？**
有很多树的问题可以用上面四种遍历中的任何一种来解决。此类问题的例子有[大小](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-size-of-a-tree/)、[最大](http://geeksquiz.com/find-maximum-or-minimum-in-binary-tree/)、[最小](http://geeksquiz.com/find-maximum-or-minimum-in-binary-tree/)、[打印左视图](https://www.geeksforgeeks.org/print-left-view-binary-tree/)等。

**时间复杂度有什么区别吗？**
所有四个遍历都需要 O(n)个时间，因为它们只访问每个节点一次。

**额外空间方面有区别吗？**
所需的额外空间是有区别的。

1.  级别顺序遍历所需的额外空间是 O(w)，其中 w 是二叉树的最大宽度。在层次顺序遍历中，队列一个接一个地存储不同层次的节点。
2.  深度优先遍历所需的额外空间是 0(h)，其中 h 是二叉树的最大高度。在深度优先遍历中，堆栈(或函数调用堆栈)存储节点的所有祖先。

二叉树在深度(或高度)h 的最大宽度可以是 2 <sup>h</sup> ，其中 h 从 0 开始。所以最大节点数可以在最后一级。最糟糕的情况发生在二叉树是一棵完美的二叉树，其节点数为 1、3、7、15…等。最坏的情况下，2 <sup>h</sup> 的值为 **Ceil(n/2)** 。

平衡二叉树的高度为 0。最差情况发生在倾斜的树，最差情况高度变为 0(n)。

因此，在最坏的情况下，两者都需要额外的空间。但是最坏的情况发生在不同类型的树上。

***从以上几点可以明显看出，当树比较平衡时，Level order 遍历所需的额外空间可能更多，而当树不太平衡时，Depth First 遍历所需的额外空间可能更多。**T3】*

**怎么挑一个？**

1.  额外空间可能是一个因素(如上所述)
2.  深度优先遍历通常是递归的，递归代码需要函数调用开销。
3.  最重要的一点是，BFS 从根开始访问节点，而 DFS 从叶开始访问节点。因此，如果我们的问题是寻找更接近根的东西，我们会更喜欢 BFS。如果目标节点靠近叶子，我们更喜欢 DFS。

**练习:**
应该用哪个遍历来打印二叉树的叶子，为什么？
在 k 比总层数少很多的第 k 层打印节点应该使用哪种遍历？

本文由 **Dheeraj Gupta** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论