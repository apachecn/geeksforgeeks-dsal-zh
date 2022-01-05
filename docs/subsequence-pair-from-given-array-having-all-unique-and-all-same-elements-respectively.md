# 给定数组的子序列对分别具有所有唯一和所有相同的元素

> 原文:[https://www . geeksforgeeks . org/subsequence-pair-from-给定数组-分别具有全部唯一和全部相同的元素/](https://www.geeksforgeeks.org/subsequence-pair-from-given-array-having-all-unique-and-all-same-elements-respectively/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是选择两个长度相等的子序列，使得第一个子序列必须具有所有唯一的元素，第二个子序列必须具有所有相同的元素。打印子序列对的最大长度。

**示例:**

> **输入:** arr[] = {1，2，3，1，2，3，3}
> **输出:** 3
> **解释:**
> 第一个子序列由元素{1，2，3}组成。
> 第二子序列由元素{3，3，3}组成。
> 
> **输入:** arr[] = {2，2，2，3}
> **输出:** 2
> **解释:**
> 第一个子序列由元素{2，3}组成。
> 第二子序列由元素{2，2}组成。

**进场:**

1.  计算给定数组中元素的最大频率(比如 **f** )。
2.  计算数组中存在的不同元素(比如 **d** )。
3.  要使两个子序列的长度与给定的属性相等，那么第一个子序列的大小不能超过 **d** ，第二子序列的大小不能超过 **f** 。
4.  子序列的最大值是基于以下两种情况给出的:
    *   具有不同元素的子序列必须具有最大频率的元素。因此， **(d，f–1)**的最小值是具有给定性质的子序列的可能长度。
    *   如果具有不同元素的子序列的长度大于最大频率，那么**(d–1，f)** 的最小值就是具有给定性质的子序列的可能长度。
5.  以上两种情况下的最大值是具有给定属性的子序列的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// of subsequences with given property
int maximumSubsequence(int arr[], int N)
{
    // To store the frequency
    unordered_map<int, int> M;

    // Traverse the array to store the
    // frequency
    for (int i = 0; i < N; i++) {
        M[arr[i]]++;
    }

    // M.size() given count of distinct
    // element in arr[]
    int distinct_size = M.size();
    int maxFreq = 1;

    // Traverse map to find max frequency
    for (auto& it : M) {

        maxFreq = max(maxFreq, it.second);
    }

    // Find the maximum length on the basis
    // of two cases in the approach

    cout << max(min(distinct_size, maxFreq - 1),
                min(distinct_size - 1, maxFreq));
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 4, 4, 4, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    maximumSubsequence(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum length
// of subsequences with given property
static void maximumSubsequence(int arr[], int N)
{

    // To store the frequency
    HashMap<Integer,
            Integer> M = new HashMap<Integer,
                                     Integer>();

    // Traverse the array to store the
    // frequency
    for(int i = 0; i < N; i++)
    {
        if(M.containsKey(arr[i]))
        {
            M.put(arr[i], M.get(arr[i]) + 1);
        }
        else
        {
            M.put(arr[i], 1);
        }
    }

    // M.size() given count of distinct
    // element in arr[]
    int distinct_size = M.size();
    int maxFreq = 1;

    // Traverse map to find max frequency
    for(Map.Entry<Integer, Integer> it : M.entrySet())
    {
        maxFreq = Math.max(maxFreq, it.getValue());
    }

    // Find the maximum length on the basis
    // of two cases in the approach

    System.out.print(Math.max(
        Math.min(distinct_size, maxFreq - 1),
        Math.min(distinct_size - 1, maxFreq)));
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 4, 4, 4, 4, 5 };
    int N = arr.length;

    // Function call
    maximumSubsequence(arr, N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum length
# of subsequences with given property
def maximumSubsequence(arr, N):

    # To store the frequency
    M = {i : 0 for i in range(100)}

    # Traverse the array to store the
    # frequency
    for i in range(N):
        M[arr[i]] += 1

    # M.size() given count of distinct
    # element in arr[]
    distinct_size = len(M)
    maxFreq = 1

    # Traverse map to find max frequency
    for value in M.values():
        maxFreq = max(maxFreq, value)

    # Find the maximum length on the basis
    # of two cases in the approach

    print(max(min(distinct_size,  maxFreq - 1),
          min(distinct_size - 1, maxFreq)))

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 4, 4, 4, 5 ]
    N = len(arr)

    # Function call
    maximumSubsequence(arr, N)

# This code is contributed by Samarth
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum length
// of subsequences with given property
static void maximumSubsequence(int []arr, int N)
{

    // To store the frequency
    Dictionary<int,
               int> M = new Dictionary<int,
                                       int>();

    // Traverse the array to store the
    // frequency
    for(int i = 0; i < N; i++)
    {
        if(M.ContainsKey(arr[i]))
        {
            M[arr[i]] =  M[arr[i]] + 1;
        }
        else
        {
            M.Add(arr[i], 1);
        }
    }

    // M.Count given count of distinct
    // element in []arr
    int distinct_size = M.Count;
    int maxFreq = 1;

    // Traverse map to find max frequency
    foreach(KeyValuePair<int, int> m in M)
    {
        maxFreq = Math.Max(maxFreq, m.Value);
    }

    // Find the maximum length on the basis
    // of two cases in the approach

    Console.Write(Math.Max(
        Math.Min(distinct_size, maxFreq - 1),
        Math.Min(distinct_size - 1, maxFreq)));
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 4, 4, 4, 4, 5 };
    int N = arr.Length;

    // Function call
    maximumSubsequence(arr, N);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum length
// of subsequences with given property
function maximumSubsequence(arr, N) {
    // To store the frequency
    let M = new Map();

    // Traverse the array to store the
    // frequency
    for (let i = 0; i < N; i++) {
        if (M.has(arr[i])) {
            M.set(arr[i], M.get(arr[i]) + 1);
        }
        else {
            M.set(arr[i], 1);
        }
    }

    // M.size() given count of distinct
    // element in arr[]
    let distinct_size = M.size;
    let maxFreq = 1;

    // Traverse map to find max frequency
    for (let it of M) {

        maxFreq = Math.max(maxFreq, it[1]);
    }

    // Find the maximum length on the basis
    // of two cases in the approach

    document.write(Math.max(Math.min(distinct_size, maxFreq - 1), Math.min(distinct_size - 1, maxFreq)));
}

// Driver Code

let arr = [1, 2, 3, 4, 4, 4, 4, 4, 5];
let N = arr.length;

// Function call
maximumSubsequence(arr, N);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)* ，其中 N 为数组中的元素个数。
***辅助空间复杂度:** O(N)* ，其中 N 为数组中的元素个数。