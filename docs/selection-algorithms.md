# 选择算法

> 原文:[https://www.geeksforgeeks.org/selection-algorithms/](https://www.geeksforgeeks.org/selection-algorithms/)

选择算法是一种在列表或[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中寻找第 k 个最小(或最大)数的算法。这个数字叫做 **kth 订单统计**。它包括在列表或[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中寻找最小、最大和中间元素的各种情况。为了通过遍历列表找到最小(或最大)元素，我们跟踪到目前为止出现的当前最小(或最大)元素，它与[选择排序](https://www.geeksforgeeks.org/selection-sort/)相关。
以下是在无序列表中选择第 k 个最小(或最大)元素的不同方法:

1.  **通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)**
    [排序](https://www.geeksforgeeks.org/sorting-algorithms/)列表或[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)进行选择，然后选择所需的元素可以使选择变得容易。这种方法对于选择单个元素是低效的，但是当需要从一个数组中进行许多选择时，它是高效的，因为它只需要对一个数组进行排序。因为链表中的选择是 **O(n)** 即使[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)由于缺少随机访问而被排序。
    不用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)整个列表或者一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，我们可以使用[部分排序](https://www.geeksforgeeks.org/stdpartial_sort-in-cpp/)选择列表或者一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中第 kth 个最小(或者最大)的元素。那么第 k 个最小(或最大)的元素就是部分排序列表中最大(或最小)的元素。这需要**0(1)**在数组中访问，而**0(k)**在列表中访问。
    *   **无序部分排序**
        无序部分[排序](https://www.geeksforgeeks.org/sorting-algorithms/)是一种[排序](https://www.geeksforgeeks.org/sorting-algorithms/)算法，前 k 个元素按排序顺序排列，其余元素按随机顺序排列。寻找第 k 个最小(或最大)元素。时间复杂度降低到 **O(k log k)** 。但由于 K ≤ n，渐近时间复杂度收敛到 **O(n)** 。
        **注意:**由于元素相等的可能性，在对列表或[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)进行排序时，不能包含小于或等于第 kth 个元素的元素，因为大于第 kth 个元素的元素也可能等于第 kth 个最小元素。
    *   **部分[选择排序](https://www.geeksforgeeks.org/selection-sort/)**
        在[选择排序](https://www.geeksforgeeks.org/selection-sort/)中使用的概念帮助我们将数组部分排序到第 k 个最小(或最大)元素，以找到数组中第 k 个最小(或最大)元素。因此，部分选择排序产生一个简单的选择算法，该算法花费 **O(k*n)** 时间来排序[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)。这是渐近低效的，但是如果 k 很小，则可以足够高效，并且易于实现。
        以下是部分[选择排序](https://www.geeksforgeeks.org/selection-sort/)的算法:

        ```
        function partialSelectionSort(arr[0..n], k) {
            for i in [0, k) {
                minIndex = i
                minValue = arr[i]
                for j in [i+1, n) {
                    if (arr[j] < minValue)  then
                        minIndex = j
                        minValue = arr[j]
                        swap(arr[i], arr[minIndex])
                }  
            }
            return arr[k]
        }

        ```

2.  **基于分区的选择**
    对于基于分区的选择，使用[快速选择算法](https://www.geeksforgeeks.org/quickselect-algorithm/)。它是[快速排序](https://www.geeksforgeeks.org/quick-sort/)算法的变种。在这两种情况下，我们选择一个枢轴元素，并使用[快速排序](https://www.geeksforgeeks.org/quick-sort/)算法中的分割步骤，将所有小于枢轴的元素排列在其左侧，大于枢轴的元素排列在其右侧。
    但是当[快速排序](https://www.geeksforgeeks.org/quick-sort/)在分区的两侧递归时，[快速选择](https://www.geeksforgeeks.org/quickselect-algorithm/)仅在一侧递归，即存在所需 kth 元素的一侧。
    基于分区的算法已经到位，导致数据部分排序。可以不改变原始数据，以 **O(n)** 辅助空间为代价，进行错位。
3.  **中值选择作为枢轴**
    中值选择算法可用于执行选择算法或排序算法，方法是在[快速选择](https://www.geeksforgeeks.org/quickselect-algorithm/)或[快速选择](https://www.geeksforgeeks.org/quick-sort/)算法中选择数组的中值作为枢轴元素。
    在实践中，中枢计算的开销很大，因此通常不使用这些算法，但是这种技术在关联选择和排序算法中具有理论意义。
    数组的中值是数组排序的最佳支点，因为它将数据平均分成两部分。，从而保证最佳排序，假设选择算法是最佳的。