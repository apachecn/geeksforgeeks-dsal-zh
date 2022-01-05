# 排序算法分类

> 原文:[https://www . geeksforgeeks . org/分类排序算法/](https://www.geeksforgeeks.org/classification-of-sorting-algorithms/)

排序是一种算法，它以特定的顺序[升序或降序]排列给定列表的元素。

排序算法根据以下基础分类–

1.  **按比较次数:**
    基于比较的排序算法通过键比较操作检查列表的元素，对于大多数输入至少需要 O(n log n)次比较。在这种方法中，算法根据比较的次数进行分类。对于基于比较的排序算法，最佳情况行为是 O(n log n)，最坏情况行为是 O(n2)。例如–快速排序、冒泡排序、插入排序等。

2.  **按互换数量:**
    在这种方法中，排序算法按互换数量分类(互换到数字的位置，也称为反转)。

3.  **按内存使用情况:**
    一些排序算法已经“就位”，它们需要 O(1)或 O(log n)内存来创建临时排序数据的辅助位置。

4.  **By 递归:**
    排序算法要么是递归的(例如–快速排序)，要么是非递归的(例如–选择排序和插入排序)，有些算法同时使用两者(例如–合并排序)。

5.  **按稳定性:**
    如果两个值相等的元素在输出中出现的顺序与在输入中相同，则排序算法是稳定的。排序算法的稳定性可以通过它如何对待相等的元素来检验。稳定的算法会保持相等元素的相对顺序，而不稳定的排序算法则不会。换句话说，稳定排序保持两个相等元素的位置彼此相似。例如–插入排序、冒泡排序和基数排序。

6.  **By Adaptability :**
    In a few sorting algorithms, the complexity changes based on pre-sorted input i.e. pre-sorted array of the input affects the running time. The algorithms that take this adaptability into account are known to be adaptive algorithms. For example – Quick sort is an adaptive sorting algorithm because the time complexity of Quick sort depends on the  initial input sequence. If input is already sorted then time complexity becomes O(n^2) and if input sequence is not sorted then time complexity becomes O(n logn).

    一些自适应排序算法有:冒泡排序、插入排序和快速排序。另一方面，一些非自适应排序算法是:选择排序、合并排序和堆排序。

7.  **内部排序:**
    在排序过程中专门使用主存的排序算法称为内部排序算法。这种算法假设对所有内存进行高速随机访问。使用此排序功能的一些常见算法有:冒泡排序、插入排序。，和快速排序。

8.  **外部排序:**
    在排序过程中使用外部内存的排序算法属于这一类。它们比内部排序算法相对慢。例如合并排序算法。它对每个适合内存的块进行排序，然后将排序后的块合并在一起。