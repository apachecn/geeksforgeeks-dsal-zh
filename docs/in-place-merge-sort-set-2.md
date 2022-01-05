# 就地合并排序|集合 2

> 原文:[https://www.geeksforgeeks.org/in-place-merge-sort-set-2/](https://www.geeksforgeeks.org/in-place-merge-sort-set-2/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是[使用](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)[就地合并排序](https://www.geeksforgeeks.org/in-place-merge-sort/)以递增的顺序对数组进行排序。

**示例:**

> **输入:** A = {5，6，3，2，1，6，7}
> 输出: {1，2，3，5，6，6，7}
> 
> **输入:** A = {2，3，4，1}
> **输出:** {1，2，3，4}

**方法:**想法是使用 [**inplace_merge()**](https://www.geeksforgeeks.org/merge-operations-using-stl-in-c-merge-includes-set_union-set_intersection-set_difference/) 函数来[合并 O(1)空间](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)中的排序数组。按照以下步骤解决问题:

*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **mergeSort()** ，该函数接受[数组](https://www.geeksforgeeks.org/array-data-structure/)的开始和结束索引作为参数。现在，执行以下步骤:
    *   如果[数组](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)的大小等于 1，只需[退出功能](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)。
    *   否则，计算中间索引，将阵列分成两个子阵列。
    *   递归调用左右子阵上的 **mergeSort()** ，分别进行排序。
    *   然后，调用 [**inplace_merge()**](https://www.geeksforgeeks.org/merge-operations-using-stl-in-c-merge-includes-set_union-set_intersection-set_difference/) 函数合并两个子阵列。
*   完成以上步骤后，[打印排序后的数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **A[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define it vector<int>::iterator
using namespace std;

// Recursive function to split the array
// into two subarrays and sort them
void mergeSortUtil(it left, it right)
{
    // Handle the base case
    if (right - left <= 1)
        return;

    // Otherwise, find the middle index
    it mid = left + (right - left) / 2;

    // Recursively sort
    // the left subarray
    mergeSortUtil(left, mid);

    // Recursively sort
    // the right subarray
    mergeSortUtil(mid, right);

    // Merge the two sorted arrays using
    // inplace_merge() function
    inplace_merge(left, mid, right);

    return;
}

// Function to sort the array
// using inplace Merge Sort
void mergeSort(vector<int> arr)
{
    // Recursive function to sort the array
    mergeSortUtil(arr.begin(), arr.end());

    // Print the sorted array
    for (int el : arr)
        cout << el << " ";
}

// Driver Code
int main()
{
    vector<int> arr = { 5, 6, 3, 2, 1, 6, 7 };

    mergeSort(arr);

    return 0;
}
```

**Output:** 

```
1 2 3 5 6 6 7
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*

**替代方法:**关于解决这个问题的其他方法，请参考[上一篇文章](https://www.geeksforgeeks.org/in-place-merge-sort/)。