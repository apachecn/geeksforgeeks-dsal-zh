# 所有排序算法的时间复杂度

> 原文:[https://www . geeksforgeeks . org/time-所有排序算法的复杂性/](https://www.geeksforgeeks.org/time-complexities-of-all-sorting-algorithms/)

算法的效率取决于两个参数:

1.时间复杂性

2.空间复杂性

**时间复杂度:**时间复杂度定义为特定指令集执行的次数，而不是总时间。这是因为花费的总时间还取决于一些外部因素，如使用的编译器、处理器的速度等。

**空间复杂度:**空间复杂度是程序执行所需的总内存空间。

两者都是作为输入大小(n)的函数计算的。

这里重要的一点是，尽管有这些参数，算法的效率也取决于**输入的**性质**和**大小**。**

下面是一个快速修订表，你可以在最后一刻参考

<figure class="table">

| **算法** | **时间复杂度** |   |
| --- | --- | --- |
|   | **最佳** | **平均值** | **最差** |   |
| --- | --- | --- | --- | --- |
| [选择排序](http://geeksquiz.com/selection-sort/) | Ω（n^2） | θ（n^2） | O(n^2) |   |
| [气泡排序](http://geeksquiz.com/bubble-sort/) | Ω（n） | θ（n^2） | O(n^2) |   |
| [插入输出](http://geeksquiz.com/insertion-sort/) | Ω（n） | θ（n^2） | O(n^2) |   |
| [堆排序](http://geeksquiz.com/heap-sort/) | Ω（n log（n）） | θ（n log（n）） | O(n 对数(n)) |   |
| [快速排序](http://geeksquiz.com/quick-sort/) | Ω（n log（n）） | θ（n log（n）） | O(n^2) |   |
| [合并排序](http://geeksquiz.com/merge-sort/) | Ω（n log（n）） | θ（n log（n）） | O(n 对数(n)) |   |
| [桶排序](https://www.geeksforgeeks.org/bucket-sort-2/) | Ω（n+k） | θ(n+k) | O(n^2) |   |
| [基数排序](https://www.geeksforgeeks.org/radix-sort/) | ω(NK) | ο(消歧义) | O(nk) |   |
| 计数排序 | Ω（n+k） | θ(n+k) | O(n+k) |   |

另外，请参见:

*   [搜索和整理文章](https://www.geeksforgeeks.org/fundamentals-of-algorithms/#SearchingandSorting)
*   [上一年 GATE 关于排序的问题](https://www.geeksforgeeks.org/algorithms-gq/searching-and-sorting-gq/)

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

</figure>