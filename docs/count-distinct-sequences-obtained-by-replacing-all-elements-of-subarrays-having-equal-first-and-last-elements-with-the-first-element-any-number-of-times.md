# 对通过用第一个元素替换具有相等的第一个和最后一个元素的子阵列的所有元素任意次数获得的不同序列进行计数

> 原文:[https://www . geeksforgeeks . org/count-distinct-sequence-通过用任意次数的第一个元素替换子数组中具有相等的第一个和最后一个元素的所有元素获得/](https://www.geeksforgeeks.org/count-distinct-sequences-obtained-by-replacing-all-elements-of-subarrays-having-equal-first-and-last-elements-with-the-first-element-any-number-of-times/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在给定数组**arr【】**上执行以下操作任意多次后，找出可以形成的不同序列的数量。

> 选择两个索引 **i** 和 **j** ，使得**arr【I】**等于**arr【j】**，并将数组中**【I，j】**范围内的所有元素更新为**arr【I】**。

**示例:**

> **输入:** arr[] = {1，2，1，2，2}
> **输出:** 3
> **解释:**
> 可以有三种可能的顺序:
> 
> 1.  初始数组{1，2，1，2，2}。
> 2.  选择索引 0 和 2，当 arr[0](= 1)和 arr[2](= 1)相等时，在[0，2]到 arr[0](= 1)的范围内更新数组元素 arr[]。获得的新序列是{1，1，1，2，2}。
> 3.  选择索引 1 和 3，当 arr[1](= 2)和 arr[3](= 2)相等时，将数组元素 arr[]在范围[1，3]内更新为 arr[1](= 2)。得到的新序列是{1，2，2，2，2}。
> 
> 因此，形成的序列总数是 3。
> 
> **输入:** arr[] = {4，2，5，4，2，4 }
> T3】输出: 5

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决问题:

*   初始化辅助数组 **dp[]** ，其中 **dp[i]** 存储给定数组 **arr[]** 的第一个 **i** 元素可能的不同序列的数量，并将 **dp[0]** 初始化为 **1** 。
*   初始化一个数组**last occurrence[]**，其中**last occurrence[I]**存储元素 **arr[i]** 在[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr[]** 的第一个 **i** 元素中的最后一个出现，并用 **-1** 初始化**last occurrence[0]**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   将 **dp[i]** 的值更新为**DP[I–1]**。
    *   如果当前元素的最后一次出现不等于 **-1** 且小于**(I–1)**，则将 **dp【最后一次出现【curEle】】**的值加到**DP【I】**上。
    *   将**最后一次出现的【curEle】**的值更新为 **i** 。
*   完成上述步骤后，打印**DP【N】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of sequences
// satisfying the given criteria
void countPossiblities(int arr[], int n)
{
    // Stores the index of the last
    // occurrence of the element
    int lastOccur[100000];
    for (int i = 0; i < n; i++) {
        lastOccur[i] = -1;
    }

    // Initialize an array to store the
    // number of different sequences
    // that are possible of length i
    int dp[n + 1];

    // Base Case
    dp[0] = 1;

    for (int i = 1; i <= n; i++) {

        int curEle = arr[i - 1];

        // If no operation is applied
        // on ith element
        dp[i] = dp[i - 1];

        // If operation is applied on
        // ith element
        if (lastOccur[curEle] != -1
            & lastOccur[curEle] < i - 1) {
            dp[i] += dp[lastOccur[curEle]];
        }

        // Update the last occurrence
        // of curEle
        lastOccur[curEle] = i;
    }

    // Finally, print the answer
    cout << dp[n] << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countPossiblities(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG {

    // Function to count number of sequences
    // satisfying the given criteria
    static void countPossiblities(int arr[], int n)
    {
        // Stores the index of the last
        // occurrence of the element
        int[] lastOccur = new int[100000];
        for (int i = 0; i < n; i++) {
            lastOccur[i] = -1;
        }

        // Initialize an array to store the
        // number of different sequences
        // that are possible of length i
        int[] dp = new int[n + 1];

        // Base Case
        dp[0] = 1;

        for (int i = 1; i <= n; i++) {

            int curEle = arr[i - 1];

            // If no operation is applied
            // on ith element
            dp[i] = dp[i - 1];

            // If operation is applied on
            // ith element
            if (lastOccur[curEle] != -1
                & lastOccur[curEle] < i - 1) {
                dp[i] += dp[lastOccur[curEle]];
            }

            // Update the last occurrence
            // of curEle
            lastOccur[curEle] = i;
        }

        // Finally, print the answer
        System.out.println(dp[n]);
    }

    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 1, 2, 2 };
        int N = arr.length;
        countPossiblities(arr, N);

    }
}

    // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count number of sequences
# satisfying the given criteria
def countPossiblities(arr, n):

    # Stores the index of the last
    # occurrence of the element
    lastOccur = [-1] * 100000

    # Initialize an array to store the
    # number of different sequences
    # that are possible of length i
    dp = [0] * (n + 1)

    # Base Case
    dp[0] = 1

    for i in range(1, n + 1):
        curEle = arr[i - 1]

        # If no operation is applied
        # on ith element
        dp[i] = dp[i - 1]

        # If operation is applied on
        # ith element
        if (lastOccur[curEle] != -1 and
            lastOccur[curEle] < i - 1):
            dp[i] += dp[lastOccur[curEle]]

        # Update the last occurrence
        # of curEle
        lastOccur[curEle] = i

    # Finally, print the answer
    print(dp[n])

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 1, 2, 2 ]
    N = len(arr)

    countPossiblities(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program for the above approach
using System;

class GFG {

    // Function to count number of sequences
    // satisfying the given criteria
    static void countPossiblities(int[] arr, int n)
    {
        // Stores the index of the last
        // occurrence of the element
        int[] lastOccur = new int[100000];
        for (int i = 0; i < n; i++) {
            lastOccur[i] = -1;
        }

        // Initialize an array to store the
        // number of different sequences
        // that are possible of length i
        int[] dp = new int[n + 1];

        // Base Case
        dp[0] = 1;

        for (int i = 1; i <= n; i++) {

            int curEle = arr[i - 1];

            // If no operation is applied
            // on ith element
            dp[i] = dp[i - 1];

            // If operation is applied on
            // ith element
            if (lastOccur[curEle] != -1
                & lastOccur[curEle] < i - 1) {
                dp[i] += dp[lastOccur[curEle]];
            }

            // Update the last occurrence
            // of curEle
            lastOccur[curEle] = i;
        }

        // Finally, print the answer
        Console.WriteLine(dp[n]);
    }

    public static void Main()
    {
        int[] arr = { 1, 2, 1, 2, 2 };
        int N = arr.Length;
        countPossiblities(arr, N);
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to count number of sequences
       // satisfying the given criteria
       function countPossiblities(arr, n)
       {

           // Stores the index of the last
           // occurrence of the element
           let lastOccur = new Array(100000);
           for (let i = 0; i < n; i++) {
               lastOccur[i] = -1;
           }

           // Initialize an array to store the
           // number of different sequences
           // that are possible of length i
           dp = new Array(n + 1);

           // Base Case
           dp[0] = 1;

           for (let i = 1; i <= n; i++) {

               let curEle = arr[i - 1];

               // If no operation is applied
               // on ith element
               dp[i] = dp[i - 1];

               // If operation is applied on
               // ith element
               if (lastOccur[curEle] != -1
                   & lastOccur[curEle] < i - 1) {
                   dp[i] += dp[lastOccur[curEle]];
               }

               // Update the last occurrence
               // of curEle
               lastOccur[curEle] = i;
           }

           // Finally, prlet the answer
           document.write(dp[n] + "<br>");
       }

       // Driver Code

       let arr = [1, 2, 1, 2, 2];
       let N = arr.length;
       countPossiblities(arr, N);

   // This code is contributed by Potta Lokesh

   </script>
```

**输出:**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)