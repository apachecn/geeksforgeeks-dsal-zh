# 计算矩阵中达到给定分数的方法数量

> 原文:[https://www . geesforgeks . org/count-到达给定矩阵分数的途径数/](https://www.geeksforgeeks.org/count-number-of-ways-to-reach-a-given-score-in-a-matrix/)

给定一个由非负整数组成的 **N x N** 矩阵 **mat[][]** ，任务是找到达到给定分数的途径数 **M** 从单元格 **(0，0)** 开始，仅向下(从(I，j)到(i + 1，j))或向右(从(I，j)到(I，j + 1))到达单元格**(N–1，N–1)**。每当到达单元格 **(i，j)** 时，总分由**current core+mat[I][j]**更新。
**举例:**

> **输入:** mat[][] = {{1，1，1}，
> {1，1，1}，
> {1，1，1}}，M = 4
> **输出:** 0
> 所有路径均为 5 分。
> **输入:** mat[][] = {{1，1，1}，
> {1，1，1}，
> {1，1，1}}，M = 5
> **输出:** 6

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。首先，我们需要决定民主党的状态。对于每个单元格 **(i，j)** 和一个数字 **0 ≤ X ≤ M** ，我们将存储从单元格 **(0，0)** 到达该单元格的途径数，总分为 **X** 。因此，我们的解决方案将使用三维动态规划，两个用于单元格的坐标，一个用于所需的分值。
所需的递归关系为，

> DP[I][j][m]= DP[I-1][j][m-mat[I][j]]+DP[I][j-1][m-mat[I][j]]

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;
#define n 3
#define MAX 30

// To store the states of dp
int dp[n][n][MAX];

// To check whether a particular state
// of dp has been solved
bool v[n][n][MAX];

// Function to find the ways
// using memoization
int findCount(int mat[][n], int i, int j, int m)
{
    // Base cases
    if (i == 0 && j == 0) {
        if (m == mat[0][0])
            return 1;
        else
            return 0;
    }

    // If required score becomes negative
    if (m < 0)
        return 0;

    if (i < 0 || j < 0)
        return 0;

    // If current state has been reached before
    if (v[i][j][m])
        return dp[i][j][m];

    // Set current state to visited
    v[i][j][m] = true;

    dp[i][j][m] = findCount(mat, i - 1, j, m - mat[i][j])
                  + findCount(mat, i, j - 1, m - mat[i][j]);
    return dp[i][j][m];
}

// Driver code
int main()
{
    int mat[n][n] = { { 1, 1, 1 },
                      { 1, 1, 1 },
                      { 1, 1, 1 } };
    int m = 5;
    cout << findCount(mat, n - 1, n - 1, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int n = 3;
static int MAX =30;

// To store the states of dp
static int dp[][][] = new int[n][n][MAX];

// To check whether a particular state
// of dp has been solved
static boolean v[][][] = new boolean[n][n][MAX];

// Function to find the ways
// using memoization
static int findCount(int mat[][], int i, int j, int m)
{
    // Base cases
    if (i == 0 && j == 0)
    {
        if (m == mat[0][0])
            return 1;
        else
            return 0;
    }

    // If required score becomes negative
    if (m < 0)
        return 0;

    if (i < 0 || j < 0)
        return 0;

    // If current state has been reached before
    if (v[i][j][m])
        return dp[i][j][m];

    // Set current state to visited
    v[i][j][m] = true;

    dp[i][j][m] = findCount(mat, i - 1, j, m - mat[i][j])
                + findCount(mat, i, j - 1, m - mat[i][j]);
    return dp[i][j][m];
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 1, 1, 1 },
                    { 1, 1, 1 },
                    { 1, 1, 1 } };
    int m = 5;
    System.out.println(findCount(mat, n - 1, n - 1, m));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
n = 3
MAX = 60

# To store the states of dp
dp = [[[0 for i in range(30)]  
          for i in range(30)]
          for i in range(MAX + 1)]

# To check whether a particular state
# of dp has been solved
v = [[[0 for i in range(30)]
         for i in range(30)]
         for i in range(MAX + 1)]

# Function to find the ways
# using memoization
def findCount(mat, i, j, m):

    # Base cases
    if (i == 0 and j == 0):
        if (m == mat[0][0]):
            return 1
        else:
            return 0

    # If required score becomes negative
    if (m < 0):
        return 0

    if (i < 0 or j < 0):
        return 0

    # If current state has been reached before
    if (v[i][j][m] > 0):
        return dp[i][j][m]

    # Set current state to visited
    v[i][j][m] = True

    dp[i][j][m] = (findCount(mat, i - 1, j,
                             m - mat[i][j]) +
                   findCount(mat, i, j - 1,
                             m - mat[i][j]))

    return dp[i][j][m]

# Driver code
mat = [ [ 1, 1, 1 ],
        [ 1, 1, 1 ],
        [ 1, 1, 1 ] ]
m = 5
print(findCount(mat, n - 1, n - 1, m))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int n = 3;
static int MAX = 30;

// To store the states of dp
static int [,,]dp = new int[n, n, MAX];

// To check whether a particular state
// of dp has been solved
static bool [,,]v = new bool[n, n, MAX];

// Function to find the ways
// using memoization
static int findCount(int [,]mat, int i,
                          int j, int m)
{
    // Base cases
    if (i == 0 && j == 0)
    {
        if (m == mat[0, 0])
            return 1;
        else
            return 0;
    }

    // If required score becomes negative
    if (m < 0)
        return 0;

    if (i < 0 || j < 0)
        return 0;

    // If current state has been reached before
    if (v[i, j, m])
        return dp[i, j, m];

    // Set current state to visited
    v[i, j, m] = true;

    dp[i, j, m] = findCount(mat, i - 1, j, m - mat[i, j]) +
                  findCount(mat, i, j - 1, m - mat[i, j]);
    return dp[i, j, m];
}

// Driver code
public static void Main()
{
    int [,]mat = {{ 1, 1, 1 },
                  { 1, 1, 1 },
                  { 1, 1, 1 }};
    int m = 5;
    Console.WriteLine(findCount(mat, n - 1, n - 1, m));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$n = 3;
$MAX = 30;

// To store the states of dp
$dp = array($n, $n, $MAX);

// To check whether a particular state
// of dp has been solved
$v = array($n, $n, $MAX);

// Function to find the ways
// using memoization
function findCount($mat, $i, $j, $m)
{
    // Base cases
    if ($i == 0 && $j == 0)
    {
        if ($m == $mat[0][0])
            return 1;
        else
            return 0;
    }

    // If required score becomes negative
    if ($m < 0)
        return 0;

    if ($i < 0 || $j < 0)
        return 0;

    // If current state has been reached before
    if ($v[$i][$j][$m])
        return $dp[$i][$j][$m];

    // Set current state to visited
    $v[$i][$j][$m] = true;

    $dp[$i][$j][$m] = findCount($mat, $i - 1, $j,      
                                $m - $mat[$i][$j]) +
                      findCount($mat, $i, $j - 1,
                                $m - $mat[$i][$j]);
    return $dp[$i][$j][$m];
}

// Driver code
$mat = array(array(1, 1, 1 ),
             array(1, 1, 1 ),
             array(1, 1, 1 ));
$m = 5;
echo(findCount($mat, $n - 1, $n - 1, $m));

// This code contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var n = 3;
var MAX = 30;

// To store the states of dp
var dp = Array(n);
for(var i =0; i<n; i++)
{
    dp[i] = Array(n);
    for(var j=0; j<n; j++)
    {
        dp[i][j]=Array(MAX);
    }
}

// To check whether a particular state
// of dp has been solved
var v = Array(n);
for(var i =0; i<n; i++)
{
    v[i] = Array(n);
    for(var j=0; j<n; j++)
    {
        v[i][j]=Array(MAX);
    }
}

// Function to find the ways
// using memoization
function findCount(mat, i, j, m)
{
    // Base cases
    if (i == 0 && j == 0) {
        if (m == mat[0][0])
            return 1;
        else
            return 0;
    }

    // If required score becomes negative
    if (m < 0)
        return 0;

    if (i < 0 || j < 0)
        return 0;

    // If current state has been reached before
    if (v[i][j][m])
        return dp[i][j][m];

    // Set current state to visited
    v[i][j][m] = true;

    dp[i][j][m] = findCount(mat, i - 1, j,
                            m - mat[i][j])
                  + findCount(mat, i, j - 1,
                              m - mat[i][j]);
    return dp[i][j][m];
}

// Driver code
var mat = [ [ 1, 1, 1 ],
                  [ 1, 1, 1 ],
                  [ 1, 1, 1 ] ];
var m = 5;
document.write( findCount(mat, n - 1, n - 1, m));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N * N * M)