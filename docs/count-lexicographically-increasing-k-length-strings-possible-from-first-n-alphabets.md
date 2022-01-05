# 从第一个 N 个字母开始计算字典顺序增加的 K 长度字符串

> 原文:[https://www . geeksforgeeks . org/count-按字典顺序递增-k-length-strings-可能从第一个 n 字母开始/](https://www.geeksforgeeks.org/count-lexicographically-increasing-k-length-strings-possible-from-first-n-alphabets/)

给定两个正整数 **N** 和 **K** ，任务是找出可以从第一个 **N** 字母生成的 **K** 长度字符串的数量，以便按字典顺序对字符串中的字符进行排序。

**示例:**

> **输入:** N = 5，K = 2
> **输出:** 15
> **说明:**所有可能的字符串为{“AA”、“AB”、“AC”、“AD”、“AE”、“BB”、“BC”、“BD”、“BE”、“CC”、“CD”、“CE”、“DD”、“DE”、“EE”}。
> 
> **输入:** N = 7，K = 10
> T3】输出: 8008

**天真方法:**解决问题最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来生成所有可能的字符排列，对于每个刺痛，检查字符是否遵循字典顺序递增。打印所有此类字符串的计数。

***时间复杂度:**O(K<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为在递归调用中有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，可以通过使用辅助 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **dp[][]** 来[记忆或列表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)，并计算自下而上方法中每个状态的值。

> **dp[i][j]** 代表用**【j】**不同字母排列**【I】**长度字符串的方法数量。
> **DP[I][j]**=**DP[I][j–1]**(选择不以首字母开头)
> +**DP[I–1][j–1]**(选择字符串中的前 1 个字母作为首字母)
> +**DP[I–2][j–1]**(选择字符串中的前 2 个字母作为首字母)
> + …。
> + …。
> +**DP[0][j–1]**(选择字符串中的前 I 个字母作为第一个字母)
> **dp[i][j]** =第(j-1)列中“I”行的所有值之和

按照以下步骤解决此问题:

*   初始化大小为 **(N+1)** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **列总和[]** ，其中**列总和[i]** 是数组 **dp[][]** 列“j”中所有值的总和。
*   初始化大小为 **(K + 1)*(N + 1)** 的 **dp[][]** 表。
*   将 **dp[0][i]** 初始化为 **1** ，随后更新数组 **columnSum[]** 。
*   分别使用变量 **i** 和 **j** 在 **K** 上迭代两个嵌套循环:
    *   将 **dp[i][j]** 存储为**栏 sum[j–1]**。
    *   将**列总和【j】**更新为**列总和【j】+DP【I】【j】**。
*   完成上述步骤后，打印 **dp[K][N]** 的值作为路的合成数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count K-length
// strings from first N alphabets
void waysToArrangeKLengthStrings(
    int N, int K)
{
    // To keep track of column sum in dp
    int column_sum[N + 1] = { 0 }, i, j;

    // Auxiliary 2d dp array
    int dp[K + 1][N + 1] = { 0 };

    // Initialize dp[0][i] = 1 and
    // update the column_sum
    for (i = 0; i <= N; i++) {
        dp[0][i] = 1;
        column_sum[i] = 1;
    }

    // Iterate for K times
    for (i = 1; i <= K; i++) {

        // Iterate for N times
        for (j = 1; j <= N; j++) {

            // dp[i][j]: Stores the number
            // of ways to form i-length
            // strings consisting of j letters
            dp[i][j] += column_sum[j - 1];

            // Update the column_sum
            column_sum[j] += dp[i][j];
        }
    }

    // Print number of ways to arrange
    // K-length strings with N alphabets
    cout << dp[K][N];
}

// Driver Code
int main()
{
    // Given N and K
    int N = 5, K = 2;

    // Function Call
    waysToArrangeKLengthStrings(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count K-length
// strings from first N alphabets
static void waysToArrangeKLengthStrings(
    int N, int K)
{

    // To keep track of column sum in dp
    int[] column_sum = new int[N + 1];
    int i, j;

    for(i = 1; i < N + 1; i++)
    {
        column_sum[i] = 0;
    }

    // Auxiliary 2d dp array
    int dp[][] = new int[K + 1][N + 1];

    for(i = 1; i < K + 1; i++)
    {
        for(j = 1; j < N + 1; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Initialize dp[0][i] = 1 and
    // update the column_sum
    for(i = 0; i <= N; i++)
    {
        dp[0][i] = 1;
        column_sum[i] = 1;
    }

    // Iterate for K times
    for(i = 1; i <= K; i++)
    {

        // Iterate for N times
        for(j = 1; j <= N; j++)
        {

            // dp[i][j]: Stores the number
            // of ways to form i-length
            // strings consisting of j letters
            dp[i][j] += column_sum[j - 1];

            // Update the column_sum
            column_sum[j] += dp[i][j];
        }
    }

    // Print number of ways to arrange
    // K-length strings with N alphabets
    System.out.print(dp[K][N]);
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 5, K = 2;

    // Function Call
    waysToArrangeKLengthStrings(N, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count K-length
# strings from first N alphabets
def waysToArrangeKLengthStrings(N, K):

    # To keep track of column sum in dp
    column_sum = [0 for i in range(N + 1)]
    i = 0
    j = 0

    # Auxiliary 2d dp array
    dp = [[0 for i in range(N + 1)]
             for j in range(K + 1)]

    # Initialize dp[0][i] = 1 and
    # update the column_sum
    for i in range(N + 1):
        dp[0][i] = 1
        column_sum[i] = 1

    # Iterate for K times
    for i in range(1, K + 1):

        # Iterate for N times
        for j in range(1, N + 1):

            # dp[i][j]: Stores the number
            # of ways to form i-length
            # strings consisting of j letters
            dp[i][j] += column_sum[j - 1]

            # Update the column_sum
            column_sum[j] += dp[i][j]

    # Print number of ways to arrange
    # K-length strings with N alphabets
    print(dp[K][N])

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N = 5
    K = 2

    # Function Call
    waysToArrangeKLengthStrings(N, K)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count K-length
// strings from first N alphabets
static void waysToArrangeKLengthStrings(int N,
                                        int K)
{

    // To keep track of column sum in dp
    int[] column_sum = new int[N + 1];
    int i, j;

    for(i = 1; i < N + 1; i++)
    {
        column_sum[i] = 0;
    }

    // Auxiliary 2d dp array
    int[,] dp = new int[K + 1, N + 1];

    for(i = 1; i < K + 1; i++)
    {
        for(j = 1; j < N + 1; j++)
        {
            dp[i, j] = 0;
        }
    }

    // Initialize dp[0][i] = 1 and
    // update the column_sum
    for(i = 0; i <= N; i++)
    {
        dp[0, i] = 1;
        column_sum[i] = 1;
    }

    // Iterate for K times
    for(i = 1; i <= K; i++)
    {

        // Iterate for N times
        for(j = 1; j <= N; j++)
        {

            // dp[i][j]: Stores the number
            // of ways to form i-length
            // strings consisting of j letters
            dp[i, j] += column_sum[j - 1];

            // Update the column_sum
            column_sum[j] += dp[i, j];
        }
    }

    // Print number of ways to arrange
    // K-length strings with N alphabets
    Console.Write(dp[K, N]);
}

// Driver Code
public static void Main()
{

    // Given N and K
    int N = 5, K = 2;

    // Function Call
    waysToArrangeKLengthStrings(N, K);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count K-length
// strings from first N alphabets
function waysToArrangeKLengthStrings(N, K)
{

    // To keep track of column sum in dp
    let column_sum = [];
    let i, j;

    for(i = 1; i < N + 1; i++)
    {
        column_sum[i] = 0;
    }

    // Auxiliary 2d dp array
    let dp = new Array(K + 1);
    // Loop to create 2D array using 1D array
    for (i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    for(i = 1; i < K + 1; i++)
    {
        for(j = 1; j < N + 1; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Initialize dp[0][i] = 1 and
    // update the column_sum
    for(i = 0; i <= N; i++)
    {
        dp[0][i] = 1;
        column_sum[i] = 1;
    }

    // Iterate for K times
    for(i = 1; i <= K; i++)
    {

        // Iterate for N times
        for(j = 1; j <= N; j++)
        {

            // dp[i][j]: Stores the number
            // of ways to form i-length
            // strings consisting of j letters
            dp[i][j] += column_sum[j - 1];

            // Update the column_sum
            column_sum[j] += dp[i][j];
        }
    }

    // Print number of ways to arrange
    // K-length strings with N alphabets
    document.write(dp[K][N]);
}

    // Driver Code

    // Given N and K
    let N = 5, K = 2;

    // Function Call
    waysToArrangeKLengthStrings(N, K);

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N*K)