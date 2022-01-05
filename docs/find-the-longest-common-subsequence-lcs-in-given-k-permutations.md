# 在给定的 K 个排列中找到最长的公共子序列(LCS)

> 原文:[https://www . geesforgeks . org/find-最长公共子序列-给定 k 排列中的 LCS/](https://www.geeksforgeeks.org/find-the-longest-common-subsequence-lcs-in-given-k-permutations/)

给定 2D 数组中从 **1 到 N** 的数字排列 **arr[][]** 。任务是找到这 K 个排列中[最长的公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)。

**示例:**

> **输入:** N = 4，K = 3
> arr[][] = {{1，4，2，3}，
> {4，1，2，3}，
> {1，2，4，3}}
> **输出:** 3
> **说明:**最长的公共子序列是{1，2，3}，长度为 3。
> 
> **输入:** N = 6，K = 3，
> arr[][] = {{2，5，1，4，6，3}，
> {5，1，4，3，2，6}，
> {5，4，2，6，3，1}}
> **输出:** 3
> **解释:**最长的公共子序列是{5，4，6}，其长度为 3。

**方法:**这个问题是[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)的扩展。解决方案基于[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)的概念。请遵循以下步骤:

*   创建一个 **2D 数组**(位置[][])来存储每个序列中从 1 到 N 的所有数字的**位置**，，其中位置【I】【j】表示序列中**值 j 的位置。**
*   初始化一个数组(dp[])，其中 **dp[i]** 存储在位置 i 结束的最长公共子序列**。**
    *   将**第一个序列作为参考**，对于**第一个序列的每个元素**，检查它们在其他序列中的**相对位置**。
        *   迭代所有可能的索引 j，使得 **j < i** 并且查看在**第一序列**的**索引 i** 处的值是否可以被**附加到在 j** 处结束的最长递增子序列**上。**
        *   这是通过检查数字 **arr[0][j]** 的**位置**是否小于等于所有排列中**值 arr[0][i]** 的位置来实现的。那么 arr[0][i]处的值可以被附加到结束于位置 j 的序列中。
*   所以递归为 **dp[i] = max(dp[i]，1 + dp[j])** 。
*   数组 dp[]中的**最大值**就是答案。

请参见下图:

> 插图:
> 
> 举个例子:
> **N** = 4， **K** = 3， **arr[][]** = {{1，4，2，3}，
> {4，1，2，3}，
> {1，2，4，3}}
> 
> 1.  **组成位置数组:** pos[][] = {{1，3，4，2}，
>     {2，3，4，1}，
>     {1，2，4，3}}
>     在第一个序列中，1 在第一个位置，2 在第三个位置，3 在第四个位置，4 在第二个位置。其他序列也是如此。
> 2.  我**初始化 dp[]数组:**初始化 dp[]数组，它最初 **dp[] = {0，0，0，0}**
> 3.  **参考序列:**第一个序列 i{1，4，2，3}用作参考序列，即根据这个序列检查其他序列中元素的相对位置。
> 4.  **对于 i = 1:** dp[1] = 1，因为长度为 1 的任何序列都是递增序列。现在 **dp[] = {1，0，0，0}**
> 5.  **对于 i = 2:** 现在将在所有 3 个序列中检查 4 和 1 的相对位置。在第二序列和第三序列中，不保持相对位置。所以 dp[2] = dp[1]。现在 **dp[] = {1，1，0，0}** 。
> 6.  **对于 i = 3:** 检查(1，4，2)的相对位置。
>     当 j = 1，即值 1 和 2 的相对位置被检查时，它满足范围**【1，K】**中所有 **ind** 的条件**pos【ind】【arr【1】【1】】<pos【ind】【arr【1】【3】】**。所以 dp[3] = max(dp[3]，dp[1]+1) = max(0，2) = 2。
>     **现在 dp[] = {1，1，2，0}**
> 7.  **对于 i = 4:** 此处同样当 j = 3 时，则**pos[ind][arr[1][3]]<pos[ind][arr[1][4]]**对于范围**【1，K】**内的所有 **ind** 。因此，第一个序列的第四个元素可以追加到以第三个索引结束的最长递增子序列中。dp[4] = dp[3] + 1 = 2 + 1 = 3。
>     **现在 dp[] = {1，1，2，3}**
> 8.  ****DP[]中的最大**值为 3** 。因此，最长递增子序列的最大长度为 3。
> 
> **注意:**实际实现中使用的是基于 0 的索引。这里使用基于 1 的索引以便于理解

下面是上述方法的实现。

## C++

```
// C++ code to find the longest common
// sub sequence of k permutations.
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest common
// sub sequence of k permutations.
int findLcs(vector<vector<int>> &arr,
            int n, int k)
{
    // Variable to keep track of the length
    // of the longest common sub sequence
    int maxLen = 0;

    // position array to keep track
    // of position of elements
    // in each permutation
    int pos[k][n];

    // Array to store the length of LCS
    int dp[n];

    for (int i = 0; i < k; i++)
    {
        for (int j = 0; j < n; j++)
        {
            pos[i][arr[i][j] - 1] = j;
        }
    }

    // Loop to calculate the LCS
    // of all the permutations
    for (int i = 0; i < n; i++)
    {
        dp[i] = 1;
        for (int j = 0; j < i; j++)
        {
            bool good = true;
            for (int p = 0; p < k; p++)
            {
                if (pos[p][arr[0][j] - 1]
                    > pos[p][arr[0][i] - 1])
                {
                    good = false;
                    break;
                }
            }
            if (good)
            {
                dp[i] = max(dp[i], 1 + dp[j]);
                maxLen = max(maxLen, dp[i]);
            }
        }
    }
    return maxLen;
}

// Driver code
int main()
{
    vector<vector<int>> arr =
    {{2, 5, 1, 4, 6, 3},
     {5, 1, 4, 3, 2, 6},
     {5, 4, 2, 6, 3, 1}};
    int N = arr[0].size();
    int K = 3;

    // Function Call
    cout << findLcs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the longest common
// sub sequence of k permutations.
import java.util.*;

class GFG{

// Function to find the longest common
// sub sequence of k permutations.
static int findLcs(int[][]arr,
            int n, int k)
{
    // Variable to keep track of the length
    // of the longest common sub sequence
    int maxLen = 0;

    // position array to keep track
    // of position of elements
    // in each permutation
    int [][]pos = new int[k][n];

    // Array to store the length of LCS
    int []dp = new int[n];

    for (int i = 0; i < k; i++)
    {
        for (int j = 0; j < n; j++)
        {
            pos[i][arr[i][j] - 1] = j;
        }
    }

    // Loop to calculate the LCS
    // of all the permutations
    for (int i = 0; i < n; i++)
    {
        dp[i] = 1;
        for (int j = 0; j < i; j++)
        {
            boolean good = true;
            for (int p = 0; p < k; p++)
            {
                if (pos[p][arr[0][j] - 1]
                    > pos[p][arr[0][i] - 1])
                {
                    good = false;
                    break;
                }
            }
            if (good)
            {
                dp[i] = Math.max(dp[i], 1 + dp[j]);
                maxLen = Math.max(maxLen, dp[i]);
            }
        }
    }
    return maxLen;
}

// Driver code
public static void main(String[] args)
{
    int[][] arr =
    {{2, 5, 1, 4, 6, 3},
     {5, 1, 4, 3, 2, 6},
     {5, 4, 2, 6, 3, 1}};
    int N = arr[0].length;
    int K = 3;

    // Function Call
    System.out.print(findLcs(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the longest common
# sub sequence of k permutations.
def findLcs(arr, n, k):

    # Variable to keep track of the length
    # of the longest common sub sequence
    maxLen = 0

    # position array to keep track
    # of position of elements
    # in each permutation
    pos = [0] * k
    for i in range(len(pos)):
        pos[i] = [0] * n

    # Array to store the length of LCS
    dp = [0] * n

    for i in range(k):
        for j in range(n):
            pos[i][arr[i][j] - 1] = j

    # Loop to calculate the LCS
    # of all the permutations
    for i in range(n):
        dp[i] = 1
        for j in range(i):
            good = True
            for p in range(k):
                if (pos[p][arr[0][j] - 1] > pos[p][arr[0][i] - 1]):
                    good = False
                    break
            if (good):
                dp[i] = max(dp[i], 1 + dp[j])
                maxLen = max(maxLen, dp[i])
    return maxLen

# Driver code
arr = [[2, 5, 1, 4, 6, 3], [5, 1, 4, 3, 2, 6], [5, 4, 2, 6, 3, 1]]
N = len(arr[0])
K = 3

# Function Call
print(findLcs(arr, N, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to find the longest common
// sub sequence of k permutations.
using System;

class GFG {

    // Function to find the longest common
    // sub sequence of k permutations.
    static int findLcs(int[, ] arr, int n, int k)
    {
        // Variable to keep track of the length
        // of the longest common sub sequence
        int maxLen = 0;

        // position array to keep track
        // of position of elements
        // in each permutation
        int[, ] pos = new int[k, n];

        // Array to store the length of LCS
        int[] dp = new int[n];

        for (int i = 0; i < k; i++) {
            for (int j = 0; j < n; j++) {
                pos[i, arr[i, j] - 1] = j;
            }
        }

        // Loop to calculate the LCS
        // of all the permutations
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
            for (int j = 0; j < i; j++) {
                bool good = true;
                for (int p = 0; p < k; p++) {
                    if (pos[p, arr[0, j] - 1]
                        > pos[p, arr[0, i] - 1]) {
                        good = false;
                        break;
                    }
                }
                if (good) {
                    dp[i] = Math.Max(dp[i], 1 + dp[j]);
                    maxLen = Math.Max(maxLen, dp[i]);
                }
            }
        }
        return maxLen;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[, ] arr = { { 2, 5, 1, 4, 6, 3 },
                        { 5, 1, 4, 3, 2, 6 },
                        { 5, 4, 2, 6, 3, 1 } };
        int N = arr.GetLength(1);
        int K = 3;

        // Function Call
        Console.WriteLine(findLcs(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the longest common
       // sub sequence of k permutations.
       function findLcs(arr, n, k)
       {

           // Variable to keep track of the length
           // of the longest common sub sequence
           let maxLen = 0;

           // position array to keep track
           // of position of elements
           // in each permutation
           let pos = new Array(k);
           for (let i = 0; i < pos.length; i++) {
               pos[i] = new Array(n)
           }

           // Array to store the length of LCS
           let dp = new Array(n);

           for (let i = 0; i < k; i++) {
               for (let j = 0; j < n; j++) {
                   pos[i][arr[i][j] - 1] = j;
               }
           }

           // Loop to calculate the LCS
           // of all the permutations
           for (let i = 0; i < n; i++) {
               dp[i] = 1;
               for (let j = 0; j < i; j++) {
                   let good = true;
                   for (let p = 0; p < k; p++) {
                       if (pos[p][arr[0][j] - 1]
                           > pos[p][arr[0][i] - 1]) {
                           good = false;
                           break;
                       }
                   }
                   if (good) {
                       dp[i] = Math.max(dp[i], 1 + dp[j]);
                       maxLen = Math.max(maxLen, dp[i]);
                   }
               }
           }
           return maxLen;
       }

       // Driver code
       let arr =
           [[2, 5, 1, 4, 6, 3],
           [5, 1, 4, 3, 2, 6],
           [5, 4, 2, 6, 3, 1]];
       let N = arr[0].length;
       let K = 3;

       // Function Call
       document.write(findLcs(arr, N, K));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
3
```

**时间复杂度:**O(N<sup>2</sup>* K)
T5】辅助空间: O(N * K)