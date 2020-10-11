# 查找是否有一个总和为 0 的子数组

> 原文： [https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/](https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/)

给定一个正负数数组，请查找是否存在一个总和为 0 的子数组（大小至少为一个）。

**示例**：

```
Input: {4, 2, -3, 1, 6}
Output: true 
There is a subarray with zero sum from index 1 to 3.

Input: {4, 2, 0, 1, 6}
Output: true 
There is a subarray with zero sum from index 2 to 2.

Input: {-3, 2, 3, 1, 6}
Output: false
There is no subarray with zero sum.

```



**简单解决方案**是一个个地考虑所有子数组，并检查每个子数组的总和。 我们可以运行两个循环：外部循环选择起始点`i`，内部循环尝试从`i`开始的所有子数组（有关实现，请参见[这里](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)）。 该方法的时间复杂度为 `O(n^2)`。

我们还可以**使用哈希**。 想法是遍历数组，对于每个元素`arr[i]`，计算从 0 到`i`的元素总和（这可以简单地通过`sum += arr[i]`来完成）。 如果当前总和是以前看过的，则有一个零总和数组。 散列用于存储总和值，以便我们可以快速存储总和并找出当前总和是否之前被查看过。

范例：

```
arr[] = {1, 4, -2, -2, 5, -4, 3}

If we consider all prefix sums, we can
notice that there is a subarray with 0
sum when :
1) Either a prefix sum repeats or
2) Or prefix sum becomes 0.

Prefix sums for above array are:
1, 5, 3, 1, 6, 2, 5

Since prefix sum 1 repeats, we have a subarray
with 0 sum. 

```

以下是上述方法的实现。

## C++ 

```cpp

// A C++ program to find if there is a zero sum 
// subarray 
#include <bits/stdc++.h> 
using namespace std; 

bool subArrayExists(int arr[], int n) 
{ 
    unordered_set<int> sumSet; 

    // Traverse through array and store prefix sums 
    int sum = 0; 
    for (int i = 0 ; i < n ; i++) 
    { 
        sum += arr[i]; 

        // If prefix sum is 0 or it is already present 
        if (sum == 0 || sumSet.find(sum) != sumSet.end()) 
            return true; 

        sumSet.insert(sum); 
    } 
    return false; 
} 

// Driver code 
int main() 
{ 
    int arr[] =  {-3, 2, 3, 1, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    if (subArrayExists(arr, n)) 
        cout << "Found a subarray with 0 sum"; 
    else
        cout << "No Such Sub Array Exists!"; 
    return 0; 
} 

```