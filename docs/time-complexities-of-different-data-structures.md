# 不同数据结构的时间复杂度

> 原文:[https://www . geeksforgeeks . org/不同数据结构的时间复杂性/](https://www.geeksforgeeks.org/time-complexities-of-different-data-structures/)

[时间复杂度](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)是计算机科学中的一个概念，处理一组代码或[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)处理或运行所花费的时间量的量化，作为输入量的函数。换句话说，时间复杂度是程序处理给定输入所需的时间。算法的效率取决于两个参数:

*   时间复杂性
*   空间复杂性

**时间复杂度:**定义为特定指令集执行的次数，而不是总耗时。这是因为花费的总时间还取决于一些外部因素，如使用的编译器、处理器的速度等。

**空间复杂度:**是程序执行所需的总内存空间。

### **<u>不同操作的不同数据结构的平均时间复杂度</u>**

<figure class="table">

| **数据结构** | **进入** | **搜索** | 插入 | **删除** |
| **阵列** | O(1) | O(N) | O(N) | O(N) |
| **堆叠** | O(N) | O(N) | O(1) | O(1) |
| 队列 | O(N) | O(N) | O(1) | O(1) |
| **单链表** | O(N) | O(N) | O(1) | O(1) |
| **双向链表** | O(N) | O(N) | O(1) | O(1) |
| **散列表** | O(1) | O(1) | O(1) | O(1) |
| **二叉查找树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |
| **AVL 树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |
| **B 树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |
| **红黑树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |

</figure>

### **<u>不同操作不同数据结构的最坏情况时间复杂度</u>**

<figure class="table">

| **数据结构** | **进入** | **搜索** | 插入 | **删除** |
| **阵列** | O(1) | O(N) | O(N) | O(N) |
| **堆叠** | O(N) | O(N) | O(1) | O(1) |
| 队列 | O(N) | O(N) | O(1) | O(1) |
| **单链表** | O(N) | O(N) | O(1) | O(1) |
| **双向链表** | O(N) | O(N) | O(1) | O(1) |
| **散列表** | O(N) | O(N) | O(N) | O(N) |
| **二叉查找树** | O(N) | O(N) | O(N) | O(N) |
| **AVL 树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |
| **二叉树** | O(N) | O(N) | O(N) | O(N) |
| **红黑树** | o(对数 N) | o(对数 N) | o(对数 N) | o(对数 N) |

</figure>