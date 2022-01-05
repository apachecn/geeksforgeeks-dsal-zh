# 检查是否可以从每行取一个元素得到给定的和

> 原文:[https://www . geeksforgeeks . org/check-如果有可能，从每行中取一个元素来获得给定的总和/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-get-given-sum-by-taking-one-element-from-each-row/)

给定一个由 **N** 行和 **M** 列以及一个整数 **K** 组成的二维数组。任务是找出是否有可能从给定数组的每一行中恰好取一个元素，并使总和等于 k。
**示例:**

```
Input: N = 2, M = 10, K = 5
arr = {{4, 0, 15, 3, 2, 20, 10, 1, 5, 4}, 
      {4, 0, 10, 3, 2, 25, 4, 1, 5, 4}}
Output: YES
Explanation:
Take 2 from first row and 3 from second row.
2 + 3 = 5
So, we can make 5 by taking exactly one element
from each row.

Input:N = 3, M = 5, K = 5
arr = {{4, 3, 4, 5, 4}, 
       {2, 2, 3, 4, 3}, 
       {2, 1, 3, 3, 2}}
Output: NO
```

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

1.  我们可以做一个 N 行 K 列的二维二进制数组 DP[][]。其中 DP[i][j] = 1 表示我们可以通过从每一行取一个元素直到 i.
    得到一个等于 j 的和
2.  因此，我们将从 i = [0，N]，k = [0，K]迭代数组，并检查当前和(K)是否存在。

3.  如果当前和存在，那么我们将迭代该列，并为每个小于或等于 k 的可能和更新数组

以下是上述方法的实施

## C++

```
// C++ implementation to find
// whether is it possible to
// make sum equal to K
#include <bits/stdc++.h>
using namespace std;

// Function that prints whether is it
// possible to make sum equal to K
void PossibleSum(int n, int m,
              vector<vector<int> > v,
              int k)
{
    int dp[n + 1][k + 1] = { 0 };

    // Base case
    dp[0][0] = 1;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j <= k; j++)
        {
            // Condition if we can make
            // sum equal to current column
            // by using above rows
            if (dp[i][j] == 1)
            {
                // Iterate through current
                // column and check whether
                // we can make sum less than
                // or equal to k
                for (int d = 0; d < m; d++)
                {
                    if ((j + v[i][d]) <= k)
                    {
                        dp[i + 1][j + v[i][d]] = 1;
                    }
                }
            }
        }
    }

    // Printing whether is it
    // possible or not
    if (dp[n][k] == 1)
        cout << "YES\n";
    else
        cout << "NO\n";
}

// Driver Code
int main()
{
    int N = 2, M = 10, K = 5;

    vector<vector<int> > arr = { { 4, 0, 15, 3, 2,
                                  20, 10, 1, 5, 4 },
                                 { 4, 0, 10, 3, 2,
                                  25, 4, 1, 5, 4 } };

    PossibleSum(N, M, arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// whether is it possible to
// make sum equal to K
import java.io.*;
import java.util.*;

class GFG {

// Function that prints whether is it
// possible to make sum equal to K
static void PossibleSum(int n, int m,
                        int[][] v, int k)
{
    int[][] dp = new int[n + 1][k + 1];

    // Base case
    dp[0][0] = 1;

    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j <= k; j++)
       {

          // Condition if we can make
          // sum equal to current column
          // by using above rows
          if (dp[i][j] == 1)
          {

              // Iterate through current
              // column and check whether
              // we can make sum less than
              // or equal to k
              for(int d = 0; d < m; d++)
              {
                 if ((j + v[i][d]) <= k)
                 {
                     dp[i + 1][j + v[i][d]] = 1;
                 }
              }
          }
       }
    }

    // Printing whether is it
    // possible or not
    if (dp[n][k] == 1)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver code
public static void main(String[] args)
{
    int N = 2, M = 10, K = 5;
    int[][] arr = new int[][]{ { 4, 0, 15, 3, 2,
                                20, 10, 1, 5, 4 },
                               { 4, 0, 10, 3, 2,
                                25, 4, 1, 5, 4 } };
    PossibleSum(N, M, arr, K);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation to find
# whether is it possible to
# make sum equal to K

# Function that prints whether is it
# possible to make sum equal to K
def PossibleSum(n, m, v, k):

    dp = [[0] * (k + 1) for i in range(n + 1)]

    # Base case
    dp[0][0] = 1

    for i in range(n):
        for j in range(k + 1):

            # Condition if we can make
            # sum equal to current column
            # by using above rows
            if dp[i][j] == 1:

                # Iterate through current
                # column and check whether
                # we can make sum less than
                # or equal to k
                for d in range(m):
                    if (j + v[i][d]) <= k:
                        dp[i + 1][j + v[i][d]] = 1

    # Printing whether is it
    # possible or not
    if dp[n][k] == 1:
        print("YES")
    else:
        print("NO")

# Driver Code
N = 2
M = 10
K = 5
arr = [ [ 4, 0, 15, 3, 2,
         20, 10, 1, 5, 4 ],
        [ 4, 0, 10, 3, 2,
          25, 4, 1, 5, 4 ] ]

PossibleSum(N, M, arr, K)

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to find
// whether is it possible to
// make sum equal to K
using System;
class GFG{

// Function that prints whether is it
// possible to make sum equal to K
static void PossibleSum(int n, int m,
                        int[,] v, int k)
{
    int[,] dp = new int[n + 1, k + 1];

    // Base case
    dp[0, 0] = 1;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j <= k; j++)
        {

            // Condition if we can make
            // sum equal to current column
            // by using above rows
            if (dp[i, j] == 1)
            {

                // Iterate through current
                // column and check whether
                // we can make sum less than
                // or equal to k
                for(int d = 0; d < m; d++)
                {
                    if ((j + v[i, d]) <= k)
                    {
                        dp[i + 1, j + v[i, d]] = 1;
                    }
                }
            }
        }
    }

    // Printing whether is it
    // possible or not
    if (dp[n, k] == 1)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Driver code
public static void Main(String[] args)
{
    int N = 2, M = 10, K = 5;
    int[,] arr = new int[,]{ { 4, 0, 15, 3, 2,
                              20, 10, 1, 5, 4 },
                             { 4, 0, 10, 3, 2,
                              25, 4, 1, 5, 4 } };
    PossibleSum(N, M, arr, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find
// whether is it possible to
// make sum equal to K

// Function that prints whether is it
// possible to make sum equal to K
function PossibleSum(n, m, v, k)
{
    var dp = Array.from(Array(n+1), ()=>Array(k+1).fill(0));

    // Base case
    dp[0][0] = 1;

    for (var i = 0; i < n; i++)
    {
        for (var j = 0; j <= k; j++)
        {
            // Condition if we can make
            // sum equal to current column
            // by using above rows
            if (dp[i][j] == 1)
            {
                // Iterate through current
                // column and check whether
                // we can make sum less than
                // or equal to k
                for (var d = 0; d < m; d++)
                {
                    if ((j + v[i][d]) <= k)
                    {
                        dp[i + 1][j + v[i][d]] = 1;
                    }
                }
            }
        }
    }

    // Printing whether is it
    // possible or not
    if (dp[n][k] == 1)
        document.write( "YES");
    else
        document.write( "NO");
}

// Driver Code
var N = 2, M = 10, K = 5;
var arr = [ [ 4, 0, 15, 3, 2,
                              20, 10, 1, 5, 4 ],
                             [ 4, 0, 10, 3, 2,
                              25, 4, 1, 5, 4 ] ];
PossibleSum(N, M, arr, K);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N * M * K)