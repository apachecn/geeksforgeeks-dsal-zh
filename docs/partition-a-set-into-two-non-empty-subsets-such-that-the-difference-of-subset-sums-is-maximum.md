# 将一个集合划分为两个非空子集，使得子集和的差最大

> 原文:[https://www . geeksforgeeks . org/partition-a-set-in-two-non-empty-subset-sums-different-of-subset-sums-max/](https://www.geeksforgeeks.org/partition-a-set-into-two-non-empty-subsets-such-that-the-difference-of-subset-sums-is-maximum/)

给定一组整数 **S** ，任务是将给定的集合分成两个非空集合 **S1** 和 **S2** ，使得它们的和之间的绝对差最大，即 **abs(和(S1)–和(S2))** 最大。

**示例:**

> **输入:** S[] = { 1，2，1 }
> **输出:** 2
> **说明:**
> 子集为{1}和{2，1 }。它们的绝对差是
> ABS(1 –( 2+1))= 2，最大。
> 
> **输入:** S[] = { -2，3，-1，5 }
> **输出:** 11
> **说明:**
> 子集为{-1，-2}和{3，5 }。它们的绝对差是
> abs((-1，-2)–(3+5))= 11，最大。

**天真法:**生成并存储整数集合的所有子集，求子集之和与集合之和与该子集之和之差的最大绝对差，即***ABS(sum(S1)–(totalSum–sum(S1))***。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*

**高效方法:**优化幼稚方法，思路是用一些数学观察。这个问题可以分为两种情况:

*   如果集合只包含正整数或负整数，那么最大差值是通过拆分集合得到的，使得一个子集只包含集合的最小元素，而另一个子集包含集合的所有剩余元素，即，

> ***ABS((total sum–min(S))–min(S))***或***ABS(total sum–2×min(S))**、*其中 **S** 为整数集

*   如果集合同时包含正整数和负整数，则最大差值通过拆分集合来获得，使得一个子集包含所有正整数，而另一个子集包含所有负整数，即，

> ***ABS(sum(S1)–sum(S2)***或***ABS(sum(S)***其中 **S1、S2** 分别为正整数和负整数的集合。

下面是上述方法的实现:

## C++

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// difference between the subset sums
int maxDiffSubsets(int arr[], int N)
{
    // Stores the total
    // sum of the array
    int totalSum = 0;

    // Checks for positive
    // and negative elements
    bool pos = false, neg = false;

    // Stores the minimum element
    // from the given array
    int min = INT_MAX;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        // Calculate total sum
        totalSum += abs(arr[i]);

        // Mark positive element
        // present in the set
        if (arr[i] > 0)
            pos = true;

        // Mark negative element
        // present in the set
        if (arr[i] < 0)
            neg = true;

        // Find the minimum
        // element of the set
        if (arr[i] < min)
            min = arr[i];
    }

    // If the array contains both
    // positive and negative elements
    if (pos && neg)
        return totalSum;

    // Otherwise
    else
        return totalSum - 2 * min;
}

// Driver Code
int main()
{
    // Given the array
    int S[] = {1, 2, 1};

    // Length of the array
    int N = sizeof(S) / sizeof(S[0]);

    if (N < 2)
        cout << ("Not Possible");

    else
        // Function Call
        cout << (maxDiffSubsets(S, N));
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to return the maximum
    // difference between the subset sums
    static int maxDiffSubsets(int[] arr)
    {
        // Stores the total
        // sum of the array
        int totalSum = 0;

        // Checks for positive
        // and negative elements
        boolean pos = false, neg = false;

        // Stores the minimum element
        // from the given array
        int min = Integer.MAX_VALUE;

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // Calculate total sum
            totalSum += Math.abs(arr[i]);

            // Mark positive element
            // present in the set
            if (arr[i] > 0)
                pos = true;

            // Mark negative element
            // present in the set
            if (arr[i] < 0)
                neg = true;

            // Find the minimum
            // element of the set
            if (arr[i] < min)
                min = arr[i];
        }

        // If the array contains both
        // positive and negative elements
        if (pos && neg)
            return totalSum;

        // Otherwise
        else
            return totalSum - 2 * min;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given the array
        int[] S = { 1, 2, 1 };

        // Length of the array
        int N = S.length;

        if (N < 2)
            System.out.println("Not Possible");

        else
            // Function Call
            System.out.println(maxDiffSubsets(S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach
import sys

# Function to return the maximum
# difference between the subset sums
def maxDiffSubsets(arr):

    # Stores the total
    # sum of the array
    totalSum = 0

    # Checks for positive
    # and negative elements
    pos = False
    neg = False

    # Stores the minimum element
    # from the given array
    min = sys.maxsize

    # Traverse the array
    for i in range(len(arr)):

        # Calculate total sum
        totalSum += abs(arr[i])

        # Mark positive element
        # present in the set
        if (arr[i] > 0):
            pos = True

        # Mark negative element
        # present in the set
        if (arr[i] < 0):
            neg = True

        # Find the minimum
        # element of the set
        if (arr[i] < min):
            min = arr[i]

    # If the array contains both
    # positive and negative elements
    if (pos and neg):
        return totalSum

    # Otherwise
    else:
        return totalSum - 2 * min

# Driver Code
if __name__ == '__main__':

    # Given the array
    S = [ 1, 2, 1 ]

    # Length of the array
    N = len(S)

    if (N < 2):
        print("Not Possible")
    else:

        # Function Call
        print(maxDiffSubsets(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program for above approach
using System;
class GFG{

    // Function to return the maximum
    // difference between the subset sums
    static int maxDiffSubsets(int[] arr)
    {
        // Stores the total
        // sum of the array
        int totalSum = 0;

        // Checks for positive
        // and negative elements
        bool pos = false, neg = false;

        // Stores the minimum element
        // from the given array
        int min = int.MaxValue;

        // Traverse the array
        for (int i = 0; i < arr.Length; i++)
        {
            // Calculate total sum
            totalSum += Math.Abs(arr[i]);

            // Mark positive element
            // present in the set
            if (arr[i] > 0)
                pos = true;

            // Mark negative element
            // present in the set
            if (arr[i] < 0)
                neg = true;

            // Find the minimum
            // element of the set
            if (arr[i] < min)
                min = arr[i];
        }

        // If the array contains both
        // positive and negative elements
        if (pos && neg)
            return totalSum;

        // Otherwise
        else
            return totalSum - 2 * min;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given the array
        int[] S = {1, 2, 1};

        // Length of the array
        int N = S.Length;

        if (N < 2)
            Console.WriteLine("Not Possible");
        else

            // Function Call
            Console.WriteLine(maxDiffSubsets(S));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript Program for above approach
    // Function to return the maximum
    // difference between the subset sums
    function maxDiffSubsets(arr) {
        // Stores the total
        // sum of the array
        var totalSum = 0;

        // Checks for positive
        // and negative elements
        var pos = false, neg = false;

        // Stores the minimum element
        // from the given array
        var min = Number.MAX_VALUE;

        // Traverse the array
        for (i = 0; i < arr.length; i++) {

            // Calculate total sum
            totalSum += Math.abs(arr[i]);

            // Mark positive element
            // present in the set
            if (arr[i] > 0)
                pos = true;

            // Mark negative element
            // present in the set
            if (arr[i] < 0)
                neg = true;

            // Find the minimum
            // element of the set
            if (arr[i] < min)
                min = arr[i];
        }

        // If the array contains both
        // positive and negative elements
        if (pos && neg)
            return totalSum;

        // Otherwise
        else
            return totalSum - 2 * min;
    }

    // Driver Code

        // Given the array
        var S = [ 1, 2, 1 ];

        // Length of the array
        var N = S.length;

        if (N < 2)
            document.write("Not Possible");

        else
            // Function Call
            document.write(maxDiffSubsets(S));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)