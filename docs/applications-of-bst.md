# BST 的应用

> 原文:[https://www.geeksforgeeks.org/applications-of-bst/](https://www.geeksforgeeks.org/applications-of-bst/)

[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)，是一种基于节点的二叉树数据结构，具有以下特性:

*   节点的左子树只包含键小于节点键的节点。
*   节点的右子树只包含键大于节点键的节点。
*   左右子树也必须是二叉查找树树。
    不能有重复节点。

![200px-Binary_search_tree.svg](img/2bb297fb1a678d9c862d10acac5302e9.png)

一个 BST 在 O(h)时间内支持搜索、插入、删除、楼层、天花板、更大、更小等操作，其中 h 是 BST 的高度。为了保持更低的身高，实践中使用了自平衡 BST(如[AVL](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/))。这些自平衡 BST 将高度保持为 0(对数 n)。因此，上述所有操作都变成了 0(对数 n)。与这些一起，BST 还允许在 O(n)时间内对数据进行有序遍历。

1.  自平衡二叉查找树用于维护有序的数据流。例如，假设我们正在获得在线订单，并且我们希望按照价格的排序顺序维护实时数据(在内存中)。例如，我们希望随时了解以低于给定成本的成本购买的物品数量。或者我们想知道以高于给定成本的价格购买的物品数量。
2.  自平衡二叉查找树用于实现双端[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。使用二进制堆，我们可以实现一个支持 extractMin()或 extractMax()的优先级队列。如果我们希望支持这两种操作，我们使用自平衡二叉查找树来实现这两种操作
3.  还有很多算法问题，其中自平衡 BST 是最适合的数据结构，比如[计算右侧较小的元素](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)、[计算右侧最小的较大元素](https://www.geeksforgeeks.org/smallest-greater-element-on-right-side/)等。