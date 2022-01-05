# 奇偶排序/砖块排序的 C/C++程序

> 原文:[https://www . geesforgeks . org/c-c-program-for-奇数-偶数-sort-brick-sort/](https://www.geeksforgeeks.org/c-c-program-for-odd-even-sort-brick-sort/)

这基本上是[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的变体。该算法分为两个阶段——奇数阶段和偶数阶段。该算法一直运行到数组元素被排序，并且在每次迭代中出现两个阶段——奇数阶段和偶数阶段。

在奇数阶段，我们对奇数索引元素执行冒泡排序，在偶数阶段，我们对偶数索引元素执行冒泡排序。

```
// A C++ Program to implement Odd-Even / Brick Sort
#include <bits/stdc++.h>
using namespace std;

// A function to sort the algorithm using Odd Even sort
void oddEvenSort(int arr[], int n)
{
    bool isSorted = false; // Initially array is unsorted

    while (!isSorted) {
        isSorted = true;

        // Perform Bubble sort on odd indexed element
        for (int i = 1; i <= n - 2; i = i + 2) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                isSorted = false;
            }
        }

        // Perform Bubble sort on even indexed element
        for (int i = 0; i <= n - 2; i = i + 2) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                isSorted = false;
            }
        }
    }

    return;
}

// A utility function ot print an array of size n
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << "\n";
}

// Driver program to test above functions.
int main()
{
    int arr[] = { 34, 2, 10, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    oddEvenSort(arr, n);
    printArray(arr, n);

    return (0);
}
```

**输出:**

```
-9 2 10 34

```

详情请参考[奇偶排序/砖块排序](https://www.geeksforgeeks.org/odd-even-sort-brick-sort/)整篇文章！