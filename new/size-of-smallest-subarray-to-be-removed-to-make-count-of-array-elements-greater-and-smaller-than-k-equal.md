# 要删除的最小子数组的大小，以使数组元素的数量大于或小于 K

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)

给定一个整数 **K** 和一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，该数组由 **N** 个整数组成，任务是找到以下子数组的长度： 要删除的最小可能长度，以使其余数组中小于和大于 **K** 的数组元素数相等。

**示例**：

> **输入**：arr [] = {5，7，2，8，7，4，5，9}，K = 5
> **输出**：2
> **解释**：
> 需要删除的最小子数组是{8，7}，以使最大的结果数组{5、7、2、4、5、9}满足给定条件。
> 
> **输入**：arr [] = {12，16，12，13，10}，K = 13
> **输出**：3
> **说明**：为了使最大的合成数组{12，16}满足给定条件，需要删除的
> 最大的子数组{12，13，10}。

**天真的方法**：解决问题的最简单方法是[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并且[遍历其余数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，以保留严格限制的数组元素的数量 大于和小于整数 **K** 。 然后，选择最小的子数组，该子数组的删除将给出具有相等数量的较小和较大元素的数组。

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N <sup>2</sup> ）*

**高效方法**：的想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)，并对数组进行一些修改以在 **O（N）**时间内解决该问题。 给定的数组可以具有 3 种类型的元素：

*   **元素= K** ：将元素更改为 0（因为我们需要**严格大于 **K** 或小于 **K** 的元素）**

*   **元素> K** ：将元素更改为 1

*   **元素< K** ：将元素更改为-1

现在，[计算所有数组元素](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的总和，并将其存储在变量中，例如 *total_sum* 。 现在，total_sum 可以具有三个可能的值范围：

*   **如果 total_sum = 0** ：所有 1 都被-1 抵消。 因此，已经存在相等数量的 **K** 元素。 不需要删除操作。 因此，**打印 0** 作为所需答案。

*   **如果 total_sum > 0** ：一些 1s 不能取消-1s。 即数组比 **K** 具有更多的大元素，而比 **K** 具有更少的小元素。 因此，找到 **sum = total_sum** 的最小子数组，因为它是要删除的最小子数组。

*   **如果 total_sum < 0**：一些-1s 不能取消 1s。 即数组比 k 具有更多的较小元素，并且比 **K** 具有更少的较大元素。 因此，找到 **sum = total_sum** 的最小子数组，因为它是要删除的最小子数组。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function ot find the length
// of the smallest subarray
int smallSubarray(int arr[], int n,
                  int total_sum)
{
    // Stores (prefix Sum, index)
    // as (key, value) mappings
    unordered_map<int, int> m;
    int length = INT_MAX;
    int prefixSum = 0;

    // Iterate till N
    for (int i = 0; i < n; i++) {

        // Update the prefixSum
        prefixSum += arr[i];

        // Update the length
        if (prefixSum == total_sum) {
            length = min(length, i + 1);
        }

        // Put the latest index to
        // find the minimum length
        m[prefixSum] = i;

        if (m.count(prefixSum - total_sum)) {

            // Update the length
            length
                = min(length,
                      i - m[prefixSum - total_sum]);
        }
    }

    // Return the answer
    return length;
}

// Function to find the length of
// the largest subarray
int smallestSubarrayremoved(int arr[], int n,
                            int k)
{

    // Stores the sum of all array
    // elements after modification
    int total_sum = 0;

    for (int i = 0; i < n; i++) {

        // Change greater than k to 1
        if (arr[i] > k) {
            arr[i] = 1;
        }

        // Change smaller than k to -1
        else if (arr[i] < k) {
            arr[i] = -1;
        }

        // Change equal to k to 0
        else {
            arr[i] = 0;
        }

        // Update total_sum
        total_sum += arr[i];
    }

    // No deletion required, return 0
    if (total_sum == 0) {
        return 0;
    }

    else {

        // Delete smallest subarray
        // that has sum = total_sum
        return smallSubarray(arr, n,
                             total_sum);
    }
}

// Driver Code
int main()
{
    int arr[] = { 12, 16, 12, 13, 10 };
    int K = 13;

    int n = sizeof(arr) / sizeof(int);

    cout << smallestSubarrayremoved(
        arr, n, K);

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function ot find the length
// of the smallest subarray
static int smallSubarray(int arr[], int n,
                         int total_sum)
{

    // Stores (prefix Sum, index)
    // as (key, value) mappings
    Map<Integer,
        Integer> m = new HashMap<Integer,
                                 Integer>();

    int length = Integer.MAX_VALUE;
    int prefixSum = 0;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Update the prefixSum
        prefixSum += arr[i];

        // Update the length
        if (prefixSum == total_sum)
        {
            length = Math.min(length, i + 1);
        }

        // Put the latest index to
        // find the minimum length
        m.put(prefixSum, i);

        if (m.containsKey(prefixSum - total_sum))
        {

            // Update the length
            length = Math.min(length,
                              i - m.get(prefixSum - 
                                        total_sum));
        }
    }

    // Return the answer
    return length;
}

// Function to find the length of
// the largest subarray
static int smallestSubarrayremoved(int arr[], int n,
                                   int k)
{

    // Stores the sum of all array
    // elements after modification
    int total_sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Change greater than k to 1
        if (arr[i] > k)
        {
            arr[i] = 1;
        }

        // Change smaller than k to -1
        else if (arr[i] < k)
        {
            arr[i] = -1;
        }

        // Change equal to k to 0
        else
        {
            arr[i] = 0;
        }

        // Update total_sum
        total_sum += arr[i];
    }

    // No deletion required, return 0
    if (total_sum == 0)
    {
        return 0;
    }
    else
    {

        // Delete smallest subarray
        // that has sum = total_sum
        return smallSubarray(arr, n, total_sum);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 12, 16, 12, 13, 10 };
    int K = 13;
    int n = arr.length;

    System.out.println(
        smallestSubarrayremoved(arr, n, K));
}
}

// This code is contributed by chitranayal

```

## Python3

```py

# Python3 program to implement

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
# the above approach

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
import sys

# Function ot find the length

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
# of the smallest subarray

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
def smallSubarray(arr, n, total_sum):

    # Stores (prefix Sum, index)
    # as (key, value) mappings
    m = {}
    length = sys.maxsize
    prefixSum = 0

    # Iterate till N
    for i in range(n):

        # Update the prefixSum
        prefixSum += arr[i]

        # Update the length
        if(prefixSum == total_sum):
            length = min(length, i + 1)

        # Put the latest index to
        # find the minimum length
        m[prefixSum] = i

        if((prefixSum - total_sum) in m.keys()):

            # Update the length
            length = min(length,
                         i - m[prefixSum - total_sum])

    # Return the answer
    return length

# Function to find the length of

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
# the largest subarray

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
def smallestSubarrayremoved(arr, n, k):

    # Stores the sum of all array
    # elements after modification
    total_sum = 0

    for i in range(n):

        # Change greater than k to 1
        if(arr[i] > k):
            arr[i] = 1

        # Change smaller than k to -1
        elif(arr[i] < k):
            arr[i] = -1

        # Change equal to k to 0
        else:
            arr[i] = 0

        # Update total_sum
        total_sum += arr[i]

    # No deletion required, return 0
    if(total_sum == 0):
        return 0
    else:

        # Delete smallest subarray
        # that has sum = total_sum
        return smallSubarray(arr, n,
                             total_sum)

# Driver Code

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
arr = [ 12, 16, 12, 13, 10 ]
K = 13

n = len(arr)

# Function call

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)
print(smallestSubarrayremoved(arr, n, K))

# This code is contributed by Shivam Singh

> 原文：[https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/](https://www.geeksforgeeks.org/size-of-smallest-subarray-to-be-removed-to-make-count-of-array-elements-greater-and-smaller-than-k-equal/)

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function ot find the length
// of the smallest subarray
static int smallSubarray(int []arr, int n,
                         int total_sum)
{

    // Stores (prefix Sum, index)
    // as (key, value) mappings
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    int length = int.MaxValue;
    int prefixSum = 0;

    // Iterate till N
    for(int i = 0; i < n; i++)
    {

        // Update the prefixSum
        prefixSum += arr[i];

        // Update the length
        if (prefixSum == total_sum)
        {
            length = Math.Min(length, i + 1);
        }

        // Put the latest index to
        // find the minimum length
        if (m.ContainsKey(prefixSum))
            m[prefixSum] = i;
        else
            m.Add(prefixSum, i);

        if (m.ContainsKey(prefixSum - total_sum))
        {

            // Update the length
            length = Math.Min(length,
                              i - m[prefixSum - 
                                    total_sum]);
        }
    }

    // Return the answer
    return length;
}

// Function to find the length of
// the largest subarray
static int smallestSubarrayremoved(int []arr, 
                                   int n, int k)
{

    // Stores the sum of all array
    // elements after modification
    int total_sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Change greater than k to 1
        if (arr[i] > k)
        {
            arr[i] = 1;
        }

        // Change smaller than k to -1
        else if (arr[i] < k)
        {
            arr[i] = -1;
        }

        // Change equal to k to 0
        else
        {
            arr[i] = 0;
        }

        // Update total_sum
        total_sum += arr[i];
    }

    // No deletion required, return 0
    if (total_sum == 0)
    {
        return 0;
    }
    else
    {

        // Delete smallest subarray
        // that has sum = total_sum
        return smallSubarray(arr, n, total_sum);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 12, 16, 12, 13, 10 };
    int K = 13;
    int n = arr.Length;

    Console.WriteLine(
            smallestSubarrayremoved(arr, n, K));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
3

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *



