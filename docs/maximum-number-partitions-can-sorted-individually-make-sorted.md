# 可以单独排序来使数组排序的最大分区数

> 原文： [https://www.geeksforgeeks.org/maximum-number-partitions-can-sorted-individually-make-sorted/](https://www.geeksforgeeks.org/maximum-number-partitions-can-sorted-individually-make-sorted/)

给定大小为`n`的数组`arr[]`，以使`arr[]`的元素在`[0, 1, .., n-1]`范围内，其中每个数字最多出现一次。 我们的任务是将数组划分为可以单独排序的最大分区数，然后进行连接以对整个数组进行排序。

**示例**：

```
Input : arr[] = [2, 1, 0, 3]
Output : 2
If divide arr[] into two partitions
{2, 1, 0} and {3}, sort then and concatenate
then, we get the whole array sorted.

Input : arr[] = [2, 1, 0, 3, 4, 5]
Output : 4
The maximum number of partitions are four, we
get these partitions as {2, 1, 0}, {3}, {4} 
and {5}

```



这个想法基于这样一个事实，即如果`i`处的元素最大为前缀`arr[0..i]`，那么我们可以创建一个以`i`结尾的分区。

## C++ 

```cpp

// CPP program to find Maximum number of partitions 
// such that we can get a sorted array. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find maximum partitions. 
int maxPartitions(int arr[], int n) 
{ 
    int ans = 0, max_so_far = 0; 
    for (int i = 0; i < n; ++i) { 

        // Find maximum in prefix arr[0..i] 
        max_so_far = max(max_so_far, arr[i]); 

        // If maximum so far is equal to index, 
        // we can make a new partition ending at 
        // index i. 
        if (max_so_far == i) 
            ans++; 
    } 
    return ans; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 0, 2, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << maxPartitions(arr, n); 
    return 0; 
} 

```