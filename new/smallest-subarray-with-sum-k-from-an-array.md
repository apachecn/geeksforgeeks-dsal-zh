# 来自数组

的总和为 K 的最小子数组

给定由 **N** 个整数组成的数组 **arr []** ，任务是找到总和等于 **K** 的最小子数组的长度。

**示例**：

> **输入**：arr [] = {2，4，6，10，2，1}，K = 12
> **输出**：2
> **说明：[
> 
> 总和为 12 的所有可能的子数组为{2，4，6}和{10，2}。**
> 
> **输入**：arr [] = {1，2，4，3，2，4，1}，K = 7
> **输出**：2

**天真的方法**：解决该问题的最简单方法是[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并为每个子数组检查其总和是否等于 **K** 。 打印所有此类子数组的最小长度。

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（1）*

**有效方法**：可以使用[前缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术和 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 进一步优化上述方法。 请按照以下步骤解决问题：

1.  计算每个索引的前缀总和，并将其（索引，前缀总和）存储为映射中的键值对。

2.  遍历前缀总和数组，并计算前缀总和与所需总和之间的差。

3.  如果 HashMap 中存在差异值，则意味着存在一个总和等于 **K** 的子数组，然后将子数组的长度与获得的最小长度进行比较，并相应地更新最小长度。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// smallest subarray with sum K
int subArraylen(int arr[], int n, int K)
{
    // Stores the frequency of
    // prefix sums in the array
    unordered_map<int, int> mp;

    mp[arr[0]] = 0;

    for (int i = 1; i < n; i++) {

        arr[i] = arr[i] + arr[i - 1];
        mp[arr[i]] = i;
    }

    // Initialize len as INT_MAX
    int len = INT_MAX;

    for (int i = 0; i < n; i++) {

        // If sum of array till i-th
        // index is less than K
        if (arr[i] < K)

            // No possible subarray
            // exists till i-th index
            continue;

        else {

            // Find the exceeded value
            int x = arr[i] - K;

            // If exceeded value is zero
            if (x == 0)
                len = min(len, i);

            if (mp.find(x) == mp.end())
                continue;
            else {
                len = min(len, i - mp[x]);
            }
        }
    }

    return len;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 3, 2, 4, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int K = 7;

    int len = subArraylen(arr, n, K);

    if (len == INT_MAX) {
        cout << "-1";
    }
    else {
        cout << len << endl;
    }

    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the length of the
// smallest subarray with sum K
static int subArraylen(int arr[], int n, int K)
{
    // Stores the frequency of
    // prefix sums in the array
    HashMap<Integer,
              Integer> mp = new HashMap<Integer,
                                        Integer>();

    mp.put(arr[0], 0);

    for (int i = 1; i < n; i++) 
    {
        arr[i] = arr[i] + arr[i - 1];
        mp.put(arr[i], i);
    }

    // Initialize len as Integer.MAX_VALUE
    int len = Integer.MAX_VALUE;

    for (int i = 0; i < n; i++)
    {

        // If sum of array till i-th
        // index is less than K
        if (arr[i] < K)

            // No possible subarray
            // exists till i-th index
            continue;
        else
        {

            // Find the exceeded value
            int x = K - arr[i];

            // If exceeded value is zero
            if (x == 0)
                len = Math.min(len, i);

            if (mp.containsValue(x))
                continue;
            else
            {
                len = Math.min(len, i );
            }
        }
    }
    return len;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 3, 2, 4, 1 };
    int n = arr.length;

    int K = 7;

    int len = subArraylen(arr, n, K);

    if (len == Integer.MAX_VALUE) 
    {
        System.out.print("-1");
    }
    else
    {
        System.out.print(len + "\n");
    }
}
}

// This code is contributed by Rohit_ranjan

```

## Python3

```py

# Python3 program to implement
# the above approach
from collections import defaultdict
import sys

# Function to find the length of the
# smallest subarray with sum K
def subArraylen(arr, n, K):

    # Stores the frequency of
    # prefix sums in the array
    mp = defaultdict(lambda : 0)

    mp[arr[0]] = 0

    for i in range(1, n):
        arr[i] = arr[i] + arr[i - 1]
        mp[arr[i]] = i

    # Initialize ln 
    ln = sys.maxsize

    for i in range(n):

        # If sum of array till i-th
        # index is less than K
        if(arr[i] < K):

            # No possible subarray
            # exists till i-th index
            continue
        else:

            # Find the exceeded value
            x = K - arr[i]

            # If exceeded value is zero
            if(x == 0):
                ln = min(ln, i)

            if(x in mp.keys()):
                continue
            else:
                ln = min(ln, i - mp[x])

    return ln

# Driver Code
arr = [ 1, 2, 4, 3, 2, 4, 1 ]
n = len(arr)

K = 7

ln = subArraylen(arr, n, K)

# Function call
if(ln == sys.maxsize):
    print("-1")
else:
    print(ln)

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the length of the
// smallest subarray with sum K
static int subArraylen(int []arr, int n, int K)
{
    // Stores the frequency of
    // prefix sums in the array
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    mp.Add(arr[0], 0);

    for (int i = 1; i < n; i++) 
    {
        arr[i] = arr[i] + arr[i - 1];
        mp.Add(arr[i], i);
    }

    // Initialize len as int.MaxValue
    int len = int.MaxValue;

    for (int i = 0; i < n; i++)
    {

        // If sum of array till i-th
        // index is less than K
        if (arr[i] < K)

            // No possible subarray
            // exists till i-th index
            continue;
        else
        {

            // Find the exceeded value
            int x = K - arr[i];

            // If exceeded value is zero
            if (x == 0)
                len = Math.Min(len, i);

            if (mp.ContainsValue(x))
                continue;
            else
            {
                len = Math.Min(len, i );
            }
        }
    }
    return len;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 4, 3, 2, 4, 1 };
    int n = arr.Length;

    int K = 7;

    int len = subArraylen(arr, n, K);

    if (len == int.MaxValue) 
    {
        Console.Write("-1");
    }
    else
    {
        Console.Write(len + "\n");
    }
}
}

// This code is contributed by Rohit_ranjan

```

**Output**

```
2

```

***时间复杂度**：O（NlogN）*

***辅助空间**：O（N）*



* * *

* * *



