# 为什么二进制堆优先于 BST 优先队列？

> 原文:[https://www . geesforgeks . org/why-is-binary-heap-preferred-over-BST-for-priority-queue/](https://www.geeksforgeeks.org/why-is-binary-heap-preferred-over-bst-for-priority-queue/)

典型的[优先级队列](http://geeksquiz.com/priority-queue-set-1-introduction/)需要以下操作才能有效。

1.  获取最高优先级元素(获取最小值或最大值)
2.  插入元素
3.  删除最高优先级元素
4.  减少键

一个[二进制堆](http://geeksquiz.com/binary-heap/)支持上述操作，时间复杂度如下:

1.  O(1)
2.  O(Logn)
3.  O(Logn)
4.  O(Logn)

[![heapvsbst](https://media.geeksforgeeks.org/wp-content/cdn-uploads/heapvsbst.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/heapvsbst.png)

像 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)、[红黑树、](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)等这样的自平衡二叉查找树也可以支持同样时间复杂度的上述操作。

1.  寻找最小值和最大值自然不是 O(1)，但可以通过将一个额外的指针保持在最小值或最大值，并在需要时通过插入和删除来更新指针，从而在 O(1)中轻松实现。删除后，我们可以通过寻找更早的前任或继任者来更新。
2.  插入一个元素自然是 O(Logn)
3.  删除最大值或最小值也是 O(Logn)
4.  减少键可以在 O(Logn)中通过先删除后插入来完成。详见[本](http://geeksquiz.com/how-to-implement-decrease-key-or-change-key-in-binary-search-tree/)。

**那么为什么优先队列优先选择二进制堆呢？**

*   因为二进制堆是使用数组实现的，所以总是有更好的引用局部性，并且操作对缓存更友好。
*   尽管运算的时间复杂度相同，但二叉查找树的常数更高。
*   我们可以在 O(n)时间内构建一个二进制堆。自平衡基站需要 0(nLogn)时间来构建。
*   二进制堆不需要额外的指针空间。
*   二进制堆更容易实现。
*   有像斐波那契堆这样的二进制堆的变体，可以支持θ(1)时间内的插入和减少键

**二进制堆总是更好吗？**
虽然二进制堆是针对优先级队列的，但是 BST 有自己的优势，优势列表实际上比二进制堆更大。

*   在自平衡 BST 中搜索一个元素是 O(Logn)，也就是二进制堆中的 O(n)。
*   我们可以在 O(n)时间内按排序顺序打印 BST 的所有元素，但是 Binary Heap 需要 O(nLogn)时间。
*   [地板和天花板](https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/)可以在 O(Logn)时间找到。
*   [通过用附加字段扩充树，在 0(Logn)时间内找到第 K 个最大/最小元素](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)。

本文由 **Vivek Gupta** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论