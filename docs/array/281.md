# 计算排序数组中的出现次数（或频率）

> 原文： [https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)

给定一个已排序的数组`arr[]`和一个数字`x`，编写一个函数计算`arr[]`中`x`的出现。 预期时间复杂度为`O(Logn)`。

**示例**：

```
  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 2
  Output: 4 // x (or 2) occurs 4 times in arr[]

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 3
  Output: 1 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 1
  Output: 2 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 4
  Output: -1 // 4 doesn't occur in arr[] 
```



**方法 1（线性搜索）**：

线性搜索`x`，计算`x`的出现次数并返回计数。

## C++ 

```cpp

// C++ program to count occurrences of an element 
#include<bits/stdc++.h> 
using namespace std; 

// Returns number of times x occurs in arr[0..n-1] 
int countOccurrences(int arr[], int n, int x) 
{ 
    int res = 0; 
    for (int i=0; i<n; i++) 
        if (x == arr[i]) 
          res++; 
    return res; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 2; 
    cout << countOccurrences(arr, n, x); 
    return 0; 
} 

```