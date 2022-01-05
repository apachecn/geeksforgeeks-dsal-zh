# 最大的子序列，使得所有索引和所有值分别是倍数

> 原文:[https://www . geesforgeks . org/最大子序列-这样-所有索引和所有值-都是-倍数-单独/](https://www.geeksforgeeks.org/largest-subsequence-such-that-all-indices-and-all-values-are-multiples-individually/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到 arr【】的最大严格递增子序列，使得 arr【】中所选元素的索引和所选元素分别是彼此的倍数。
**注意:**考虑对数组进行基于 1 的索引 **arr[]** 。
**举例:**

> **输入:** arr[] = {1，4，2，3，6，4，9}
> **输出:** 3
> **解释:**
> 我们可以选择索引 1，3，6，取值为 1，2，4:
> 这里每个较大的索引都可以被较小的索引整除，每个较大的索引值都大于较小的索引值。
> **输入:** arr[] = {5，3，4，6}
> **输出:** 2
> **解释:**
> 我们可以选择索引 1 和 3，取值为 3 和 6:
> 这里，每个较大的索引都可以被较小的索引整除，每个较大的索引值都大于较小的索引值。

**天真方法:**
天真方法是简单地生成所有可能的子序列，并为每个子序列检查两个条件:

*   首先检查元素是否严格按递增顺序排列
*   其次，检查 arr[]中所选元素的索引是否是彼此的倍数。

在满足给定两个条件的所有可能的子序列中，选择最大的子序列。
***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O( N )*
**高效途径:**
我们可以通过使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来优化代码，通过缓存其结果来避免重复子问题的冗余计算。

1.  创建一个数组 **dp[]** ，其大小等于 **arr[]** 的大小，其中 **dp[i]** 表示满足给定条件的第 I 个索引之前的最大子序列的大小。

2.  用 0 初始化数组 **dp[]** 。

3.  现在，从头到尾迭代数组 **arr[]** 。
4.  对于每个指数，找到指数 **j** ，将当前指数进行划分，并检查当前指数的值是否大于指数 **j** 的元素。
5.  如果是，则更新**DP【j】**为:

> **dp[j] = max(dp[current] + 1，dp[j])**

最后，遍历数组 **dp[]** 并打印最大值。
下面是高效方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that print maximum length
// of array
void maxLength(int arr[], int n)
{
    // dp[] array to store the
    // maximum length
    vector<int> dp(n, 1);

    for (int i = n - 1; i > 1; i--) {

        // Find all divisors of i
        for (int j = 1;
             j <= sqrt(i); j++) {

            if (i % j == 0) {
                int s = i / j;

                if (s == j) {

                    // If the current value
                    // is greater than the
                    // divisor's value
                    if (arr[i] > arr[s]) {

                        dp[s] = max(dp[i] + 1,
                                    dp[s]);
                    }
                }
                else {

                    // If current value
                    // is greater
                    // than the divisor's value
                    // and s is not equal
                    // to current index
                    if (s != i
                        && arr[i] > arr[s])
                        dp[s] = max(dp[i] + 1,
                                    dp[s]);

                    // Condition if current
                    // value is greater
                    // than the divisor's value
                    if (arr[i] > arr[j]) {
                        dp[j] = max(dp[i] + 1,
                                    dp[j]);
                    }
                }
            }
        }
    }

    int max = 0;

    // Computing the greatest value
    for (int i = 1; i < n; i++) {
        if (dp[i] > max)
            max = dp[i];
    }

    // Printing maximum length of array
    cout << max << "\n";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 0, 1, 4, 2, 3, 6, 4, 9 };
    int size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxLength(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function that print maximum length
// of array
static void maxLength(int arr[], int n)
{

    // dp[] array to store the
    // maximum length
    int dp[] = new int[n];
    for(int i = 1; i < n; i++)
    {
        dp[i] = 1;
    }

    for(int i = n - 1; i > 1; i--)
    {

        // Find all divisors of i
        for(int j = 1;
                j <= Math.sqrt(i); j++)
        {
            if (i % j == 0)
            {
                int s = i / j;

                if (s == j)
                {

                    // If the current value
                    // is greater than the
                    // divisor's value
                    if (arr[i] > arr[s])
                    {
                        dp[s] = Math.max(dp[i] + 1,
                                         dp[s]);
                    }
                }
                else
                {

                    // If current value is greater
                    // than the divisor's value
                    // and s is not equal
                    // to current index
                    if (s != i && arr[i] > arr[s])
                        dp[s] = Math.max(dp[i] + 1,
                                         dp[s]);

                    // Condition if current
                    // value is greater
                    // than the divisor's value
                    if (arr[i] > arr[j])
                    {
                        dp[j] = Math.max(dp[i] + 1,
                                         dp[j]);
                    }
                }
            }
        }
    }
    int max = 0;

    // Computing the greatest value
    for(int i = 1; i < n; i++)
    {
        if (dp[i] > max)
            max = dp[i];
    }

    // Printing maximum length of array
    System.out.println(max);
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 0, 1, 4, 2, 3, 6, 4, 9 };
    int size = arr.length;

    // Function call
    maxLength(arr, size);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import *

# Function that print maximum length
# of array
def maxLength (arr, n):

    # dp[] array to store the
    # maximum length
    dp = [1] * n

    for i in range(n - 1, 1, -1):

        # Find all divisors of i
        for j in range(1, int(sqrt(i)) + 1):
            if (i % j == 0):
                s = i // j

                if (s == j):

                    # If the current value
                    # is greater than the
                    # divisor's value
                    if (arr[i] > arr[s]):
                        dp[s] = max(dp[i] + 1, dp[s])

                else:
                    # If current value
                    # is greater
                    # than the divisor's value
                    # and s is not equal
                    # to current index
                    if (s != i and arr[i] > arr[s]):
                        dp[s] = max(dp[i] + 1, dp[s])

                    # Condition if current
                    # value is greater
                    # than the divisor's value
                    if (arr[i] > arr[j]):
                        dp[j] = max(dp[i] + 1, dp[j])

    Max = 0

    # Computing the greatest value
    for i in range(1, n):
        if (dp[i] > Max):
            Max = dp[i]

    # Printing maximum length of array
    print(Max)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 0, 1, 4, 2, 3, 6, 4, 9]
    size = len(arr)

    # Function call
    maxLength(arr, size)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that print maximum length
// of array
static void maxLength(int[] arr, int n)
{

    // dp[] array to store the
    // maximum length
    int[] dp = new int[n];
    for(int i = 1; i < n; i++)
    {
        dp[i] = 1;
    }

    for(int i = n - 1; i > 1; i--)
    {

        // Find all divisors of i
        for(int j = 1;
                j <= Math.Sqrt(i); j++)
        {
            if (i % j == 0)
            {
                int s = i / j;

                if (s == j)
                {

                    // If the current value
                    // is greater than the
                    // divisor's value
                    if (arr[i] > arr[s])
                    {
                        dp[s] = Math.Max(dp[i] + 1,
                                         dp[s]);
                    }
                }
                else
                {

                    // If current value is greater
                    // than the divisor's value
                    // and s is not equal
                    // to current index
                    if (s != i && arr[i] > arr[s])
                        dp[s] = Math.Max(dp[i] + 1,
                                         dp[s]);

                    // Condition if current
                    // value is greater
                    // than the divisor's value
                    if (arr[i] > arr[j])
                    {
                        dp[j] = Math.Max(dp[i] + 1,
                                         dp[j]);
                    }
                }
            }
        }
    }
    int max = 0;

    // Computing the greatest value
    for(int i = 1; i < n; i++)
    {
        if (dp[i] > max)
            max = dp[i];
    }

    // Printing maximum length of array
    Console.WriteLine(max);
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = new int[] { 0, 1, 4, 2,
                            3, 6, 4, 9 };
    int size = arr.Length;

    // Function call
    maxLength(arr, size);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function that print maximum length
// of array
function maxLength(arr, n)
{

    // dp[] array to store the
    // maximum length
    let dp = [];
    for(let i = 1; i < n; i++)
    {
        dp[i] = 1;
    }

    for(let i = n - 1; i > 1; i--)
    {

        // Find all divisors of i
        for(let j = 1;
                j <= Math.sqrt(i); j++)
        {
            if (i % j == 0)
            {
                let s = i / j;
                if (s == j)
                {

                    // If the current value
                    // is greater than the
                    // divisor's value
                    if (arr[i] > arr[s])
                    {
                        dp[s] = Math.max(dp[i] + 1,
                                         dp[s]);
                    }
                }
                else
                {

                    // If current value is greater
                    // than the divisor's value
                    // and s is not equal
                    // to current index
                    if (s != i && arr[i] > arr[s])
                        dp[s] = Math.max(dp[i] + 1,
                                         dp[s]);

                    // Condition if current
                    // value is greater
                    // than the divisor's value
                    if (arr[i] > arr[j])
                    {
                        dp[j] = Math.max(dp[i] + 1,
                                         dp[j]);
                    }
                }
            }
        }
    }
    let max = 0;

    // Computing the greatest value
    for(let i = 1; i < n; i++)
    {
        if (dp[i] > max)
            max = dp[i];
    }

    // Printing maximum length of array
    document.write(max);
}

// Driver Code

    // Given array arr[]
    let arr = [ 0, 1, 4, 2, 3, 6, 4, 9 ];
    let size = arr.length;

    // Function call
    maxLength(arr, size);

    // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(N*(sqrt(N))* 因为，对于数组的每个索引，我们计算它的所有除数，这需要 **O(sqrt(N))**
**辅助空间:** ***O(N)***