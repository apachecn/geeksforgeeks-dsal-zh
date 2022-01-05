# 哪种排序算法的内存写入次数最少？

> 原文:[https://www . geesforgeks . org/哪个排序算法产生最小写入次数/](https://www.geeksforgeeks.org/which-sorting-algorithm-makes-minimum-number-of-writes/)

当对一些非常昂贵的大型数据集进行写入时，最大限度地减少写入次数非常有用，例如使用 [EEPROMs](http://en.wikipedia.org/wiki/EEPROM "EEPROM") 或[闪存](http://en.wikipedia.org/wiki/Flash_memory "Flash memory")，每次写入都会缩短内存的使用寿命。

在我们通常在数据结构和算法课程中学习的排序算法中，[选择排序](http://en.wikipedia.org/wiki/Selection_sort)的写入次数最少(它进行 O(n)次交换)。但是，[循环排序](http://en.wikipedia.org/wiki/Cycle_sort)与选择排序相比，几乎总是产生较少的写入次数。在循环排序中，每个值要么被写入零次(如果它已经在正确的位置)，要么被写入一次到正确的位置。这与完成就地排序所需的最小覆盖次数相匹配。

资料来源:[【http://en . Wikipedia . org/wiki/cycle _ sort】](http://en.wikipedia.org/wiki/Cycle_sort)
[【http://en . Wikipedia . org/wiki/selection _ sort】](http://en.wikipedia.org/wiki/Selection_sort)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。