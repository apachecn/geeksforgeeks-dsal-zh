# 来自给定数组

的总和为负的第一个子数组

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是找到第一个子数组的起始索引和结尾索引为负数。 如果不存在这样的子数组，则打印**“ -1”** 。

**注意**：如果给定数组中有多个负和子数组，则第一个子数组是指起始索引最低的子数组。

**示例**：

> **输入**：arr [] = {3，3，-4，-2}
> **输出**：1 2
> **说明**：
> 具有负和的第一个子数组是从索引 1 到索引 2，即 arr [1] + arr [2] = -1。
> 
> **输入**：arr [] = {1、2、3、10}。
> **输出**：-1
> **说明**：
> 不存在负和的子阵列。

**朴素方法**：朴素方法是[从阵列中从左到右生成所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查这些子阵列中的任何一个是否具有负和。 如果是，则打印该子数组的开始和结束索引。

***时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：O（1）*

**有效方法**：的想法是使用[前缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)解决问题。 步骤如下：

1.  计算数组的 **[前缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)** 并将其存储到 **[HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)** 中。

2.  遍历数组，对于第 i 个<sup>索引（其中 i 的范围为 **[0，N – 1]** ），检查第 i 个<sup>索引</sup>的元素是否为 否定的。 如果是这样，则 arr [i]是必需的子数组。</sup>

3.  否则，找到一个从 i +1 开始的索引，其中前缀和小于前缀和，直到 **i** 。

4.  如果在上述步骤中找到任何这样的**索引**，则来自索引 **{i，index}** 的子数组将给出第一个负子数组。

5.  如果找不到这样的子数组，则打印**“ -1”** 。 否则，打印获得的子数组。

下面是上述方法的实现：

## C++

```cpp

// CPP program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check if a sum less 
// than pre_sum is present 
int b_search(int pre_sum, 
             map<int, vector<int> >& m, 
             int index) 
{ 
    // Returns an iterator either equal 
    // to given key or next greater 
    auto it = m.lower_bound(pre_sum); 

    if (it == m.begin()) 
        return -1; 

    // Decrement the iterator 
    it--; 

    // Check if the sum found at 
    // a greater index 
    auto it1 
        = lower_bound(it->second.begin(), 
                      it->second.end(), 
                      index); 

    if (*it1 > index) 
        return *it1; 

    return -1; 
} 

// Function to return the index 
// of first negative subarray sum 
vector<int> findSubarray(int arr[], int n) 
{ 
    // Stores the prefix sum- index 
    // mappings 
    map<int, vector<int> > m; 

    int sum = 0; 

    // Stores the prefix sum of 
    // the original array 
    int prefix_sum[n]; 

    for (int i = 0; i < n; i++) { 
        sum += arr[i]; 

        // Check if we get sum negative 
        // starting from first element 
        if (sum < 0) 
            return { 0, i }; 

        prefix_sum[i] = sum; 
        m[sum].push_back(i); 
    } 

    // Iterate through array find 
    // the sum which is just less 
    // then the previous prefix sum 
    for (int i = 1; i < n; i++) { 

        // Check if the starting element 
        // is itself negative 
        if (arr[i] < 0) 

            // arr[i] becomes the required 
            // subarray 
            return { i, i }; 

        else { 
            int pre_sum = prefix_sum[i - 1]; 

            // Find the index which forms 
            // negative sum subarray 
            // from i-th index 
            int index = b_search(pre_sum, 
                                 m, i); 

            // If a subarray is found 
            // starting from i-th index 
            if (index != -1) 
                return { i, index }; 
        } 
    } 

    // Return -1 if no such 
    // subarray is present 
    return { -1 }; 
} 

// Driver Code 
int main() 
{ 
    // Given array arr[] 
    int arr[] = { 1, 2, -1, 3, -4, 3, -5 }; 

    int n = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    vector<int> res = findSubarray(arr, n); 

    // If subarray does not exist 
    if (res[0] == -1) 
        cout << "-1" << endl; 

    // If the subarray exists 
    else { 
        cout << res[0] 
             << " " << res[1]; 
    } 
    return 0; 
} 

```

**Output:**

```
0 6

```

**时间复杂度**：*O（N * log N）*

**辅助空间**：*O（N）*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



