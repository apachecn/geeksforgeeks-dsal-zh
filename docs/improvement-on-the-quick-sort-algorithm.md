# 快速排序算法的改进

> 原文:[https://www . geeksforgeeks . org/快速排序算法改进/](https://www.geeksforgeeks.org/improvement-on-the-quick-sort-algorithm/)

**先决条件:** [快速排序算法](https://www.geeksforgeeks.org/quick-sort/)

本文讨论的快速排序算法在最坏的情况下可以取*T3】O(N<sup>2</sup>)*时间。因此，需要某些能够有效划分阵列并围绕枢轴重新排列元素的变体。

**<u>单轴分区</u> :** 在单轴分区中，数组 **A[]** 可以分为 **{A[p]，A[p + 1]，A[p + 2]，…，A[r]}** 两部分 **A[p…q]** 和 **A[q+1…r]** 这样:

*   All elements in the first partition, **a [p … q]**
*   All elements in the second partition, **a [q+1 … r]** are greater than or equal to the pivot value **a [q]** .
*   After that, the two partitions are regarded as independent input arrays and feed themselves to the **quick sort** .

**<u>洛木托的分区</u> :** 这是实现起来最简单的分区程序。从最左边的元素开始，跟踪较小(或等于)元素的索引，如 **i** 。遍历时，如果发现一个较小的元素，用**A【I】**交换当前元素。否则，忽略当前元素。

在[这篇](https://www.geeksforgeeks.org/quick-sort/)文章中有详细讨论。

**<u>霍尔的分区</u> :** 它的工作原理是初始化两个从两端开始的索引，这两个索引相向移动，直到找到一个反转(左侧的值较小，右侧的值较大)。当发现反转时，交换两个值并重复该过程。**霍尔的分区方案**比**洛木托的分区方案**效率更高，因为它的交换次数平均减少了三倍，即使所有值都相等，它也能创建高效的分区。

**Lomuto 的**和 **Hoare 的**划分的比较在这里[详细讨论](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)。

[**<u>【随机旋转】</u>**](https://www.geeksforgeeks.org/quicksort-using-random-pivoting/) **:** 在上述两种方法中，思想是取未探索数组的第一个或最后一个元素，并找到该元素在数组中的正确位置，将其视为旋转点。如果数组已经按照递增或递减的顺序排序，并且第一个元素总是被选为轴心，那么它将总是未探索的数组元素中的[最大或最小元素](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)。它将未探索数组的大小仅减少 1，因此可以使快速排序算法执行***O(N<sup>2</sup>)***的最坏情况时间复杂度。

不是每次都选择第一个元素作为轴心，如果我们从未探索的数组中选择一个随机元素，并将其与第一个元素交换，然后执行分区过程(上面两个中的任何一个)，那么它将把预期的或平均的时间复杂度提高到 ***O(N*log N)*** 。最坏情况下的复杂性仍然是 ***O(N <sup>2</sup> )*** 。虽然，当数组已经被排序时，最坏的情况被避免，但是当数组包含许多重复的元素时，最坏的情况被命中。

要了解随机化算法如何提高平均案例时间复杂度，请参考本文。

**<u>重复元素的性能</u> :** 考虑一个数组 **arr[] = [3，3，3，3，3]** ，即数组中有所有(或许多)相等的元素。在用单轴分区方案对这个数组进行分区时，我们将得到两个分区。第一个分区将为空，而第二个分区将具有**(N–1)个元素**。此外，分区过程的每次后续调用将只减少一个输入大小。由于分区程序具有 ***O(N)*** 的复杂度，因此整体时间复杂度将为***O(N<sup>2</sup>)***。当输入数组有许多重复的元素时，这是最坏的情况。

为了减少重复元素大量出现时的最坏情况，我们可以实现一个三向分区方案，而不是单轴分区方案。

**<u>三向分区</u> :** 为了高效地对重复键数量较多的数组进行排序，我们可以在第一次遇到键时将其放置在正确的位置。所以数组的三向分区由以下三个分区组成:

*   The leftmost partition contains elements that are strictly smaller than the axis.
*   The middle partition contains all elements equal to the pivot.
*   The rightmost partition contains all elements strictly larger than the pivot.

[**<u>荷兰国旗(DNF)排序算法</u>**](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/) **:** 它可以将一个数组的所有数字相对于给定的枢轴分为三组:

*   The **Tiny** group contains all elements that are strictly smaller than the pivot.
*   The **Equal** group contains all elements equal to the pivot.
*   **The group greater than** contains all elements strictly greater than the pivot.

要解决 DNF 问题，选择第一个元素作为轴心，从左到右扫描数组。当我们检查每个元素时，我们将其移动到正确的组，即**较小的**、**相等的**和**较大的**。

要了解 DNF 排序算法的实现，请参考本文。

**<u>宾利-麦克洛伊的优化 3 路划分</u> :** 这个算法是一个基于**迭代的划分方案**。数组的所有元素最初都没有被探索过。从左右方向开始探索数组的元素。每次迭代后，可以将数组可视化为五个区域的组合:

*   The extremes are areas where the elements are equal to the pivot value.
*   The unexplored area stays in the center, and its size decreases with each iteration.
*   On the left side of the unexplored area are elements smaller than the pivot value.
*   On the right side of the unexplored area are elements larger than the pivot value.

随着迭代过程的继续，数组中未探索的区域不断减少，最后，数组中将没有剩余的未探索元素。

现在，由于与枢轴元素相等的元素大于较小区域中的元素，小于较大区域中的元素，因此它们需要移动到较小区域和较大区域之间的中心。它们通过与较小和较大区域的元素交换而被带到中心。

最后，问题简化为再次使用相同的方法在较小和较大的区域中对元素进行排序，直到整个数组被排序。

**<u>三向划分分析</u> :** 一般来说，快速排序算法的平均情况时间复杂度为 O(N*log(N))，最坏情况时间复杂度为 ***O(N <sup>2</sup> )*** 。对于大量的重复键，我们总是通过快速排序的简单实现获得最差的性能。

然而，使用三向分区减少了大量重复键的影响。事实上，一个包含所有元素的数组在单轴分区中是按照***【O(N)<sup>2</sup>)***时间排序的，而在三轴分区中是按照***【O(N)***(线性)时间复杂度排序的。因此，过去最糟糕的情况变成了三向分区的最佳情况。