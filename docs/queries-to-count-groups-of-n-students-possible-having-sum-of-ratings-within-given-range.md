# 对给定范围内可能具有评分总和的 N 组学生进行计数的查询

> 原文:[https://www . geeksforgeeks . org/查询-计数-n 组学生-可能有-给定范围内的评分总和/](https://www.geeksforgeeks.org/queries-to-count-groups-of-n-students-possible-having-sum-of-ratings-within-given-range/)

给定整数 **N** 和 **K** 分别表示批次数量和每批学生数量，以及大小为 **N * K** 的 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **等级[][]** ，其中每行具有每一个 **K** 学生的等级和 **Q** 类型的 **{a，b}** 查询。每个查询的任务是通过从每个批次中选择一名学生来计算可能的 **N** 学生的组数，使得每个组中的评分总和在**【a，b】**范围内(包括这两个范围)。

**示例:**

> **输入:** N = 2，K = 3，评分[][]= { {1，2，3}，{4，5，6} }，Q = 2，查询[][]={ {6，6}，{1， 6} }
> **输出:** 2 3
> **说明:**
> 大小 N(=2)所有可能的组为:
> 1+4 = 5
> 1+5 = 6
> 1+6 = 7
> 2+4 = 6
> 2+5 = 7
> 2+6 = 8
> 3+4 = 7
> 3+5 = 8
> 3+6 = 9
> T19
> **查询 2:** 范围(1，6)内和为(1 + 4)、(1 + 5)、(2 + 4)的组为 3。
> 
> **输入:** N = 3，K = 3，评级[][]={ {1，2，3}，{4，5，6}，{7，8，9} }，Q = 2，查询[][]={ {10，13}，{1，7} }
> **输出:** 4 0
> **解释** :
> 在所有可能的大小组中 N =(3):
> **查询 1:** 其和在范围内的组
> **查询 2:** 在(1，7)范围内总和为 0 的组。

**天真方法:**最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)生成所有可能的大小组 **N** 。在**递归**的每一步，计算位于查询的**范围**内的和，并找到位于给定范围内的**组数**。

***时间复杂度:**O(N<sup>K</sup>)*
***辅助空间:** O(1)*

**高效方法**:以上方法可以使用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 进行优化。其思想是如果知道**和 S** 在 **i <sup>第</sup>** 行出现的次数，那么 [**前缀和手法**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 就可以在恒定时间内回答所有的查询。这样[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)只计算一次，将指数时间减少为多项式时间。以下是步骤:

*   初始化辅助数组 **dp[][]** ，其中 **dp[i][sum]** 是总和在 **i <sup>第</sup>行**中出现的次数。
*   对于每个批次， **i** 遍历所有可能的总和 **S** ，对于每个 **j** 学生，如果总和 **S** 大于当前等级**等级【I】【j】**，则更新当前 dp 状态**DP【I】【S】**为:

> DP[I][S]= DP[I][S]+DP[I–1][sum–评级[i][j]]

*   经过上述步骤后，**DP[N–1][sum]，**即总和出现在**(N–1)<sup>第</sup>行**的次数。
*   为了有效地回答每个查询，找到最后一行的前缀和，即所有和值 **S** 的 DP【N–1】【S】。
*   现在，在给定范围[a，b]内形成组的方法数量为**DP[N–1][b]–DP[N–1][a–1]**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Given n batches and k students
#define n 2
#define k 3

// Function to count number of
// ways to get given sum groups
void numWays(int ratings[n][k], int queries[][2])
{

    // Initialise dp array
    int dp[n][10000 + 2];

    // Mark all 1st row values as 1
    // since the mat[0][i] is all
    // possible sums in first row
    for (int i = 0; i < k; i++)
        dp[0][ratings[0][i]] += 1;

    // Fix the ith row
    for (int i = 1; i < n; i++) {

        // Fix the sum
        for (int sum = 0; sum <= 10000; sum++)
        {
            // Iterate through all
            // values of ith row
            for (int j = 0; j < k; j++)
            {
                // If sum can be obtained
                if (sum >= ratings[i][j])
                    dp[i][sum]
                        += dp[i - 1][sum - ratings[i][j]];
            }
        }
    }

    // Find the prefix sum of last row
    for (int sum = 1; sum <= 10000; sum++)
    {
        dp[n - 1][sum] += dp[n - 1][sum - 1];
    }

    // Traverse each query

    for (int q = 0; q < 2; q++)
    {
        int a = queries[q][0];
        int b = queries[q][1];

        // No of ways to form groups
        cout << dp[n - 1][b] - dp[n - 1][a - 1] << " ";
    }
}

// Driver Code
int main()
{

    // Given ratings
    int ratings[n][k] = { { 1, 2, 3 }, { 4, 5, 6 } };

    // Given Queries
    int queries[][2] = { { 6, 6 }, { 1, 6 } };

    // Function Call
    numWays(ratings, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    // Function to count number of
    // ways to get given sum groups
    public static void
    numWays(int[][] ratings,
            int queries[][],
            int n, int k)
    {

        // Initialise dp array
        int dp[][] = new int[n][10000 + 2];

        // Mark all 1st row values as 1
        // since the mat[0][i] is all
        // possible sums in first row
        for (int i = 0; i < k; i++)
            dp[0][ratings[0][i]] += 1;

        // Fix the ith row
        for (int i = 1; i < n; i++)
        {

            // Fix the sum
            for (int sum = 0; sum <= 10000; sum++)
            {

                // Iterate through all
                // values of ith row
                for (int j = 0; j < k; j++)
                {

                    // If sum can be obtained
                    if (sum >= ratings[i][j])
                        dp[i][sum]
                            += dp[i - 1]
                               [sum - ratings[i][j]];
                }
            }
        }

        // Find the prefix sum of last row
        for (int sum = 1; sum <= 10000; sum++) {
            dp[n - 1][sum] += dp[n - 1][sum - 1];
        }

        // Traverse each query
        for (int q = 0; q < queries.length; q++) {

            int a = queries[q][0];
            int b = queries[q][1];

            // No of ways to form groups
            System.out.print(dp[n - 1][b] - dp[n - 1][a - 1]
                             + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given N batches and K students
        int N = 2, K = 3;

        // Given ratings
        int ratings[][] = { { 1, 2, 3 }, { 4, 5, 6 } };

        // Given Queries
        int queries[][] = { { 6, 6 }, { 1, 6 } };

        // Function Call
        numWays(ratings, queries, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to count number of
# ways to get given sum groups
def numWays(ratings, queries,
            n, k):

    # Initialise dp array
    dp = [[0 for i in range(10002)]
             for j in range(n)];

    # Mark all 1st row values as 1
    # since the mat[0][i] is all
    # possible sums in first row
    for i in range(k):
        dp[0][ratings[0][i]] += 1;

    # Fix the ith row
    for i in range(1, n):

        # Fix the sum
        for sum in range(10001):

            # Iterate through all
            # values of ith row
            for j in range(k):

                # If sum can be obtained
                if (sum >= ratings[i][j]):
                    dp[i][sum] += dp[i - 1][sum -
                                            ratings[i][j]];

    # Find the prefix sum of
    # last row
    for sum in range(1, 10001):
        dp[n - 1][sum] += dp[n - 1][sum - 1];

    # Traverse each query
    for q in range(len(queries)):
        a = queries[q][0];
        b = queries[q][1];

        # No of ways to form groups
        print(dp[n - 1][b] -
              dp[n - 1][a - 1],
              end = " ");

# Driver Code
if __name__ == '__main__':

    # Given N batches and
    # K students
    N = 2;
    K = 3;

    # Given ratings
    ratings = [[1, 2, 3],
               [4, 5, 6]];

    queries = [[6, 6],
               [1, 6]];

    # Function Call
    numWays(ratings, queries, N, K);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of
// ways to get given sum groups
public static void numWays(int[,] ratings,
                           int [,]queries,
                           int n, int k)
{

    // Initialise dp array
    int [,]dp = new int[n, 10000 + 2];

    // Mark all 1st row values as 1
    // since the mat[0,i] is all
    // possible sums in first row
    for(int i = 0; i < k; i++)
        dp[0, ratings[0, i]] += 1;

    // Fix the ith row
    for(int i = 1; i < n; i++)
    {

        // Fix the sum
        for(int sum = 0; sum <= 10000; sum++)
        {

            // Iterate through all
            // values of ith row
            for(int j = 0; j < k; j++)
            {

                // If sum can be obtained
                if (sum >= ratings[i, j])
                    dp[i, sum] += dp[i - 1,
                                   sum - ratings[i, j]];
            }
        }
    }

    // Find the prefix sum of last row
    for(int sum = 1; sum <= 10000; sum++)
    {
        dp[n - 1, sum] += dp[n - 1, sum - 1];
    }

    // Traverse each query
    for(int q = 0; q < queries.GetLength(0); q++)
    {
        int a = queries[q, 0];
        int b = queries[q, 1];

        // No of ways to form groups
        Console.Write(dp[n - 1, b] -
                      dp[n - 1, a - 1] + " ");
    }
}

// Driver Code
public static void Main(String []args)
{

    // Given N batches and K students
    int N = 2, K = 3;

    // Given ratings
    int [,]ratings = { { 1, 2, 3 }, { 4, 5, 6 } };

    // Given Queries
    int [,]queries = { { 6, 6 }, { 1, 6 } };

    // Function Call
    numWays(ratings, queries, N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Given n batches and k students
var n = 2;
var k = 3;

// Function to count number of
// ways to get given sum groups
function numWays(ratings, queries)
{

    // Initialise dp array
    var dp = Array.from(
        Array(n), ()=>Array(10002).fill(0));

    // Mark all 1st row values as 1
    // since the mat[0][i] is all
    // possible sums in first row
    for(var i = 0; i < k; i++)
        dp[0][ratings[0][i]] += 1;

    // Fix the ith row
    for(var i = 1; i < n; i++)
    {

        // Fix the sum
        for(var sum = 0; sum <= 10000; sum++)
        {

            // Iterate through all
            // values of ith row
            for(var j = 0; j < k; j++)
            {

                // If sum can be obtained
                if (sum >= ratings[i][j])
                    dp[i][sum]+= dp[i - 1][sum - ratings[i][j]];
            }
        }
    }

    // Find the prefix sum of last row
    for(var sum = 1; sum <= 10000; sum++)
    {
        dp[n - 1][sum] += dp[n - 1][sum - 1];
    }

    // Traverse each query
    for(var q = 0; q < 2; q++)
    {
        var a = queries[q][0];
        var b = queries[q][1];

        // No of ways to form groups
        document.write(dp[n - 1][b] -
                       dp[n - 1][a - 1] + " ");
    }
}

// Driver Code

// Given ratings
var ratings = [ [ 1, 2, 3 ], [ 4, 5, 6 ] ];

// Given Queries
var queries = [ [ 6, 6 ], [ 1, 6 ] ];

// Function Call
numWays(ratings, queries);

// This code is contributed by famously

</script>
```

**Output**

```
2 3 
```

**时间复杂度:** O(N*maxSum*K)，其中 maxSum 为最大和。
**辅助空间:** O(N*maxSum)，其中 maxSum 为最大和。