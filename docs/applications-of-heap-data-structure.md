# 堆数据结构的应用

> 原文:[https://www . geesforgeks . org/applications-of-of-heap-data-structure/](https://www.geeksforgeeks.org/applications-of-heap-data-structure/)

堆数据结构通常是用堆函数教授的。Heapsort 算法的用途有限，因为快速排序在实践中更好。然而，堆数据结构本身被大量使用。以下是 Heapsort 之外的一些用法。

*优先级队列:*优先级队列可以使用 Binary Heap 高效实现，因为它支持 O(logn)时间内的 insert()、delete()和 extractmax()、decreaseKey()操作。二项式堆和斐波那契堆是二进制堆的变体。这些变体也在 0(logn)时间内执行联合，这是二进制堆中的 0(n)操作。堆实现的优先级队列用于图形算法，如[的 Prim 算法](http://en.wikipedia.org/wiki/Prim%27s_algorithm)和[的 Dijkstra 算法](http://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)。

*顺序统计:*堆数据结构可以用来高效地找到数组中第 kth 个最小(或最大)的元素。详见[本](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)帖方法四、六。

参考文献:
[http://net . pku . edu . cn/~ course/cs101/2007/resource/intro 2 algorithm/book 6/chap 07 . htm](http://net.pku.edu.cn/~course/cs101/2007/resource/Intro2Algorithm/book6/chap07.htm)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。