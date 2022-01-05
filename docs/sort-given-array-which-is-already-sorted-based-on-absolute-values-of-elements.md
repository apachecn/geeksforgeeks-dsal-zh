# 根据元素的绝对值对已经排序的给定数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-given-array-这是基于元素绝对值的已排序数组/](https://www.geeksforgeeks.org/sort-given-array-which-is-already-sorted-based-on-absolute-values-of-elements/)

给定一个大小为 **N** 的数组 **arr[]** ，根据其元素的绝对值进行排序。任务是根据元素的实际值对这个数组进行排序。

**示例:**

> **输入:** arr[] = {5，-7，10，-11，18}
> **输出:** -11，-7，5，10，18
> **说明:**数组排序时，负值会出现在数组的开头。
> 
> **输入:** arr[] = {1，-2，-3，4，-5}
> **输出:** -5，-3，-2，1，4

**方式:**这个问题可以使用[双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)解决。其思想是从左到右遍历数组，在 deque 的前面插入负元素，在后面插入正元素。现在弹出元素从前面的德奎填补阵列，并得到答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <deque>
#include <iostream>
using namespace std;

// Function to sort
void SortWithoutSorting(int arr[], int N)
{
    deque<int> dq;
    for (int i = 0; i < N; i++) {

        // Pushing negative elements in
        // the front of the deque
        if (arr[i] < 0) {
            dq.push_front(arr[i]);
        }

        // Pushing positive elements in
        // the back of the deque
        else {
            dq.push_back(arr[i]);
        }
    }

    // Preparing the output array
    int i = 0;
    for (auto it = dq.begin(); it != 
         dq.end(); it++)
        arr[i++] = *it;
}

// Function to print the array.
void showArray(int arr[], int N)
{
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, -2, 3, -4, -5, 6 };
    int N = sizeof(arr) / sizeof(int);

    SortWithoutSorting(arr, N);
    showArray(arr, N);
    return 0;
}
```

**Output**

```
-5 -4 -2 1 3 6 
```

***时间复杂度:**T3】O(N)
T5**辅助空间** :* O(N)