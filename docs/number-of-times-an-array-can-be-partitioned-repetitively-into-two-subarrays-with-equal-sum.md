# 一个数组可以被重复划分为两个相等和的子数组的次数

> 原文:[https://www . geeksforgeeks . org/一个数组可以被等和重复划分为两个子数组的次数/](https://www.geeksforgeeks.org/number-of-times-an-array-can-be-partitioned-repetitively-into-two-subarrays-with-equal-sum/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出该阵列可以重复划分为两个子阵列的次数，使得两个子阵列的元素之和[相同](https://www.geeksforgeeks.org/split-array-two-equal-sum-subarrays/)。

**示例:**

> **输入:** arr[] = { 2，2，2，2 }
> **输出:** 3
> **解释:**
> 1。创建索引 1 之后的第一个分区。其余的阵列都在{2，2}的右侧和左侧。
> 2。考虑左侧子阵列{2，2}。在这个左子阵列的索引 0 后做一个分区。
> 现在形成了两个相似的子阵列，每个子阵列有一个元素，即{2}，不能再细分。
> 3。考虑右侧的子阵列{2，2}。在这个左子阵列的索引 0 后做一个分区。
> 现在形成了两个相似的子阵列，每个子阵列有一个元素，即{2}，不能再细分。
> 因此输出为 3，因为阵列被分割了 3 次。
> 
> **输入:** arr[] = {12，3，3，0，3，3}
> **输出:** 4
> **解释:**
> 1。第一个分区在索引 0 之后。剩余数组为 arr[] = {3，3，0，3，3}。
> 2。第二个分区在索引 1 之后。剩下的数组是{3，3}和{0，3，3}。
> 3。第三个分区位于数组{3，3}中的索引 0 之后。
> 4。第四个分区在数组{0，3，3}
> 中的 1 之后，剩下的数组是{0，3}和{3}，不能再细分。
> 因此输出为 4。

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  找到给定数组 arr[]的前缀和，并将其存储在数组 **pref[]** 中。
2.  从开始位置迭代到结束位置。
3.  对于每个可能的分区索引(比如 **K** ，如果**前缀 _ 和[K]–前缀 _ 和[start-1] =前缀 _ 和[end]–前缀 _ 和[k]** ，则该分区有效。
4.  如果在上述步骤中分区有效，则分别进行左右子阵列，并确定这两个子阵列是否形成有效分区。
5.  对左分区和右分区重复步骤 3 和 4，直到不可能再进行任何分区。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursion Function to calculate the
// possible splitting
int splitArray(int start, int end,
               int* arr,
               int* prefix_sum)
{
    // If there are less than
    // two elements, we cannot
    // partition the sub-array.
    if (start >= end)
        return 0;

    // Iterate from the start
    // to end-1.
    for (int k = start; k < end; ++k) {

        if ((prefix_sum[k] - prefix_sum[start - 1])
            == (prefix_sum[end] - prefix_sum[k])) {

            // Recursive call to the left
            // and the right sub-array.
            return 1 + splitArray(start,
                                  k,
                                  arr,
                                  prefix_sum)
                   + splitArray(k + 1,
                                end,
                                arr,
                                prefix_sum);
        }
    }

    // If there is no such partition,
    // then return 0
    return 0;
}

// Function to find the total splitting
void solve(int arr[], int n)
{

    // Prefix array to store
    // the prefix-sum using
    // 1 based indexing
    int prefix_sum[n + 1];

    prefix_sum[0] = 0;

    // Store the prefix-sum
    for (int i = 1; i <= n; ++i) {
        prefix_sum[i] = prefix_sum[i - 1]
                        + arr[i - 1];
    }

    // Function Call to count the
    // number of splitting
    cout << splitArray(1, n,
                       arr,
                       prefix_sum);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 12, 3, 3, 0, 3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    solve(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Recursion Function to calculate the
// possible splitting
static int splitArray(int start, int end,
                      int[] arr,
                      int[] prefix_sum)
{
    // If there are less than
    // two elements, we cannot
    // partition the sub-array.
    if (start >= end)
        return 0;

    // Iterate from the start
    // to end-1.
    for (int k = start; k < end; ++k)
    {
        if ((prefix_sum[k] - prefix_sum[start - 1]) ==
            (prefix_sum[end] - prefix_sum[k]))
        {

            // Recursive call to the left
            // and the right sub-array.
            return 1 + splitArray(start, k, arr, prefix_sum) +
                       splitArray(k + 1, end, arr, prefix_sum);
        }
    }

    // If there is no such partition,
    // then return 0
    return 0;
}

// Function to find the total splitting
static void solve(int arr[], int n)
{

    // Prefix array to store
    // the prefix-sum using
    // 1 based indexing
    int []prefix_sum = new int[n + 1];

    prefix_sum[0] = 0;

    // Store the prefix-sum
    for (int i = 1; i <= n; ++i)
    {
        prefix_sum[i] = prefix_sum[i - 1] +
                               arr[i - 1];
    }

    // Function Call to count the
    // number of splitting
    System.out.print(splitArray(1, n, arr,
                                prefix_sum));
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 12, 3, 3, 0, 3, 3 };
    int N = arr.length;

    // Function call
    solve(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Recursion Function to calculate the
# possible splitting
def splitArray(start, end, arr, prefix_sum):

    # If there are less than
    # two elements, we cannot
    # partition the sub-array.
    if (start >= end):
        return 0

    # Iterate from the start
    # to end-1.
    for k in range(start, end):
        if ((prefix_sum[k] - prefix_sum[start - 1]) ==
            (prefix_sum[end] - prefix_sum[k])) :

            # Recursive call to the left
            # and the right sub-array.
            return (1 + splitArray(start, k, arr,
                                   prefix_sum) +
                        splitArray(k + 1, end, arr,
                                   prefix_sum))

    # If there is no such partition,
    # then return 0
    return 0

# Function to find the total splitting
def solve(arr, n):

    # Prefix array to store
    # the prefix-sum using
    # 1 based indexing
    prefix_sum = [0] * (n + 1)

    prefix_sum[0] = 0

    # Store the prefix-sum
    for i in range(1, n + 1):
        prefix_sum[i] = (prefix_sum[i - 1] +
                                arr[i - 1])

    # Function Call to count the
    # number of splitting
    print(splitArray(1, n, arr, prefix_sum))

# Driver Code

# Given array
arr = [ 12, 3, 3, 0, 3, 3 ]
N = len(arr)

# Function call
solve(arr, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursion Function to calculate the
// possible splitting
static int splitArray(int start, int end,
                      int[] arr,
                      int[] prefix_sum)
{

    // If there are less than
    // two elements, we cannot
    // partition the sub-array.
    if (start >= end)
        return 0;

    // Iterate from the start
    // to end-1.
    for(int k = start; k < end; ++k)
    {
       if ((prefix_sum[k] -
            prefix_sum[start - 1]) ==
           (prefix_sum[end] -
            prefix_sum[k]))
       {

           // Recursive call to the left
           // and the right sub-array.
           return 1 + splitArray(start, k, arr,
                                 prefix_sum) +
                      splitArray(k + 1, end, arr,
                                 prefix_sum);
       }
    }

    // If there is no such partition,
    // then return 0
    return 0;
}

// Function to find the total splitting
static void solve(int []arr, int n)
{

    // Prefix array to store
    // the prefix-sum using
    // 1 based indexing
    int []prefix_sum = new int[n + 1];

    prefix_sum[0] = 0;

    // Store the prefix-sum
    for(int i = 1; i <= n; ++i)
    {
       prefix_sum[i] = prefix_sum[i - 1] +
                              arr[i - 1];
    }

    // Function Call to count the
    // number of splitting
    Console.Write(splitArray(1, n, arr,
                             prefix_sum));
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 12, 3, 3, 0, 3, 3 };
    int N = arr.Length;

    // Function call
    solve(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Recursion Function to calculate the
// possible splitting
function splitArray(start, end, arr, prefix_sum)
{
    // If there are less than
    // two elements, we cannot
    // partition the sub-array.
    if (start >= end)
        return 0;

    // Iterate from the start
    // to end-1.
    for (let k = start; k < end; ++k)
    {
        if ((prefix_sum[k] - prefix_sum[start - 1]) ==
            (prefix_sum[end] - prefix_sum[k]))
        {

            // Recursive call to the left
            // and the right sub-array.
            return 1 + splitArray(start, k, arr, prefix_sum) +
                       splitArray(k + 1, end, arr, prefix_sum);
        }
    }

    // If there is no such partition,
    // then return 0
    return 0;
}

// Function to find the total splitting
function solve(arr, n)
{

    // Prefix array to store
    // the prefix-sum using
    // 1 based indexing
    let prefix_sum = Array.from({length: n+1}, (_, i) => 0);

    prefix_sum[0] = 0;

    // Store the prefix-sum
    for (let i = 1; i <= n; ++i)
    {
        prefix_sum[i] = prefix_sum[i - 1] +
                               arr[i - 1];
    }

    // Function Call to count the
    // number of splitting
   document.write(splitArray(1, n, arr,
                                prefix_sum));
}

// Driver code

    // Given array
    let arr = [ 12, 3, 3, 0, 3, 3 ];
    let N = arr.length;

    // Function call
    solve(arr, N);

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(N)*