# BST 优于哈希表

[哈希表](http://geeksquiz.com/hashing-set-1-introduction/)支持`Θ(1)`时间的以下操作。

1）搜索

2）插入

3）删除

自平衡[二叉搜索树（BST）](http://geeksquiz.com/binary-search-tree-set-1-search-and-insertion/)（如[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)， [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)和 [Splay 树](https://www.geeksforgeeks.org/splay-tree-set-1-insert/)）中上述操作的时间复杂度 等）是`O(Logn)`。

因此，哈希表似乎在所有常见操作中都击败了 BST。 什么时候我们应该比哈希表更喜欢 BST，有什么优势。 以下是支持 BST 的一些重要观点。

1.  只需执行 BST 的有序遍历，就可以按排序顺序获得所有键。 这不是哈希表中的自然操作，需要额外的努力。

2.  使用 BST 可以轻松进行[订单统计](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)，[查找最接近的上下元素](https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/)，[进行范围查询](https://www.geeksforgeeks.org/print-bst-keys-in-the-given-range/)。 像排序一样，这些操作对于哈希表也不是自然的操作。

3.  与散列相比，BST 易于实现，我们可以轻松实现自己的自定义 BST。 为了实现散列，我们通常依赖于编程语言提供的库。

4.  使用自平衡 BST，可以保证所有操作都可以在`O(Logn)`时间内进行。 但是对于散列，`Θ(1)`是平均时间，某些特定操作可能会很昂贵，尤其是在调整表大小时。

本文由 **Himanshu Gupta** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

