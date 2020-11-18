# 单链接列表和双链接列表之间的区别

**单链接列表简介：**单链接列表是一组节点，其中每个节点都有两个字段“数据”和“链接”。 “数据”字段存储实际的一条信息，“链接”字段用于指向下一个节点。 基本上，“链接”字段只不过是地址。

[![linkedlist](img/d97a233bf3c89e80c46e6a3193e851d6.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist.png)

**双链表简介：**一个**双链表**（DLL）包含一个额外的指针，通常称为*前一个指针*，以及那里的下一个指针和数据 在单链表中。

[![dll](img/1fac4717827a04f080fae80f8fd57fe7.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/03/DLL1.png)

<center>**Singly linked list vs Doubly linked list**</center>

| 单链表（SLL） | 双链表（DLL） |

| --- | --- |

| SLL 的节点只有一个数据字段和下一个链接字段。 | DLL 的节点具有数据字段，上一个链接字段和下一个链接字段。 |

| [![linkedlist](img/d97a233bf3c89e80c46e6a3193e851d6.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist.png) | [![dll](img/1fac4717827a04f080fae80f8fd57fe7.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/03/DLL1.png) |

| 在 SLL 中，只能使用下一个节点链接来进行遍历。 | In DLL, the traversal can be done using the previous node link or the next node link. |  |

| 由于 SLL 只有 2 个字段，因此它比 DLL 占用更少的内存。 | DLL 比 SLL 占用更多的内存，因为它具有 3 个字段。 |

| 元素访问效率较低。 | 更有效地访问元素。 |



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。