# 哈希表与 STL 映射

> 原文：[https://www.geeksforgeeks.org/hash-table-vs-stl-map/](https://www.geeksforgeeks.org/hash-table-vs-stl-map/)

本文重点讨论：比较和对比 Hash 表和 STL Map。 哈希表如何实现？ 如果输入数量很少，那么可以使用哪些数据结构选项代替哈希表？

**哈希表**

在哈希表中，通过在键上调用哈希函数来存储值。

*   值未按排序顺序存储。

*   此外，由于哈希表使用键来查找将存储该值的索引，因此可以在摊销的 O（1）时间（假设哈希表中几乎没有冲突）中进行插入或查找。

*   在哈希表中，还必须处理潜在的冲突。 通常，这是通过[链接](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)来完成的，这意味着要创建所有键映射到特定索引的所有值的链表。

**哈希表的实现**：传统上，哈希表是通过一系列链接列表来实现的。 当我们要插入键/值对时，我们使用哈希函数将键映射到数组中的索引。 然后将该值插入到该位置的链接列表中。

**注意**：链表中数组特定索引处的元素没有相同的键。 而是，哈希函数（键）对于这些值是相同的。 因此，为了检索特定键的值，我们需要在每个节点中存储确切的键和值。

总而言之，哈希表将通过一系列链接列表来实现，其中链接列表中的每个节点都包含两段数据：值和原始键。 另外，我们将要注意以下设计准则：

1.  我们希望使用良好的哈希函数来确保密钥分布合理。 如果它们分布不均，则会发生大量碰撞，并且找到元素的速度也会下降。

2.  无论哈希函数多么出色，我们仍然会有冲突，因此我们需要一种处理它们的方法。 这通常意味着通过链接列表进行链接，但这不是唯一的方法。

3.  我们可能还希望实现一些方法来根据容量动态增加或减少哈希表的大小。 例如，当元素数与表大小的比率超过某个阈值时，我们可能希望增加哈希表的大小。 这将意味着创建一个新的哈希表，并将条目从旧表转移到新表。 因为这是一项昂贵的操作，所以我们要注意不要经常这样做。

**[STL 映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)**

容器映射是 C++ 的[标准库中包含的关联容器。 此类的定义位于名称空间 std 的头文件“ map”中。](https://www.geeksforgeeks.org/stack-in-cpp-stl/)

**STL Map 内部实现**：

它是作为自平衡红黑树实现的。 可能最常见的两种自平衡树是[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)和 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)。 为了在插入/更新之后平衡树，两种算法都使用旋转的概念，在该概念中，树的节点被旋转以执行重新平衡。 在两种算法中，插入/删除操作均为 O（log n），在红黑树重新平衡旋转的情况下为 O（1）操作，而对于 AVL，这是 O（log n）操作，因此 RB 树在这方面的重新平衡鼠尾草效率更高，并且是更常用的可能原因之一。

**哈希表和 STL 映射**之间的区别

1.  **空键**：STL 映射允许一个空键和多个空值，而哈希表不允许任何空键或值。

2.  **线程同步：如果不需要线程同步，则通常首选**映射而不是哈希表。 哈希表已同步。

3.  **线程安全**：STL 映射不是线程安全的，而哈希映射是线程安全的，并且可以与许多线程共享。

4.  **值顺序**：在 STL 映射中，值按排序顺序存储，而在哈希表中，值不按排序顺序存储

5.  **搜索时间**：对于较小的数据，您可以使用 STL 映射或二叉树（尽管花费 O（log n）时间，但输入的数量可能小到可以忽略该时间），并且对于 数据，哈希表是首选。

**相关文章**

*   [BST 优于哈希图](https://www.geeksforgeeks.org/advantages-of-bst-over-hash-table/)

*   [Java 中 HashMap 和 HashTable 之间的区别](https://www.geeksforgeeks.org/differences-between-hashmap-and-hashtable-in-java/)

本文由 **Brahmani Sai** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

