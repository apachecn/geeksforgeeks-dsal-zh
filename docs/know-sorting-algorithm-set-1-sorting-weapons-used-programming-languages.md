# 了解你的排序算法|集合 1(编程语言使用的排序武器)

> 原文:[https://www . geesforgeks . org/know-sorting-algorithm-set-1-sorting-arms-used-programming-languages/](https://www.geeksforgeeks.org/know-sorting-algorithm-set-1-sorting-weapons-used-programming-languages/)

有没有想过我们在 C++/Java 中使用的 sort()函数或者 Python 中的 sorted()函数是如何在内部工作的？

这里列出了不同编程语言的所有内置排序算法以及它们在内部使用的算法。

1.  **Qport () of C– [Quick sort](https://www.geeksforgeeks.org/quick-sort/)**
    *   Optimal case time complexity-O(NlogN)
    *   Average case time complexity-O(NlogN)
    *   Worse case time complexity-O(N2)
    *   Auxiliary space-O(log N)
    *   Stable-depends on the implementation of the comparator function.
    *   Adaptive-none

[堆排序](https://www.geeksforgeeks.org/heap-sort/)

[插入排序](https://www.geeksforgeeks.org/insertion-sort/)

*   Optimal case time complexity-O(NlogN)
*   Average case time complexity-O(NlogN)
*   Worse case time complexity-O(NlogN)
*   Auxiliary space-O(logN)
*   Stable-none
*   Adaptive-none

*   Auxiliary space-O(N)*   Stable.-Yes*   Adaptive.-Yes*   **Java 6 的数组。sort()–[快速排序](https://www.geeksforgeeks.org/quick-sort/)T3】**
    *   Optimal case time complexity-O(NlogN)
    *   Average case time complexity-O(NlogN)

    [合并排序](https://www.geeksforgeeks.org/merge-sort/)

    [插入排序](https://www.geeksforgeeks.org/insertion-sort/)

    *   Optimal case time complexity-O(N)
    *   Average case time complexity-O(NlogN)
    *   Worse case time complexity-O(NlogN)
    *   Auxiliary space-O(N)
    *   Stable.-Yes
    *   self-adaption
    *   Auxiliary space-O(N)
    *   Stable.-Yes
    *   Adaptive.-Yes

    *   **Sorted ()–timsort of Python (mixed [merge sort](https://www.geeksforgeeks.org/merge-sort/) and [insert sort](https://www.geeksforgeeks.org/insertion-sort/) )**
    *   Optimal case time complexity-O(N)

    [合并排序](https://www.geeksforgeeks.org/merge-sort/)

    [插入排序](https://www.geeksforgeeks.org/insertion-sort/)

    *   Optimal case time complexity-O(N)
    *   Average case time complexity-O(NlogN)
    *   Worse case time complexity-O(NlogN)
    *   Auxiliary space-O(N)
    *   Stable.-Yes

在接下来的几集里，我们将实现 Introsort ( C++的排序武器)和 Sleep sort、Gnome Sort 以及其他非常规的排序算法。

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论