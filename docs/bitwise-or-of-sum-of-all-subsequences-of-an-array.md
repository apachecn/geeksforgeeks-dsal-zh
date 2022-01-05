# 一个数组的所有子序列之和的位或

> 原文:[https://www . geesforgeks . org/数组所有子序列的按位或和/](https://www.geeksforgeeks.org/bitwise-or-of-sum-of-all-subsequences-of-an-array/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定数组中找到所有可能的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)之和的[位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {4，2，5}
> **输出:** 15
> **解释:**给定数组的所有子序列及其对应的和:
> { 4 }–4
> { 2 }–2
> { 5 }–5
> { 4，2 }–6
> { 4，5 }–9
> { 2，5 }–7
> { 4，2，5} -11
> 
> **输入:** arr[] = {1，9，8}
> **输出:** 27
> **解释:**给定数组的所有子序列及其对应的和:
> { 1 }–1
> { 9 }–9
> { 8 }–8
> { 1，9 }–10
> { 9，8 }–17
> { 1，8 }–9
> { 1，9，8 }–17

**天真方法:**最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)中生成所有可能的子序列，并找到它们各自的和。现在，在计算它们的和之后，打印所有获得的和的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

*   数组元素中的所有[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)也在最终结果中设置。
*   给定数组的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)中设置的所有位也在最终结果中设置。

按照以下步骤解决上述问题:

*   用 **0** 初始化变量**结果**，该变量存储给定数组 **arr[]** 的每个子序列之和的**位“或”**。
*   用 **0** 初始化一个变量**前缀**，该变量随时存储**arr【】**的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [使用变量 **i** 迭代范围**【0，N】**中的数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)。
    *   将**前缀**更新为**前缀+= arr[i]** 。
    *   将**结果**更新为**结果| = arr[i] | prefixSum。**
*   完成上述步骤后，打印**结果**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate Bitwise OR of
// sums of all subsequences
int findOR(int nums[], int N)
{
    // Stores the prefix sum of nums[]
    int prefix_sum = 0;

    // Stores the bitwise OR of
    // sum of each subsequence
    int result = 0;

    // Iterate through array nums[]
    for (int i = 0; i < N; i++) {

        // Bits set in nums[i] are
        // also set in result
        result |= nums[i];

        // Calculate prefix_sum
        prefix_sum += nums[i];

        // Bits set in prefix_sum
        // are also set in result
        result |= prefix_sum;
    }

    // Return the result
    return result;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 2, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findOR(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate Bitwise OR of
// sums of all subsequences
static int findOR(int nums[], int N)
{
    // Stores the prefix sum of nums[]
    int prefix_sum = 0;

    // Stores the bitwise OR of
    // sum of each subsequence
    int result = 0;

    // Iterate through array nums[]
    for (int i = 0; i < N; i++) {

        // Bits set in nums[i] are
        // also set in result
        result |= nums[i];

        // Calculate prefix_sum
        prefix_sum += nums[i];

        // Bits set in prefix_sum
        // are also set in result
        result |= prefix_sum;
    }

    // Return the result
    return result;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 4, 2, 5 };
    int N = arr.length;
    System.out.print(findOR(arr, N));
}
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to calculate
# Bitwise OR of sums of
# all subsequences
def findOR(nums,  N):

    # Stores the prefix
    # sum of nums[]
    prefix_sum = 0

    # Stores the bitwise OR of
    # sum of each subsequence
    result = 0

    # Iterate through array nums[]
    for i in range(N):

        # Bits set in nums[i] are
        # also set in result
        result |= nums[i]

        # Calculate prefix_sum
        prefix_sum += nums[i]

        # Bits set in prefix_sum
        # are also set in result
        result |= prefix_sum

    # Return the result
    return result

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [4, 2, 5]

    N = len(arr)

    # Function Call
    print(findOR(arr, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate Bitwise OR of
// sums of all subsequences
static int findOR(int[] nums, int N)
{

    // Stores the prefix sum of nums[]
    int prefix_sum = 0;

    // Stores the bitwise OR of
    // sum of each subsequence
    int result = 0;

    // Iterate through array nums[]
    for(int i = 0; i < N; i++)
    {

        // Bits set in nums[i] are
        // also set in result
        result |= nums[i];

        // Calculate prefix_sum
        prefix_sum += nums[i];

        // Bits set in prefix_sum
        // are also set in result
        result |= prefix_sum;
    }

    // Return the result
    return result;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 4, 2, 5 };

    // Size of array
    int N = arr.Length;

    // Function call
    Console.Write(findOR(arr, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate Bitwise OR of
// sums of all subsequences
function findOR(nums, N)
{
    // Stores the prefix sum of nums[]
    let prefix_sum = 0;

    // Stores the bitwise OR of
    // sum of each subsequence
    let result = 0;

    // Iterate through array nums[]
    for (let i = 0; i < N; i++) {

        // Bits set in nums[i] are
        // also set in result
        result |= nums[i];

        // Calculate prefix_sum
        prefix_sum += nums[i];

        // Bits set in prefix_sum
        // are also set in result
        result |= prefix_sum;
    }

    // Return the result
    return result;
}

// Driver Code

   // Given array arr[]
    let arr = [ 4, 2, 5 ];
    let N = arr.length;
    document.write(findOR(arr, N));

  // This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)