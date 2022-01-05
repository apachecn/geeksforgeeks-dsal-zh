# 分类术语

> 原文:[https://www.geeksforgeeks.org/sorting-terminology/](https://www.geeksforgeeks.org/sorting-terminology/)

**什么是就地排序？**
就地排序算法使用常数空间来产生输出(仅修改给定的数组)。它只通过修改列表中元素的顺序来对列表进行排序。
例如，插入排序和选择排序是原地排序算法，因为它们不使用任何额外的空间来排序列表，并且合并排序的典型实现不在原地，计数排序的实现也不是原地排序算法。

**什么是内外排序？**
当所有需要排序的数据都无法一次放入内存时，这种排序称为[外部排序](http://en.wikipedia.org/wiki/External_sorting)。外部排序用于海量数据。合并排序及其变体通常用于外部排序。硬盘、光盘等外部存储器用于外部分类。
当所有数据都放在内存中时，那么排序称为内部排序。

**什么是稳定排序？**
参见[稳定排序算法](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论