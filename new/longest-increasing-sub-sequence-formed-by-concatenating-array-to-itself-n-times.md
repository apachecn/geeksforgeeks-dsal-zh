# 通过将数组与其自身串联 N 次而形成的最长递增子序列

> 原文：[https://www.geeksforgeeks.org/longest-increasing-sub-sequence-formed-by-concatenating-array-to-itself-n-times/](https://www.geeksforgeeks.org/longest-increasing-sub-sequence-formed-by-concatenating-array-to-itself-n-times/)

给定大小为 **N** 的数组 **arr []** ，任务是找到由 arr 串联而成的数组中[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的长度 []将自身结尾 N 次。

**示例**：[

> **输入**：arr [] = {3，2，1}，N = 3
> **输出**：3
> **解释**：
> 由串联形成的数组–
> {3，2，1，3，2，1，1，3，2，1}
> 该数组可以形成的最长递增子序列的长度为 3，即{1 ，2，3}
> 
> **输入**：N = 3 arr [] = {3，1，4}
> **输出**：
> **说明**：通过串联–
> {3，1，4，3，1，4，3，1，4}
> 该数组可形成的最长递增子序列的长度为 3，即{1，3， 4}

**<u>天真的方法：</u>**

解决此问题的基本方法是通过将给定数组与自身连接 N 次，然后在其中找到最长的递增子序列来创建最终数组 。

**时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：O（N <sup>2</sup> ）

**高效方法**：

根据高效方法，存在于最长递增子序列中的任何元素只能存在一次。 这意味着元素重复 N 次不会影响子序列，但是任何元素都可以随时选择。 因此，在长度为 N 的阵列中找到最长的增长子集是很有效的，这可以通过找到阵列的所有唯一元素来找到。

下面是有效方法的算法：

**算法**：

*   将数组的唯一元素存储在以（元素，计数）作为（键，值）对的映射中。

*   对于数组中的每个元素

    *   如果地图中不存在当前元素，则将其插入地图中，计数为 1。

    *   否则，增加数组中数组元素的数量。

*   找到地图的长度，这将是所需的答案。

**例如**：

> 给定数组为– {4，4，1}
> 创建唯一元素的映射：{（4，2），（1，1）}
> 映射的长度= 2
> 因此，所需的最长 子序列= 2

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the
// longest increasing subsequence 
// in repeating element of array

#include <bits/stdc++.h>
using namespace std;

// Function to find the LCS
int findLCS(int arr[], int n){
    unordered_map<int, int> mp;

    // Loop to create frequency array
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }
    return mp.size();
}

// Driver code
int main()
{
    int n = 3;
    int arr[] = {3, 2, 1};
    cout<<findLCS(arr, n);
    return 0;
}

```

## Java

```java

// Java implementation to find the
// longest increasing subsequence 
// in repeating element of array
import java.util.*;

class GFG{

// Function to find the LCS
static int findLCS(int arr[], int n)
{
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Loop to create frequency array
    for(int i = 0; i < n; i++)
    {
       if(mp.containsKey(arr[i]))
       {
           mp.put(arr[i], mp.get(arr[i]) + 1);
       }
       else
       {
           mp.put(arr[i], 1);
       }
    }
    return mp.size();
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    int arr[] = { 3, 2, 1 };

    System.out.print(findLCS(arr, n));
}
}

// This code is contributed by amal kumar choubey

```

## Python3

```py

# Python3 implementation to find the
# longest increasing subsequence
# in repeating element of array

# Function to find the LCS
def findLCS(arr, n):

    mp = {}

    # Loop to create frequency array
    for i in range(n):
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    return len(mp)

# Driver code
n = 3
arr = [ 3, 2, 1 ]

print(findLCS(arr, n))

# This code is contributed by ng24_7

```

## C#

```cs

// C# implementation to find the
// longest increasing subsequence 
// in repeating element of array
using System;
using System.Collections.Generic;

class GFG{

// Function to find the LCS
static int findLCS(int []arr, int n)
{
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Loop to create frequency array
    for(int i = 0; i < n; i++)
    {
       if(mp.ContainsKey(arr[i]))
       {
           mp[arr[i]] = mp[arr[i]] + 1;
       }
       else
       {
           mp.Add(arr[i], 1);
       }
    }
    return mp.Count;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    int []arr = { 3, 2, 1 };

    Console.Write(findLCS(arr, n));
}
}

// This code is contributed by amal kumar choubey

```

**效果分析**：

*   **时间复杂度**：与上述方法一样，在最坏的情况下只有一个循环占用`O(n)`时间，因此时间复杂度将为 **`O(n)`**。

*   **空间复杂度**：与上述方法一样，使用了一个哈希图，在最坏的情况下可以占用`O(n)`空间，因此空间复杂度将为 **`O(n)`**



* * *

* * *



