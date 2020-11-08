# 最大子数组，所有元素的频率相同

> 原文：[https://www.geeksforgeeks.org/largest-subarray-with-frequency-of-all-elements-same/](https://www.geeksforgeeks.org/largest-subarray-with-frequency-of-all-elements-same/)

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)`arr[]`，任务是找到所有子元素的频率相同的最大子数组的大小。

**示例**：

> **输入**：`arr[] = {1, 2, 2, 5, 6, 5, 6}`
>
> **输出**：6
>
> **说明**：
>
> `subarrary = {2, 2, 5, 5, 6, 5}`的每个元素的频率为 2。
> 
> **输入**：`arr[] = {1, 1, 1, 1, 1}`
>
> **输出**：5
>
> **说明**：
>
> `subarrary = {1, 1, 1, 1, 1}`的每个元素的频率为 5。

**方法**：的想法是[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查每个子数组是否有任何子数组具有所有元素的频率。 步骤如下：

1.  生成所有可能的子数组。

2.  对于每个子数组，取两个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，一个映射存储每个元素的频率，第二个映射存储给定频率的元素数量。

3.  如果对于任何子数组，第二个图的大小等于 **1** ，则意味着每个元素在子数组中的频率相同。

4.  返回所有此类子数组的最大大小。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <iostream> 
#include <unordered_map> 
using namespace std; 

// Function to find maximum subarray size 
int max_subarray_size(int N, int arr[]) 
{ 
    int ans = 0; 

    // Generating all subarray 
    // i -> starting index 
    // j -> end index 
    for (int i = 0; i < N; i++) { 

        // Map 1 to hash frequency 
        // of all elements in subarray 
        unordered_map<int, int> map1; 

        // Map 2 to hash frequency 
        // of all frequencies of 
        // elements 
        unordered_map<int, int> map2; 

        for (int j = i; j < N; j++) { 

            // ele_count is the previous 
            // frequency of arr[j] 
            int ele_count; 

            // Finding previous frequency of 
            // arr[j] in map 1 
            if (map1.find(arr[j]) 
                == map1.end()) { 
                ele_count = 0; 
            } 
            else { 
                ele_count = map1[arr[j]]; 
            } 

            // Increasing frequency of arr[j] 
            // by 1 
            map1[arr[j]]++; 

            // Check if previous frequency 
            // is present in map 2 
            if (map2.find(ele_count) 
                != map2.end()) { 

                // Delete previous frequency 
                // if hash is equal to 1 
                if (map2[ele_count] == 1) { 
                    map2.erase(ele_count); 
                } 
                else { 

                    // Decrement the hash of 
                    // previous frequency 
                    map2[ele_count]--; 
                } 
            } 

            // Incrementing hash of new 
            // frequency in map 2 
            map2[ele_count + 1]++; 

            // Check if map2 size is 1 
            // and updating answer 
            if (map2.size() == 1) 
                ans = max(ans, j - i + 1); 
        } 
    } 

    // Return the maximum size of subarray 
    return ans; 
} 

// Driver Code 
int main() 
{ 
    // Given array arr[] 
    int arr[] = { 1, 2, 2, 5, 6, 5, 6 }; 

    int N = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    cout << max_subarray_size(N, arr); 
    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度**：*`O(N ^ 2)`*

**辅助空间**：*`O(1)`*



* * *

* * *



