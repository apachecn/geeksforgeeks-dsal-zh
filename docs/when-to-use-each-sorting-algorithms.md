# 何时使用各种排序算法

> 原文:[https://www . geeksforgeeks . org/何时使用每次排序算法/](https://www.geeksforgeeks.org/when-to-use-each-sorting-algorithms/)

一个[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)是一个[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)让排列按照一定的顺序进行。基本任务是将项目按所需顺序排列，以便重新排列记录，使[搜索](https://www.geeksforgeeks.org/searching-algorithms/)更容易。
以下是对何时使用哪种排序算法以获得更好性能的逐一描述–

1.  **[Selection Sort](https://www.geeksforgeeks.org/selection-sort/) –**
    This sorting algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array, the subarray which is already sorted and remaining subarray which is unsorted. In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

    我们可以根据以下限制使用选择排序:

    *   当列表很小时。由于选择排序的时间复杂度为 **O(N <sup>2</sup> )** ，对于大列表来说效率不高。
    *   当内存空间有限时，因为它在排序过程中尽可能减少交换次数。

2.  **[Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/) –**
    This sorting algorithm is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order. If we have total **N** elements, then we need to repeat the above process for **N-1** times.

    我们可以按照以下限制使用气泡排序:

    *   它适用于项目几乎已排序的大型数据集，因为它只需要一次迭代来检测列表是否已排序。但是，如果列表在很大程度上没有排序，那么这种算法对于小数据集或列表是有效的。
    *   这种算法在极小或几乎排序的数据集上是最快的。
3.  **[Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/) –**
    This sorting algorithm is a simple sorting algorithm that works the way we sort playing cards in our hands. It places an unsorted element at its suitable place in each iteration.

    我们可以根据以下约束使用插入排序:

    *   如果数据已接近排序，或者列表很小，因为它的复杂性为 **O(N <sup>2</sup> )** ，并且如果列表已排序，则最少数量的元素将滑动到正确的位置插入元素。
    *   该算法稳定，在列表接近排序时运行速度快。
    *   内存的使用是一个限制，因为它具有 0(1)的空间复杂性。
4.  **[Merge Sort](https://www.geeksforgeeks.org/merge-sort/) –**
    This sorting algorithm is based on [Divide and Conquer](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/) algorithm. It divides input array into two halves, calls itself for the two halves, and then merges the two sorted halves.
    The **merge()** function is used for merging two halves. The **merge(arr, l, m, r)** is a key process that assumes that **arr[l..m]** and **arr[m+1..r]** are sorted and merges the two sorted sub-arrays into one.

    我们可以根据以下约束使用合并排序:

    *   当数据结构不支持随机访问时，使用合并排序，因为它使用纯顺序访问，即前向迭代器，而不是随机访问迭代器。
    *   它广泛用于外部排序，与顺序访问相比，随机访问可能非常非常昂贵。
    *   它用于已知数据是相似数据的情况。
    *   在链表的情况下，合并排序很快。
    *   它在链表的情况下使用，就像在链表中访问某个索引处的任何数据一样，我们需要从头遍历到那个索引，合并排序按顺序访问数据，并且随机访问的需求很低。
    *   合并排序的主要优点是它的稳定性，被比较的元素同样保持它们原来的顺序。
5.  **[Quick Sort](https://www.geeksforgeeks.org/quick-sort/) –**
    This sorting algorithm is also based on Divide and Conquer algorithm. It picks an element as pivot and partitions the given list around the picked pivot. After partitioning the list on the basis of the pivot element, the Quick is again applied recursively to two sublists i.e., sublist to the left of the pivot element and sublist to the right of the pivot element.

    我们可以根据以下限制使用快速排序:

    *   快速排序是最快的，但并不总是 **O(N*log N)** ，因为在最坏的情况下，它会变成 **O(N <sup>2</sup> )** 。
    *   快速排序对于适合内存的数据集可能更有效。对于较大的数据集，它被证明是低效的，所以在这种情况下，像合并排序这样的算法是首选。
    *   快速排序是就地排序(即不需要任何额外的存储空间)，因此将其用于阵列是合适的。