# 将给定的阵列分割成子阵列，以最大化每个子阵列中的最大值和最小值之和

> 原文:[https://www . geeksforgeeks . org/将给定阵列拆分为子阵列，以最大化每个子阵列中的最大值和最小值之和/](https://www.geeksforgeeks.org/split-given-arrays-into-subarrays-to-maximize-the-sum-of-maximum-and-minimum-in-each-subarrays/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过将给定数组拆分成不重叠的子数组来最大化每个子数组中[个最大值和最小值之差的和。](https://www.geeksforgeeks.org/sum-minimum-maximum-elements-subarrays-size-k/)

**示例:**

> **输入:** arr[] = {8，1，7，9，2}
> **输出:** 14
> **解释:**
> 将给定数组 arr[]拆分为{8，1}、{7，9，2}。现在，所有子阵列的差值最大值和最小值之和为(8–7)+(9–2)= 7+7 = 14，这是所有可能组合中的最大值。
> 
> **输入:** arr[] = {1，2，1，0，5}
> **输出:** 6

**方法:**给定的问题可以通过考虑所有可能的子阵列的断裂来解决，并找到每个子阵列中最大值和最小值之差的和，并将该值最大化。这个想法可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来实现。按照以下步骤解决给定的问题:

*   初始化一个数组， **dp[]** ，所有元素为 **0** ，这样 **dp[i]** 存储第一个 **i** 元素所有可能的分裂之和，这样每个子数组中最大值和最小值之差之和最大。
*   使用变量 **i** 遍历给定数组 **arr[]** ，并执行以下步骤:
    *   选择当前值作为子阵列的[最大和最小元素，并将其存储在变量中，分别表示为**最小值**和**最大值**。](https://www.geeksforgeeks.org/find-the-maximum-of-minimums-for-every-window-size-in-a-given-array/)
    *   使用变量 **j** 在范围**【0，I】**内循环，并执行以下步骤:
        *   用数组元素**arr【j】**更新**最小值**和**最大值**。
        *   如果 **j** 的值为正，则更新**DP【I】**为**DP【I】**和**的最大值(最大值–最小值+DP【j–1】)**。否则，将 **dp[i]** 更新为 **dp[i]** 和**(maxValue–minValue)**的最大值。
*   完成上述步骤后，打印**DP【N–1】**的值作为最终最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// differences of subarrays by splitting
// array into non-overlapping subarrays
int maxDiffSum(int arr[], int n)
{
    // Stores the answer for prefix
    // and initialize with zero
    int dp[n];
    memset(dp, 0, sizeof(dp));

    // Assume i-th index as right endpoint
    for (int i = 0; i < n; i++) {

        // Choose the current value as
        // the maximum and minimum
        int maxVal = arr[i], minVal = arr[i];

        // Find the left endpoint and
        // update the array dp[]
        for (int j = i; j >= 0; j--) {
            minVal = min(minVal, arr[j]);
            maxVal = max(maxVal, arr[j]);

            if (j - 1 >= 0)
                dp[i] = max(
                    dp[i], maxVal - minVal + dp[j - 1]);
            else
                dp[i] = max(
                    dp[i], maxVal - minVal);
        }
    }

    // Return answer
    return dp[n - 1];
}

// Driver Code
int main()
{
    int arr[] = { 8, 1, 7, 9, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxDiffSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find the maximum sum of
    // differences of subarrays by splitting
    // array into non-overlapping subarrays
    static int maxDiffSum(int[] arr, int n)
    {

        // Stores the answer for prefix
        // and initialize with zero
        int[] dp = new int[n];

        // Assume i-th index as right endpoint
        for (int i = 0; i < n; i++) {

            // Choose the current value as
            // the maximum and minimum
            int maxVal = arr[i], minVal = arr[i];

            // Find the left endpoint and
            // update the array dp[]
            for (int j = i; j >= 0; j--) {
                minVal = Math.min(minVal, arr[j]);
                maxVal = Math.max(maxVal, arr[j]);

                if (j - 1 >= 0)
                    dp[i] = Math.max(
                        dp[i], maxVal - minVal + dp[j - 1]);
                else
                    dp[i]
                        = Math.max(dp[i], maxVal - minVal);
            }
        }

        // Return answer
        return dp[n - 1];
    }

    // Driver Code
    public static void main(String []args)
    {
        int[] arr = { 8, 1, 7, 9, 2 };
        int N = arr.length;

        System.out.print(maxDiffSum(arr, N));
    }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the maximum sum of
# differences of subarrays by splitting
# array into non-overlapping subarrays
def maxDiffSum(arr, n):

    # Stores the answer for prefix
    # and initialize with zero
    dp = [0] * n

    # Assume i-th index as right endpoint
    for i in range(n):

        # Choose the current value as
        # the maximum and minimum
        maxVal = arr[i]
        minVal = arr[i]

        # Find the left endpoint and
        # update the array dp[]
        for j in range(i, -1, -1):
            minVal = min(minVal, arr[j])
            maxVal = max(maxVal, arr[j])

            if (j - 1 >= 0):
                dp[i] = max(
                    dp[i], maxVal - minVal + dp[j - 1])
            else:
                dp[i] = max(
                    dp[i], maxVal - minVal)

    # Return answer
    return dp[n - 1]

# Driver Code
arr = [8, 1, 7, 9, 2]
N = len(arr)

print(maxDiffSum(arr, N))

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the maximum sum of
    // differences of subarrays by splitting
    // array into non-overlapping subarrays
    static int maxDiffSum(int[] arr, int n)
    {

        // Stores the answer for prefix
        // and initialize with zero
        int[] dp = new int[n];

        // Assume i-th index as right endpoint
        for (int i = 0; i < n; i++) {

            // Choose the current value as
            // the maximum and minimum
            int maxVal = arr[i], minVal = arr[i];

            // Find the left endpoint and
            // update the array dp[]
            for (int j = i; j >= 0; j--) {
                minVal = Math.Min(minVal, arr[j]);
                maxVal = Math.Max(maxVal, arr[j]);

                if (j - 1 >= 0)
                    dp[i] = Math.Max(
                        dp[i], maxVal - minVal + dp[j - 1]);
                else
                    dp[i]
                        = Math.Max(dp[i], maxVal - minVal);
            }
        }

        // Return answer
        return dp[n - 1];
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 8, 1, 7, 9, 2 };
        int N = arr.Length;

        Console.WriteLine(maxDiffSum(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum sum of
       // differences of subarrays by splitting
       // array into non-overlapping subarrays
       function maxDiffSum(arr, n)
       {

           // Stores the answer for prefix
           // and initialize with zero
           let dp = new Array(n).fill(0);

           // Assume i-th index as right endpoint
           for (let i = 0; i < n; i++) {

               // Choose the current value as
               // the maximum and minimum
               let maxVal = arr[i], minVal = arr[i];

               // Find the left endpoint and
               // update the array dp[]
               for (let j = i; j >= 0; j--) {
                   minVal = Math.min(minVal, arr[j]);
                   maxVal = Math.max(maxVal, arr[j]);

                   if (j - 1 >= 0)
                       dp[i] = Math.max(
                           dp[i], maxVal - minVal + dp[j - 1]);
                   else
                       dp[i] = Math.max(
                           dp[i], maxVal - minVal);
               }
           }

           // Return answer
           return dp[n - 1];
       }

       // Driver Code
       let arr = [8, 1, 7, 9, 2];
       let N = arr.length;

       document.write(maxDiffSum(arr, N));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*