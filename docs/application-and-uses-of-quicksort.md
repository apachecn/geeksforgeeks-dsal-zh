# 快速排序的应用和用途

> 原文:[https://www . geeksforgeeks . org/application-and-use-of-quick sort/](https://www.geeksforgeeks.org/application-and-uses-of-quicksort/)

[快速排序](https://www.geeksforgeeks.org/quick-sort/):快速排序是一种[分治](https://www.geeksforgeeks.org/divide-and-conquer/)算法，也是最快的[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)。在快速排序中，它创建两个空数组来保存小于枢轴元素的元素和大于枢轴元素的元素，然后[递归](https://www.geeksforgeeks.org/recursion/)排序子数组。Quicksort 有很多版本以不同的方式拾取轴心:

*   Always pick the first element as the pivot.
*   Always select the last element as the pivot.
*   Select a random element as the axis.
*   Take the center line as the fulcrum.

快速排序算法的原理如下:

*   Select any element as **hub** .
*   Divide the array into three parts according to the rules given below:
    *   Part I: All elements of this part should be smaller than the pivot elements.
    *   Part II: Single element, that is, pivot element.
    *   Part III: All elements in this part should be greater than or equal to pivot elements.
*   Then, the algorithm is applied to the first and third parts (recursively).

**下面给出了 Quicksort 的用途和实时应用:**

*   **[business calculation]** It is used in various government and private organizations to sort various data, such as sorting files by name/date/price, sorting students by student number, sorting account files by given id, etc.
*   [Sorting](https://www.geeksforgeeks.org/sorting-algorithms/) algorithm is used for **information search** . Because fast sorting is the fastest algorithm, it is widely used as a better search method.
*   It will be used where **stable sorting** is not needed.
*   Fast sorting is a [cache-friendly](https://www.geeksforgeeks.org/cache-memory-in-computer-organization/) algorithm, because it has good locality of reference when used in arrays.
*   It is **tail recursion** , so all call optimization can be completed.
*   It is sort in place, and does not need any additional storage [memory](https://www.geeksforgeeks.org/introduction-to-memory-and-memory-units/) .
*   Used in operational research and event-driven simulation.
*   In numerical calculation and scientific research, for the accuracy of calculation, most efficiently developed algorithms use priority queue, and quick sorting is used for sorting.

*   Variants are used to separate with the smallest **or** with the largest **.**
*   Methods used to implement primitive types.
*   If the data is sorted, the search information becomes simple and efficient.