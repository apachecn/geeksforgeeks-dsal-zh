# 程序来查找数组的最小（或最大）元素

> 原文： [https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

给定一个数组，编写函数以查找其中的最小和最大元素。

## C++ 

```cpp

// CPP program to find minimum (or maximum) element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int getMin(int arr[], int n) 
{ 
    int res = arr[0]; 
    for (int i = 1; i < n; i++) 
        res = min(res, arr[i]); 
    return res; 
} 

int getMax(int arr[], int n) 
{ 
    int res = arr[0]; 
    for (int i = 1; i < n; i++) 
        res = max(res, arr[i]); 
    return res; 
} 

int main() 
{ 
    int arr[] = { 12, 1234, 45, 67, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum element of array: " << getMin(arr, n) << "\n"; 
    cout << "Maximum element of array: " << getMax(arr, n); 
    return 0; 
} 

```