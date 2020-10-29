# 所有可能长度的子数组中的最小公共元素

> 原文：[https://www.geeksforgeeks.org/minimum-common-element-in-subarrays-of-all-possible-lengths/](https://www.geeksforgeeks.org/minimum-common-element-in-subarrays-of-all-possible-lengths/)

给定[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，该数组由 **[1，N]** 范围内的 **N** 个整数组成（允许*重复 ]），任务是为每个可能的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)长度找到最小的公共元素。 如果对于任何特定长度的子数组不存在此类元素，则打印 **-1** 。*

**示例**：

> **输入**：arr [] = {1、3、4、5、6、7}
> **输出**：-1 -1 -1 4 3 1
> **说明**：
> K = 1：不存在公共元素。 因此，打印-1。
> K = 2：不存在公共元素。 因此，打印-1。
> K = 3：不存在公共元素。 因此，打印-1。
> K = 4：由于在大小为 4 的所有子阵列中共有 4，因此打印为 4。
> K = 5：由于在大小为 5 的所有子阵列中共有 3 和 4，所以将其最小打印为 3。
> K = 6：打印 1，因为它是数组中的最小元素。
> 
> **输入**：arr []：{1、2、2、2、1}
> **输出**：-1 2 2 1 1

**方法**：请按照以下步骤解决问题：

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将[每个元素](https://www.geeksforgeeks.org/print-the-last-occurrence-of-elements-in-array-in-relative-order/)的最后出现存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

*   初始化数组 **temp []** ，并为每个值存储数组中数组的任意一对连续重复之间的最大距离。

*   完成上述步骤后，通过将 **temp [i]** 与最后出现的 **i** 从阵列末端的距离进行比较，更新 **temp []** 。

*   现在，将长度为 **1** 至 **N** 的所有子数组的最小注释元素一一存储，然后打印出来。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement the 
// above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find maximum distance 
// between every two element 
void max_distance(int a[], int temp[], int n) 
{ 
    // Stores index of last occurence 
    // of each array element 
    map<int, int> mp; 

    // Initialize temp[] with -1 
    for (int i = 1; i <= n; i++) { 
        temp[i] = -1; 
    } 

    // Traverse the array 
    for (int i = 0; i < n; i++) { 

        // If array element has 
        // not occurred previously 
        if (mp.find(a[i]) == mp.end()) 

            // Update index in temp 
            temp[a[i]] = i + 1; 

        // Otherwise 
        else

            // Compare temp[a[i]] with distance 
            // from its previous occurence and 
            // store the maximum 
            temp[a[i]] = max(temp[a[i]], 
                             i - mp[a[i]]); 

        mp[a[i]] = i; 
    } 

    for (int i = 1; i <= n; i++) { 

        // Compare temp[i] with distance 
        // of its last occurence from the end 
        // of the array and store the maximum 
        if (temp[i] != -1) 
            temp[i] = max(temp[i], n - mp[i]); 
    } 
} 

// Function to find the minimum common 
// element in subarrays of all possible lengths 
void min_comm_ele(int a[], int ans[], 
                  int temp[], int n) 
{ 
    // Function call to find a the maximum 
    // distance between every pair of repetition 
    max_distance(a, temp, n); 

    // Initialize ans[] to -1 
    for (int i = 1; i <= n; i++) { 
        ans[i] = -1; 
    } 

    for (int i = 1; i <= n; i++) { 

        // Check if subarray of length 
        // temp[i] contains i as one 
        // of the common elements 
        if (ans[temp[i]] == -1) 
            ans[temp[i]] = i; 
    } 

    for (int i = 1; i <= n; i++) { 

        // Find the minimum of all 
        // common elements 
        if (i > 1 && ans[i - 1] != -1) { 

            if (ans[i] == -1) 
                ans[i] = ans[i - 1]; 
            else
                ans[i] = min(ans[i], 
                             ans[i - 1]); 
        } 

        cout << ans[i] << " "; 
    } 
} 

// Driver Code 
int main() 
{ 
    int N = 6; 
    int a[] = { 1, 3, 4, 5, 6, 7 }; 
    int temp[100], ans[100]; 
    min_comm_ele(a, ans, temp, N); 

    return 0; 
} 

```

**Output:**

```
-1 -1 -1 4 3 1

```

***时间复杂度**：`O(n)`

**辅助空间**：`O(n)`*



* * *

* * *



