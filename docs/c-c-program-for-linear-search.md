# 线性搜索的 C/C++程序

> 原文:[https://www . geesforgeks . org/c-c-program-for-linear-search/](https://www.geeksforgeeks.org/c-c-program-for-linear-search/)

**问题:**给定 n 个元素的数组 arr[]，编写一个函数在 arr[]中搜索给定的元素 x。

## C/C++

```
#include <bits/stdc++.h>
using namespace std;

// Linearly search x in arr[].  If x is present then return its
// location,  otherwise return -1
int search(int arr[], int n, int x)
{
    int i;
    for (i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 1, 7, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 4;

    int index = search(arr, n, x);
    if (index == -1)
        cout << "Element is not present in the array";
    else
        cout << "Element found at position " << index;

    return 0;
}
```

**Output:**

```
Element found at position 1

```

上述算法的时间复杂度为 O(n)。

更多详情请参考[线性搜索](https://www.geeksforgeeks.org/linear-search/)整篇文章！