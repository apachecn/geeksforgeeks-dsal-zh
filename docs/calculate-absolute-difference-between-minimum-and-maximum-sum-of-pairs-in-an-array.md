# 计算数组中对的最小和最大和的绝对差

> 原文:[https://www . geesforgeks . org/计算数组中最小和最大对和的绝对差值/](https://www.geeksforgeeks.org/calculate-absolute-difference-between-minimum-and-maximum-sum-of-pairs-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出任意一对元素 **(arr[i]，arr[j])** 的最小和最大和之间的绝对差，使得 **(i < j)** 和 **(arr[i] < arr[j])** 。

**示例:**

> **输入:** arr[] = {1，2，4，7}
> **输出:** 8
> **解释:**所有可能的对是:
> 
> *   (1，2) →总和= 3
> *   (1，4) →总和= 5
> *   (1，7) →总和= 8
> *   (2，4) →总和= 6
> *   (2，7) →总和= 9
> *   (4，7) →总和= 11
> 
> 因此，最大值和最小值之差= 11–3 = 8。
> 
> **输入:** arr[] = {2，5，3 }
> T3】输出: 2

**方法:**解决给定问题的思路是创建两个辅助数组来存储给定数组后缀的每个索引的后缀的最小值和最大值，然后找到所需的绝对差。
按照以下步骤解决问题:

*   初始化两个变量，比如 **maxSum** 和 **minSum** ，根据给定的条件存储给定数组中一对元素的最大和[最小和。](https://www.geeksforgeeks.org/smallest-pair-sum-in-an-array/)
*   初始化两个数组，比如大小为 **N** 的**后缀最大值[]** 和**后缀最小值[]** ，为数组的每个索引存储后缀的最大值和最小值 **arr[]** 。
*   [反向遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并在每个索引处更新**后缀[]** 和**后缀[]** 。
*   现在，[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，执行以下步骤:
    *   如果当前元素 **arr[i]** 小于**后缀 Max[i]** ，则将 **maxSum** 的值更新为 **maxSum** 和**的最大值(arr[i] +后缀 Max[i])** 。
    *   如果当前元素**arr【I】**小于**后缀【I】**，则更新 **minSum** 的值为 **minSum** 和**的最小值(arr【I】+后缀【I】)**。
*   完成上述步骤后，打印值**(maxSum–minSum)**作为结果差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// the maximum and minimum sum of a pair
// (arr[i], arr[j]) from the array such
// that i < j and arr[i] < arr[j]
int GetDiff(int A[], int N)
{
    // Stores the maximum from
    // the suffix of the array
    int SuffMaxArr[N];

    // Set the last element
    SuffMaxArr[N - 1] = A[N - 1];

    // Traverse the remaining array
    for (int i = N - 2; i >= 0; --i) {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMaxArr[i] = max(SuffMaxArr[i + 1],
                            A[i + 1]);
    }

    // Stores the maximum sum of any pair
    int MaximumSum = INT_MIN;

    // Calculate the maximum sum
    for (int i = 0; i < N - 1; i++) {
        if (A[i] < SuffMaxArr[i])
            MaximumSum
                = max(MaximumSum,
                      A[i] + SuffMaxArr[i]);
    }

    // Stores the maximum sum of any pair
    int MinimumSum = INT_MAX;

    // Stores the minimum of suffixes
    // from the given array
    int SuffMinArr[N];

    // Set the last element
    SuffMinArr[N - 1] = INT_MAX;

    // Traverse the remaining array
    for (int i = N - 2; i >= 0; --i) {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMinArr[i] = min(SuffMinArr[i + 1],
                            A[i + 1]);
    }

    // Calculate the minimum sum
    for (int i = 0; i < N - 1; i++) {

        if (A[i] < SuffMinArr[i]) {
            MinimumSum = min(MinimumSum,
                             A[i] + SuffMinArr[i]);
        }
    }

    // Return the resultant difference
    return abs(MaximumSum - MinimumSum);
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 1, 3, 7, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << GetDiff(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the difference between
// the maximum and minimum sum of a pair
// (arr[i], arr[j]) from the array such
// that i < j and arr[i] < arr[j]
static int GetDiff(int A[], int N)
{

    // Stores the maximum from
    // the suffix of the array
    int SuffMaxArr[] = new int[N];

    // Set the last element
    SuffMaxArr[N - 1] = A[N - 1];

    // Traverse the remaining array
    for(int i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMaxArr[i] = Math.max(SuffMaxArr[i + 1],
                                          A[i + 1]);
    }

    // Stores the maximum sum of any pair
    int MaximumSum = Integer.MIN_VALUE;

    // Calculate the maximum sum
    for(int i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMaxArr[i])
            MaximumSum = Math.max(MaximumSum,
                                  A[i] + SuffMaxArr[i]);
    }

    // Stores the maximum sum of any pair
    int MinimumSum = Integer.MAX_VALUE;

    // Stores the minimum of suffixes
    // from the given array
    int SuffMinArr[] = new int[N];

    // Set the last element
    SuffMinArr[N - 1] = Integer.MAX_VALUE;

    // Traverse the remaining array
    for(int i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMinArr[i] = Math.min(SuffMinArr[i + 1],
                                          A[i + 1]);
    }

    // Calculate the minimum sum
    for(int i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMinArr[i])
        {
            MinimumSum = Math.min(MinimumSum,
                                  A[i] + SuffMinArr[i]);
        }
    }

    // Return the resultant difference
    return Math.abs(MaximumSum - MinimumSum);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 1, 3, 7, 5, 6 };
    int N = arr.length;

    // Function Call
    System.out.println(GetDiff(arr, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to find the difference between
# the maximum and minimum sum of a pair
# (arr[i], arr[j]) from the array such
# that i < j and arr[i] < arr[j]
def GetDiff(A, N):

    # Stores the maximum from
    # the suffix of the array
    SuffMaxArr = [0 for i in range(N)]

    # Set the last element
    SuffMaxArr[N - 1] = A[N - 1]

    # Traverse the remaining array
    i = N-2
    while(i >= 0):
        # Update the maximum from suffix
        # for the remaining indices
        SuffMaxArr[i] = max(SuffMaxArr[i + 1], A[i + 1])
        i -= 1

    # Stores the maximum sum of any pair
    MaximumSum = -sys.maxsize-1

    # Calculate the maximum sum
    for i in range(N-1):
        if (A[i] < SuffMaxArr[i]):
            MaximumSum = max(MaximumSum, A[i] + SuffMaxArr[i])

    # Stores the maximum sum of any pair
    MinimumSum = sys.maxsize

    # Stores the minimum of suffixes
    # from the given array
    SuffMinArr = [0 for i in range(N)]

    # Set the last element
    SuffMinArr[N - 1] = sys.maxsize

    # Traverse the remaining array
    i = N-2
    while(i >= 0):

        # Update the maximum from suffix
        # for the remaining indices
        SuffMinArr[i] = min(SuffMinArr[i + 1], A[i + 1])
        i -= 1

    # Calculate the minimum sum
    for i in range(N - 1):
        if (A[i] < SuffMinArr[i]):
            MinimumSum = min(MinimumSum,A[i] + SuffMinArr[i])

    # Return the resultant difference
    return abs(MaximumSum - MinimumSum)

# Driver Code
if __name__ == '__main__':
    arr = [2, 4, 1, 3, 7, 5, 6]
    N = len(arr)

    # Function Call
    print(GetDiff(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG
{

// Function to find the difference between
// the maximum and minimum sum of a pair
// (arr[i], arr[j]) from the array such
// that i < j and arr[i] < arr[j]
static int GetDiff(int[] A, int N)
{

    // Stores the maximum from
    // the suffix of the array
    int[] SuffMaxArr = new int[N];

    // Set the last element
    SuffMaxArr[N - 1] = A[N - 1];

    // Traverse the remaining array
    for(int i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMaxArr[i] = Math.Max(SuffMaxArr[i + 1],
                                          A[i + 1]);
    }

    // Stores the maximum sum of any pair
    int MaximumSum = Int32.MinValue;

    // Calculate the maximum sum
    for(int i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMaxArr[i])
            MaximumSum = Math.Max(MaximumSum,
                                  A[i] + SuffMaxArr[i]);
    }

    // Stores the maximum sum of any pair
    int MinimumSum = Int32.MaxValue;

    // Stores the minimum of suffixes
    // from the given array
    int[] SuffMinArr = new int[N];

    // Set the last element
    SuffMinArr[N - 1] = Int32.MaxValue;

    // Traverse the remaining array
    for(int i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMinArr[i] = Math.Min(SuffMinArr[i + 1],
                                          A[i + 1]);
    }

    // Calculate the minimum sum
    for(int i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMinArr[i])
        {
            MinimumSum = Math.Min(MinimumSum,
                                  A[i] + SuffMinArr[i]);
        }
    }

    // Return the resultant difference
    return Math.Abs(MaximumSum - MinimumSum);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 2, 4, 1, 3, 7, 5, 6 };
    int N = arr.Length;

    // Function Call
    Console.WriteLine(GetDiff(arr, N));
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the difference between
// the maximum and minimum sum of a pair
// (arr[i], arr[j]) from the array such
// that i < j and arr[i] < arr[j]
function GetDiff(A, N)
{

    // Stores the maximum from
    // the suffix of the array
    let SuffMaxArr = Array(N).fill(0);

    // Set the last element
    SuffMaxArr[N - 1] = A[N - 1];

    // Traverse the remaining array
    for(let i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMaxArr[i] = Math.max(SuffMaxArr[i + 1],
                                          A[i + 1]);
    }

    // Stores the maximum sum of any pair
    let MaximumSum = Number.MIN_VALUE;

    // Calculate the maximum sum
    for(let i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMaxArr[i])
            MaximumSum = Math.max(MaximumSum,
                                  A[i] + SuffMaxArr[i]);
    }

    // Stores the maximum sum of any pair
    let MinimumSum = Number.MAX_VALUE;

    // Stores the minimum of suffixes
    // from the given array
    let SuffMinArr = Array(N).fill(0);

    // Set the last element
    SuffMinArr[N - 1] = Number.MAX_VALUE;

    // Traverse the remaining array
    for(let i = N - 2; i >= 0; --i)
    {

        // Update the maximum from suffix
        // for the remaining indices
        SuffMinArr[i] = Math.min(SuffMinArr[i + 1],
                                          A[i + 1]);
    }

    // Calculate the minimum sum
    for(let i = 0; i < N - 1; i++)
    {
        if (A[i] < SuffMinArr[i])
        {
            MinimumSum = Math.min(MinimumSum,
                                  A[i] + SuffMinArr[i]);
        }
    }

    // Return the resultant difference
    return Math.abs(MaximumSum - MinimumSum);
}

// Driver Code

    let arr = [ 2, 4, 1, 3, 7, 5, 6 ];
    let N = arr.length;

    // Function Call
    document.write(GetDiff(arr, N));

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)