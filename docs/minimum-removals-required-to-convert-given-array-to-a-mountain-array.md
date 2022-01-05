# 将给定阵列转换为山地阵列所需的最小清除量

> 原文:[https://www . geeksforgeeks . org/minimum-removes-需要将给定阵列转换为山形阵列/](https://www.geeksforgeeks.org/minimum-removals-required-to-convert-given-array-to-a-mountain-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到使给定数组成为山形数组所需移除的最小数组元素数。

> 山形阵列具有以下属性:
> 
> *   数组长度≥ 3。
> *   存在一些索引 **i** ( *基于 0 的索引*)与**0<I<N–1**这样:
>     *   arr[0]< arr[1]
>     *   疤痕[i] >疤痕[i + 1] >... >疤痕[arr.length – 1]。

**示例:**

> **输入:** arr[] = {1，3，1}
> **输出:** 0
> **说明:**阵法本身就是一个山阵。因此，不需要移除。
> 
> **输入:** arr[] = {2，1，1，5，6，2，3，1}
> **输出:** 3
> **说明:**去掉 arr[0]，arr[1]和 arr[5]将 arr[]修改为{1，5，6，3，1}，为山阵。

**方法:**思路是用[自下而上的动态规划](https://www.geeksforgeeks.org/tabulation-vs-memoization/)方法解决这个问题。按照以下步骤解决问题:

1.  如果给定数组的长度小于 3，则该数组不能转换为山形数组。
2.  否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个 **i** <sup>第</sup>个元素 **(0 < i < N)** ，找到子数组**中递增子序列的长度{arr[0]，…，arr[I–1]}**并将其存储在数组中，比如**left ncreasing[]**。
3.  同样，求子阵 **{arr[i+1]，…中递增子序列的长度。，arr[N-1]}** 对于每一个**I**T4 元素 **(0 < i < N)** ，并将其存储在数组中，说**右对齐[]。**
4.  找到满足以下条件的指数 **i (0 < i < N)** :
    1.  第一个强制条件是**峰值条件**，即**左进【I】>0****右进【I】>0**。
    2.  在所有指标中，如果**左重[i] +右重[i]** 为最大，则该指标为山阵峰，如 **X** 。
5.  返回结果为**N –( X+1)**，加 1 使数组索引达到长度。

插图:

> 考虑数组 arr[] = {4，3，6，4，5}
> 因此，left ncreasing[]= { 0，0，1，1，2 }&right ncreasing[]= { 2，1，1，0，0}。
> 只有一个索引 i = 2(基于 0 的索引)，对于该索引，left ncreasing[2]>0 和 right ncreasing[2]>0。
> 因此，X =左对齐[2] +右对齐[2] = 2。
> 因此，所需答案= N –( X+1)= 5 –( 2+3)= 2。
> 可能的解决方案之一可能是{4，6，5}，即删除 3 (arr[1])和 4(arr[3])。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to count array
// elements required to be removed
// to make array a mountain array
int minRemovalsUtil(int arr[], int n)
{
    int result = 0;
    if (n < 3) {
        return -1;
    }

    // Stores length of increasing
    // subsequence from [0, i-1]
    int leftIncreasing[n] = {0};

    // Stores length of increasing
    // subsequence from [i + 1, n - 1]
    int rightIncreasing[n] = {0};

    // Iterate for each position up to
    // N - 1 to find the length of subsequence
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < i; j++)
        {

            // If j is less than i, then
            // i-th position has leftIncreasing[j]
            // + 1 lesser elements including itself
            if (arr[j] < arr[i])
            {

                // Check if it is the maximum
                // obtained so far
                leftIncreasing[i]
                    = max(leftIncreasing[i],
                          leftIncreasing[j] + 1);
            }
        }
    }

    // Search for increasing subsequence from right
    for (int i = n - 2; i >= 0; i--)
    {
        for (int j = n - 1; j > i; j--)
        {
            if (arr[j] < arr[i])
            {
                rightIncreasing[i]
                    = max(rightIncreasing[i],
                               rightIncreasing[j] + 1);
            }
        }
    }

    // Find the position following the peak
    // condition and have maximum leftIncreasing[i]
    // + rightIncreasing[i]
    for (int i = 0; i < n; i++)
    {
        if (leftIncreasing[i] != 0
            && rightIncreasing[i] != 0)
        {
            result = max(result,
                         leftIncreasing[i]
                         + rightIncreasing[i]);
        }
    }
    return n - (result + 1);
}

// Function to count elements to be
// removed to make array a mountain array
void minRemovals(int arr[], int n)
{
    int ans = minRemovalsUtil(arr, n);

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 2, 1, 1, 5, 6, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minRemovals(arr, n);
    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Utility function to count array
    // elements required to be removed
    // to make array a mountain array
    public static int minRemovalsUtil(
        int[] arr)
    {
        int result = 0;
        if (arr.length < 3) {
            return -1;
        }

        // Stores length of increasing
        // subsequence from [0, i-1]
        int[] leftIncreasing
            = new int[arr.length];

        // Stores length of increasing
        // subsequence from [i + 1, n - 1]
        int[] rightIncreasing = new int[arr.length];

        // Iterate for each position up to
        // N - 1 to find the length of subsequence
        for (int i = 1; i < arr.length; i++) {

            for (int j = 0; j < i; j++) {

                // If j is less than i, then
                // i-th position has leftIncreasing[j]
                // + 1 lesser elements including itself
                if (arr[j] < arr[i]) {

                    // Check if it is the maximum
                    // obtained so far
                    leftIncreasing[i]
                        = Math.max(
                            leftIncreasing[i],
                            leftIncreasing[j] + 1);
                }
            }
        }

        // Search for increasing subsequence from right
        for (int i = arr.length - 2; i >= 0; i--) {
            for (int j = arr.length - 1; j > i; j--) {
                if (arr[j] < arr[i]) {
                    rightIncreasing[i]
                        = Math.max(rightIncreasing[i],
                                   rightIncreasing[j] + 1);
                }
            }
        }

        // Find the position following the peak
        // condition and have maximum leftIncreasing[i]
        // + rightIncreasing[i]
        for (int i = 0; i < arr.length; i++) {
            if (leftIncreasing[i] != 0
                && rightIncreasing[i] != 0) {
                result = Math.max(
                    result, leftIncreasing[i]
                                + rightIncreasing[i]);
            }
        }

        return arr.length - (result + 1);
    }

    // Function to count elements to be
    // removed to make array a mountain array
    public static void minRemovals(int[] arr)
    {
        int ans = minRemovalsUtil(arr);

        // Print the answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 2, 1, 1, 5, 6, 2, 3, 1 };

        // Function Call
        minRemovals(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Utility function to count array
# elements required to be removed
# to make array a mountain array
def minRemovalsUtil(arr):

    result = 0

    if (len(arr) < 3):
        return -1

    # Stores length of increasing
    # subsequence from [0, i-1]
    leftIncreasing = [0] * len(arr)

    # Stores length of increasing
    # subsequence from [i + 1, n - 1]
    rightIncreasing = [0] * len(arr)

    # Iterate for each position up to
    # N - 1 to find the length of subsequence
    for i in range(1, len(arr)):
        for j in range(i):

            # If j is less than i, then
            # i-th position has leftIncreasing[j]
            # + 1 lesser elements including itself
            if (arr[j] < arr[i]):

                # Check if it is the maximum
                # obtained so far
                leftIncreasing[i] = max(leftIncreasing[i],
                                        leftIncreasing[j] + 1);

    # Search for increasing subsequence from right
    for i in range(len(arr) - 2 , -1, -1):
        j = len(arr) - 1

        while j > i:
            if (arr[j] < arr[i]) :
                rightIncreasing[i] = max(rightIncreasing[i],
                                         rightIncreasing[j] + 1)

            j -= 1

    # Find the position following the peak
    # condition and have maximum leftIncreasing[i]
    # + rightIncreasing[i]
    for i in range(len(arr)):
        if (leftIncreasing[i] != 0 and
           rightIncreasing[i] != 0):
            result = max(result, leftIncreasing[i] +
                                rightIncreasing[i]);

    return len(arr) - (result + 1)

# Function to count elements to be
# removed to make array a mountain array
def minRemovals(arr):

    ans = minRemovalsUtil(arr)

    # Print the answer
    print(ans)

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 2, 1, 1, 5, 6, 2, 3, 1 ]

    # Function Call
    minRemovals(arr)

# This code is contributed by AnkThon
```

## C#

```
// C# program of the above approach
using System;

class GFG
{

    // Utility function to count array
    // elements required to be removed 
    // to make array a mountain array
    public static int minRemovalsUtil(int[] arr)
    {
        int result = 0;
        if (arr.Length < 3)
        {
            return -1;
        }

        // Stores length of increasing
        // subsequence from [0, i-1]
        int[] leftIncreasing
            = new int[arr.Length];

        // Stores length of increasing
        // subsequence from [i + 1, n - 1]
        int[] rightIncreasing = new int[arr.Length];

        // Iterate for each position up to
        // N - 1 to find the length of subsequence
        for (int i = 1; i < arr.Length; i++)
        {
            for (int j = 0; j < i; j++)
            {

                // If j is less than i, then
                // i-th position has leftIncreasing[j]
                // + 1 lesser elements including itself
                if (arr[j] < arr[i])
                {

                    // Check if it is the maximum
                    // obtained so far
                    leftIncreasing[i]
                        = Math.Max(
                            leftIncreasing[i],
                            leftIncreasing[j] + 1);
                }
            }
        }

        // Search for increasing subsequence from right
        for (int i = arr.Length - 2; i >= 0; i--)
        {
            for (int j = arr.Length - 1; j > i; j--)
            {
                if (arr[j] < arr[i])
                {
                    rightIncreasing[i]
                        = Math.Max(rightIncreasing[i],
                                   rightIncreasing[j] + 1);
                }
            }
        }

        // Find the position following the peak
        // condition and have maximum leftIncreasing[i]
        // + rightIncreasing[i]
        for (int i = 0; i < arr.Length; i++)
        {
            if (leftIncreasing[i] != 0
                && rightIncreasing[i] != 0)
            {
                result = Math.Max(result, leftIncreasing[i]
                                + rightIncreasing[i]);
            }
        }
        return arr.Length - (result + 1);
    }

    // Function to count elements to be
    // removed to make array a mountain array
    public static void minRemovals(int[] arr)
    {
        int ans = minRemovalsUtil(arr);

        // Print the answer
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        // Given array
        int[] arr = {2, 1, 1, 5, 6, 2, 3, 1};

        // Function Call
        minRemovals(arr);
    }
}

// This code is contributed by shikhasingrajput.
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Utility function to count array
// elements required to be removed
// to make array a mountain array
function minRemovalsUtil(arr, n)
{
    var result = 0;
    if (n < 3) {
        return -1;
    }

    // Stores length of increasing
    // subsequence from [0, i-1]
    var leftIncreasing = Array(n).fill(0);

    // Stores length of increasing
    // subsequence from [i + 1, n - 1]
    var rightIncreasing = Array(n).fill(0);

    // Iterate for each position up to
    // N - 1 to find the length of subsequence
    for (var i = 1; i < n; i++)
    {
        for (var j = 0; j < i; j++)
        {

            // If j is less than i, then
            // i-th position has leftIncreasing[j]
            // + 1 lesser elements including itself
            if (arr[j] < arr[i])
            {

                // Check if it is the maximum
                // obtained so far
                leftIncreasing[i]
                    = Math.max(leftIncreasing[i],
                          leftIncreasing[j] + 1);
            }
        }
    }

    // Search for increasing subsequence from right
    for (var i = n - 2; i >= 0; i--)
    {
        for (var j = n - 1; j > i; j--)
        {
            if (arr[j] < arr[i])
            {
                rightIncreasing[i]
                    = Math.max(rightIncreasing[i],
                               rightIncreasing[j] + 1);
            }
        }
    }

    // Find the position following the peak
    // condition and have maximum leftIncreasing[i]
    // + rightIncreasing[i]
    for (var i = 0; i < n; i++)
    {
        if (leftIncreasing[i] != 0
            && rightIncreasing[i] != 0)
        {
            result = Math.max(result,
                         leftIncreasing[i]
                         + rightIncreasing[i]);
        }
    }
    return n - (result + 1);
}

// Function to count elements to be
// removed to make array a mountain array
function minRemovals(arr, n)
{
    var ans = minRemovalsUtil(arr, n);

    // Print the answer
    document.write( ans);
}

// Driver Code
// Given array
var arr = [2, 1, 1, 5, 6, 2, 3, 1];
var n = arr.length;

// Function Call
minRemovals(arr, n);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*