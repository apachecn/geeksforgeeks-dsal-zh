# 检查是否存在与给定子阵列相同的非连续子序列

> 原文:[https://www . geesforgeks . org/check-如果一个非连续子序列与给定子阵列相同-存在与否/](https://www.geeksforgeeks.org/check-if-a-non-contiguous-subsequence-same-as-the-given-subarray-exists-or-not/)

给定一个由 **N** 个整数和两个整数值 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，表示一个子阵列的开始和结束索引，任务是检查是否存在与给定子阵列相同的不连续的[子序列](https://www.geeksforgeeks.org/tag/subsequence/)。如果发现是真的，打印**“是”**。否则，打印**“否”**。

> 一个**非连续子序列**包含至少两个来自非连续索引的连续字符。

**示例:**

> **输入:** arr[] = {1，7，12，1，7，5，10，11，42}，L = 3，R = 6
> **输出:**是
> **说明:**非邻接子序列{arr[0]，arr[1]，arr[5]，arr[6]}与子阵列{arr[3]相同，..，arr[6]}。
> 
> **输入:** arr[] = {0，1，2，-2，5，10}，L = 1，R = 3

**朴素方法:**最简单的方法是生成给定数组的所有可能的子序列，并检查生成的任何子序列是否等于给定子数组。如果发现是真的，那么打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该思想基于以下关键观察:如果给定子阵列的第一个元素在范围**【0，L–1】**中至少出现一次，并且子阵列的最后一个元素在范围**【R+1，N】**中至少出现一次，则总是存在非连续子序列。

**逻辑证明:**

> 如果子阵列 **{arr[L]，… arr[R]}** 的第 1 <sup>st</sup> 元素也出现在任何索引 **K** (K < L)处，那么一个这样的不连续子序列可以是 **{arr[K]，arr[L + 1]，…。，arr[R]}** 。
> 如果子阵列的最后一个元素 **{arr[L]，… arr[R]}** 也出现在任何索引 **K** (K > R)处，那么一个这样的非连续子序列可以是强的> {arr[L]，arr[L + 1]，…。，arr[R–1]，arr[K]}。
> 如果上述两个条件都不满足，则不存在这样的不连续子序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility Function to check whether
// a subsequence same as the given
// subarray exists or not
bool checkSubsequenceUtil(
    int arr[], int L, int R, int N)
{
    // Check if first element of the
    // subarray is also present before
    for (int i = 0; i < L; i++)
        if (arr[i] == arr[L])
            return true;

    // Check if last element of the
    // subarray is also present later
    for (int i = R + 1; i < N; i++)
        if (arr[i] == arr[R])
            return true;

    // If above two conditions are
    // not satisfied, then no such
    // subsequence exists
    return false;
}

// Function to check and print if a
// subsequence which is same as the
// given subarray is present or not
void checkSubsequence(int arr[], int L,
                      int R, int N)
{
    if (checkSubsequenceUtil(arr, L,
                             R, N)) {
        cout << "YES\n";
    }
    else {
        cout << "NO\n";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 7, 12, 1, 7,
                  5, 10, 11, 42 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int L = 3, R = 6;

    // Function Call
    checkSubsequence(arr, L, R, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Utility Function to check whether
// a subsequence same as the given
// subarray exists or not
static boolean checkSubsequenceUtil(int arr[], int L,
                                    int R, int N)
{

    // Check if first element of the
    // subarray is also present before
    for(int i = 0; i < L; i++)
        if (arr[i] == arr[L])
            return true;

    // Check if last element of the
    // subarray is also present later
    for(int i = R + 1; i < N; i++)
        if (arr[i] == arr[R])
            return true;

    // If above two conditions are
    // not satisfied, then no such
    // subsequence exists
    return false;
}

// Function to check and print if a
// subsequence which is same as the
// given subarray is present or not
static void checkSubsequence(int arr[], int L,
                             int R, int N)
{
    if (checkSubsequenceUtil(arr, L,
                             R, N))
    {
        System.out.print("YES\n");
    }
    else
    {
        System.out.print("NO\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 7, 12, 1, 7,
                  5, 10, 11, 42 };
    int N = arr.length;
    int L = 3, R = 6;

    // Function Call
    checkSubsequence(arr, L, R, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility Function to check whether
# a subsequence same as the given
# subarray exists or not
def checkSubsequenceUtil(arr, L, R, N):

    # Check if first element of the
    # subarray is also present before
    for i in range(L):
        if (arr[i] == arr[L]):
            return True

    # Check if last element of the
    # subarray is also present later
    for i in range(R + 1, N, 1):
        if (arr[i] == arr[R]):
            return True

    # If above two conditions are
    # not satisfied, then no such
    # subsequence exists
    return False

# Function to check and prif a
# subsequence which is same as the
# given subarray is present or not
def checkSubsequence(arr, L, R, N):

    if (checkSubsequenceUtil(arr, L,R, N)):
        print("YES")
    else:
        print("NO")

# Driver Code
arr = [ 1, 7, 12, 1, 7,
        5, 10, 11, 42 ]
N = len(arr)
L = 3
R = 6

# Function Call
checkSubsequence(arr, L, R, N)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Utility Function to check whether
// a subsequence same as the given
// subarray exists or not
static bool checkSubsequenceUtil(int[] arr, int L,
                                 int R, int N)
{

    // Check if first element of the
    // subarray is also present before
    for(int i = 0; i < L; i++)
        if (arr[i] == arr[L])
            return true;

    // Check if last element of the
    // subarray is also present later
    for(int i = R + 1; i < N; i++)
        if (arr[i] == arr[R])
            return true;

    // If above two conditions are
    // not satisfied, then no such
    // subsequence exists
    return false;
}

// Function to check and print if a
// subsequence which is same as the
// given subarray is present or not
static void checkSubsequence(int[] arr, int L,
                             int R, int N)
{
    if (checkSubsequenceUtil(arr, L,
                             R, N))
    {
        Console.Write("YES\n");
    }
    else
    {
        Console.Write("NO\n");
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 7, 12, 1, 7,
                  5, 10, 11, 42 };

    int N = arr.Length;
    int L = 3, R = 6;

    // Function Call
    checkSubsequence(arr, L, R, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Utility Function to check whether
// a subsequence same as the given
// subarray exists or not
function checkSubsequenceUtil(arr, L,
                                    R, N)
{

    // Check if first element of the
    // subarray is also present before
    for(let i = 0; i < L; i++)
        if (arr[i] == arr[L])
            return true;

    // Check if last element of the
    // subarray is also present later
    for(let i = R + 1; i < N; i++)
        if (arr[i] == arr[R])
            return true;

    // If above two conditions are
    // not satisfied, then no such
    // subsequence exists
    return false;
}

// Function to check and prlet if a
// subsequence which is same as the
// given subarray is present or not
function checkSubsequence(arr, L,
                             R, N)
{
    if (checkSubsequenceUtil(arr, L,
                             R, N))
    {
        document.write("YES\n");
    }
    else
    {
        document.write("NO\n");
    }
}

// Driver code

    let arr = [ 1, 7, 12, 1, 7,
                  5, 10, 11, 42 ];
    let N = arr.length;
    let L = 3, R = 6;

    // Function Call
    checkSubsequence(arr, L, R, N);

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)