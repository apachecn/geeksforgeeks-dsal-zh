# 链表的优缺点

> 原文:[https://www . geesforgeks . org/链表的优缺点/](https://www.geeksforgeeks.org/advantages-and-disadvantages-of-linked-list/)

有很多[数据结构](https://www.geeksforgeeks.org/data-structures/)，像[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)等等。每种安排都有其长处和短处。由于这些原因，在设计、优化和扩展程序时，了解不同数据结构的优缺点非常重要。在本文中，我们将讨论链表的优缺点。

**<u>链表</u> :**

一个[链表](https://www.geeksforgeeks.org/rotate-a-linked-list/)是一个动态排列，它包含一个到包含后续项目的结构的“链接”。它是一组结构，不是按照它们在内存中的物理位置排序的(像一个数组)，而是按照作为信息的一部分存储在结构本身中的逻辑链接排序的。

链表是收集类似数据的另一种方式。然而，与[数组](https://www.geeksforgeeks.org/array-data-structure/)不同，链表中的元素不在连续的内存位置。链表由使用指针相互连接的节点组成。该图显示了一个链接列表。

[![](img/7e6950f4f74119957c56a6697709b0e1.png)](https://media.geeksforgeeks.org/wp-content/uploads/20201030205911/Linkedlist.png)

**<u>链表类型</u> :**

*   [**【单链表】**](https://www.geeksforgeeks.org/types-of-linked-list/) **:** 这是最简单的链表类型，其中每个节点都包含一些数据和指向同一数据类型的下一个节点的指针。该节点包含指向下一个节点的指针，这意味着该节点存储序列中下一个节点的地址。单个链表只允许以一种方式遍历数据。
*   [**双向或双向链表**](https://www.geeksforgeeks.org/types-of-linked-list/) **:** 双向链表或双向链表是一种更为复杂的链表类型，它依次包含指向下一个节点和上一个节点的指针，因此，它包含三个部分:数据、指向下一个节点的指针和指向上一个节点的指针。这将使我们也能够向后遍历列表。
*   [**循环链表**](https://www.geeksforgeeks.org/types-of-linked-list/) **:** 循环链表是指最后一个节点包含指向列表第一个节点的指针的链表。当遍历一个循环的喜欢的列表时，人们可以从任何节点开始，并以任何方向向前和向后遍历列表，直到到达开始的同一个节点。因此，循环链表没有开始也没有结束。
*   [**【循环双向链表】**](https://www.geeksforgeeks.org/types-of-linked-list/) **:** 双向循环链表或循环双向链表是一种更复杂的链表类型，它包含指向序列中下一个和上一个节点的指针。双链表和循环双链表的区别与单链表和循环链表相同。循环双向链表在第一个节点的前一个字段中不包含 null。

**<u>链表优势</u> :**

*   **动态数据结构:**链表是一种动态排列，因此它可以在运行时通过分配和[解除分配内存](https://www.geeksforgeeks.org/how-to-deallocate-memory-without-using-free-in-c/)来增长和收缩。所以没有必要给出链表的初始大小。
*   **无内存浪费:**在链表中，由于链表的大小在运行时增加或减少，所以可以实现高效的内存利用，因此没有内存浪费，也不需要预分配内存。
*   **实现:**像堆栈和队列这样的线性数据结构通常很容易使用链表来实现。
*   **插入和删除操作:**插入和删除操作在链表中相当容易。在插入或删除一个元素后，不需要移动元素，只需要更新下一个指针中的地址。

**<u>链表的缺点</u> :**

*   **内存使用:**与数组相比，链表需要更多的内存。因为在链表中，还需要一个[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)来存储下一个元素的地址，并且需要额外的内存。
*   **遍历:**在[链表中遍历](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)比数组更耗时。在链表中不能像在按索引排列的数组中那样直接访问元素。例如，要访问位置为 n 的节点，必须遍历它之前的所有节点。
*   **反向遍历:**在单链表中，反向遍历是不可能的，但是在[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)的情况下，反向遍历是可能的，因为它包含一个指向每个节点的先前连接的节点的指针。为了执行这个操作，反向指针需要额外的内存，因此会浪费内存。
*   **随机访问:**由于其[动态内存分配](https://www.geeksforgeeks.org/what-is-dynamic-memory-allocation/)，在链表中不可能进行随机访问。