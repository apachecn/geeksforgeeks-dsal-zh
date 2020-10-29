# 给定数组中的最小子数组，总和大于或等于 K

> 原文：[https://www.geeksforgeeks.org/smallest-subarray-from-a-given-array-with-sum-greater-than-or-equal-to-k/](https://www.geeksforgeeks.org/smallest-subarray-from-a-given-array-with-sum-greater-than-or-equal-to-k/)

给定由 **N** 个整数和一个整数 **K** 组成的数组 **A []** ，任务是找到总和大于或等于的最小子数组的长度 到 **K** 。 如果不存在这样的子数组，则打印 **-1** 。

**示例**：

> **输入**：A [] = {2，-1，2}，K = 3
> **输出**：3
> **说明**：
> 给定数组的总和为 3。
> 因此，满足所需条件的最小可能子数组是整个数组。
> 因此，长度为 3。
> 
> **输入**：A [] = {2，1，1，-4，3，1，-1，2}，K = 5
> **输出**：4

**天真的方法**：

解决该问题的最简单方法是[生成给定数组的所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查哪个子数组总和大于或等于 **K** 。 在满足条件的所有此类子阵列中，打印具有最小长度的子阵列。

***时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：`O(1)`*

**有效方法**：

可以使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[二进制搜索](http://www.geeksforgeeks.org/binary-search/)进一步优化上述方法。 请按照以下步骤操作：

*   初始化数组以存储原始数组的**前缀和**。

*   [使用](https://www.geeksforgeeks.org/hashing-data-structure/)[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)将前缀和数组与索引混合在一起。

*   如果已经找到具有较小索引的*较大的和，则没有哈希值小于到目前为止所获得的最大前缀和的前缀和的点。 因此，请对前缀和的*递增顺序*进行哈希处理。*

*   遍历数组，如果有任何元素大于或等于 **K** ，则返回 1 作为答案。

*   否则，对于每个元素，对**前缀和数组**中的索引**（i，n-1）**进行**二进制搜索**，以找到总和为第一个索引 至少 **K** 。

*   返回从上述步骤获得的最小长度子数组。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to perform Binary Search 
// and return the smallest index with 
// sum greater than value 
int binary_search(map<int, vector<int> >& m, 
                  int value, int index) 
{ 
    // Search the value in map 
    auto it = m.lower_bound(value); 

    // If all keys in the map 
    // are less then value 
    if (it == m.end()) 
        return 0; 

    // Check if the sum is found 
    // at a greater index 
    auto it1 
        = lower_bound(it->second.begin(), 
                      it->second.end(), index); 

    if ((it1 - it->second.begin()) 
        != it->second.size()) 
        return *it1; 

    return 0; 
} 

// Function to find the smallest subarray 
// with sum greater than equal to K 
int findSubarray(int arr[], int n, int k) 
{ 

    // Prefix sum array 
    int pre_array[n]; 

    // Stores the hashes to prefix sum 
    map<int, vector<int> > m; 

    pre_array[0] = arr[0]; 
    m[pre_array[0]].push_back(0); 

    // If any array element is 
    // greater than equal to k 
    if (arr[0] >= k) 
        return 1; 

    int ans = INT_MAX; 
    for (int i = 1; i < n; i++) { 

        pre_array[i] 
            = arr[i] + pre_array[i - 1]; 

        // If prefix sum exceeds K 
        if (pre_array[i] >= k) 

            // Update size of subarray 
            ans = min(ans, i + 1); 

        auto it = m.rbegin(); 

        // Hash prefix sum in 
        // increasing order 
        if (pre_array[i] >= it->first) 
            m[pre_array[i]].push_back(i); 
    } 

    for (int i = 1; i < n; i++) { 

        int temp 
            = binary_search(m, 
                            pre_array[i - 1] + k, 
                            i); 
        if (temp == 0) 
            continue; 

        // Update size of subarray 
        ans = min(ans, temp - i + 1); 
    } 

    // If any subarray is found 
    if (ans <= n) 
        return ans; 

    // If no such subarray exists 
    return -1; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 2, 1, 1, -4, 3, 1, -1, 2 }; 

    int k = 5; 

    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << findSubarray(arr, n, k) << endl; 

    return 0; 
} 

```

**Output:**

```
4

```

**时间复杂度**：*`O(NlogN)`

**辅助空间**：*`O(n)`**



* * *

* * *



