# 堆排序在实际应用中的位置？

> 原文:[https://www . geesforgeks . org/where-is-heap-sort-used-practic/](https://www.geeksforgeeks.org/where-is-heap-sort-used-practically/)

虽然[快速排序](https://www.geeksforgeeks.org/quick-sort/)在实践中效果更好，但是[堆排序](https://www.geeksforgeeks.org/heap-sort/)的优势是 O(nLogn)的最坏情况上限。

[MergeSort](https://www.geeksforgeeks.org/merge-sort/) 也有作为 O(nLogn)的上限，与 HeapSort 相比，在实践中效果更好。但是合并排序需要额外的空间

HeapSort 在实践中使用不多，但在可用空间较少(MergeSort 不适合)的实时(或快速排序不适合的时间限制)嵌入式系统中可能很有用。请参考[介绍](https://www.geeksforgeeks.org/introsort-or-introspective-sort/)举例

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论