# 到达非零“与”值矩阵末端的途径数

> 原文:[https://www . geeksforgeeks . org/到达非零值矩阵末端的途径数/](https://www.geeksforgeeks.org/number-of-ways-to-reach-the-end-of-matrix-with-non-zero-and-value/)

给定一个由非负整数组成的 **N * N** 矩阵 **arr[][]** ，任务是找到从 **arr[0][0]** 开始通过每次移动向下或向右到达**arr[N–1][N–1]**的方法数。每当到达单元格 **arr[i][j]** 时，“与”值更新为**current val&arr[I][j]**。

**示例:**

> **输入:** arr[][] = {
> {1，1，1}，
> {1，1，1}，
> {1，1，1}}
> **输出:** 6
> 所有路径将给出非零和值。
> 因此，路的数量等于 6。
> **输入:** arr[][] = {
> {1，1，2}，
> {1，2，1}，
> {2，1，1}}
> **输出:** 0

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。首先，我们需要决定民主党的状态。对于每个单元格 **arr[i][j]** 和一个数字 **X** ，我们将存储从 **arr[i][j]** 到达**arr[N–1][N–1]**的路径数，其中 **X** 是到目前为止路径的“与”值。因此，我们的解决方案将使用三维动态编程，两个用于单元格的坐标，一个用于 **X** 。
要求的递推关系是:

> DP[I][j][x]= DP[I][j+1][x & arr[I][j]]+DP[I+1][j][x & arr[I][j]]

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define n 3
#define maxV 20
using namespace std;

// 3d array to store
// states of dp
int dp[n][n][maxV];

// Array to determine whether
// a state has been solved before
int v[n][n][maxV];

// Function to return the count of required paths
int countWays(int i, int j, int x, int arr[][n])
{

    // Base cases
    if (i == n || j == n)
        return 0;

    x = (x & arr[i][j]);
    if (x == 0)
        return 0;

    if (i == n - 1 && j == n - 1)
        return 1;

    // If a state has been solved before
    // it won't be evaluated again
    if (v[i][j][x])
        return dp[i][j][x];

    v[i][j][x] = 1;

    // Recurrence relation
    dp[i][j][x] = countWays(i + 1, j, x, arr)
                  + countWays(i, j + 1, x, arr);

    return dp[i][j][x];
}

// Driver code
int main()
{
    int arr[n][n] = { { 1, 2, 1 },
                      { 1, 1, 0 },
                      { 2, 1, 1 } };

    cout << countWays(0, 0, arr[0][0], arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int n = 3;
    static int maxV = 20;

    // 3d array to store
    // states of dp
    static int[][][] dp = new int[n][n][maxV];

    // Array to determine whether
    // a state has been solved before
    static int[][][] v = new int[n][n][maxV];

    // Function to return the count of required paths
    static int countWays(int i, int j,
                         int x, int arr[][])
    {

        // Base cases
        if (i == n || j == n) {
            return 0;
        }

        x = (x & arr[i][j]);
        if (x == 0) {
            return 0;
        }

        if (i == n - 1 && j == n - 1) {
            return 1;
        }

        // If a state has been solved before
        // it won't be evaluated again
        if (v[i][j][x] == 1) {
            return dp[i][j][x];
        }

        v[i][j][x] = 1;

        // Recurrence relation
        dp[i][j][x] = countWays(i + 1, j, x, arr)
                      + countWays(i, j + 1, x, arr);

        return dp[i][j][x];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[][] = { { 1, 2, 1 },
                        { 1, 1, 0 },
                        { 2, 1, 1 } };

        System.out.println(countWays(0, 0, arr[0][0], arr));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
n = 3
maxV = 20

# 3d array to store states of dp
dp = [[[0 for i in range(maxV)]
          for i in range(n)]
          for i in range(n)]

# Array to determine whether
# a state has been solved before
v = [[[0 for i in range(maxV)]
         for i in range(n)]
         for i in range(n)]

# Function to return
# the count of required paths
def countWays(i, j, x, arr):

    # Base cases
    if (i == n or j == n):
        return 0

    x = (x & arr[i][j])
    if (x == 0):
        return 0

    if (i == n - 1 and j == n - 1):
        return 1

    # If a state has been solved before
    # it won't be evaluated again
    if (v[i][j][x]):
        return dp[i][j][x]

    v[i][j][x] = 1

    # Recurrence relation
    dp[i][j][x] = countWays(i + 1, j, x, arr) + \
                  countWays(i, j + 1, x, arr);

    return dp[i][j][x]

# Driver code
arr = [[1, 2, 1 ],
       [1, 1, 0 ],
       [2, 1, 1 ]]

print(countWays(0, 0, arr[0][0], arr))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int n = 3;
    static int maxV = 20;

    // 3d array to store
    // states of dp
    static int[,,] dp = new int[n, n, maxV];

    // Array to determine whether
    // a state has been solved before
    static int[,,] v = new int[n, n, maxV];

    // Function to return the count of required paths
    static int countWays(int i, int j,
                        int x, int [,]arr)
    {

        // Base cases
        if (i == n || j == n)
        {
            return 0;
        }

        x = (x & arr[i, j]);
        if (x == 0)
        {
            return 0;
        }

        if (i == n - 1 && j == n - 1)
        {
            return 1;
        }

        // If a state has been solved before
        // it won't be evaluated again
        if (v[i, j, x] == 1)
        {
            return dp[i, j, x];
        }

        v[i, j, x] = 1;

        // Recurrence relation
        dp[i, j, x] = countWays(i + 1, j, x, arr)
                    + countWays(i, j + 1, x, arr);

        return dp[i, j, x];
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = { { 1, 2, 1 },
                        { 1, 1, 0 },
                        { 2, 1, 1 } };

    Console.WriteLine(countWays(0, 0, arr[0,0], arr));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var n = 3;
var maxV = 20;

// 3d array to store
// states of dp
var dp = new Array(n);

for(var i = 0; i<n; i++)
{
    dp[i] = new Array(n);
    for(var j =0; j<n;j++)
    {
        dp[i][j] = new Array(maxV);
    }
}

var v = new Array(n);

// Array to determine whether
// a state has been solved before
for(var i = 0; i<n; i++)
{
    v[i] = new Array(n);
    for(var j =0; j<n;j++)
    {
        v[i][j] = new Array(maxV);
    }
}

// Function to return the count of required paths
function countWays(i, j, x, arr)
{

    // Base cases
    if (i == n || j == n)
        return 0;

    x = (x & arr[i][j]);
    if (x == 0)
        return 0;

    if (i == n - 1 && j == n - 1)
        return 1;

    // If a state has been solved before
    // it won't be evaluated again
    if (v[i][j][x])
        return dp[i][j][x];

    v[i][j][x] = 1;

    // Recurrence relation
    dp[i][j][x] = countWays(i + 1, j, x, arr)
                  + countWays(i, j + 1, x, arr);

    return dp[i][j][x];
}

// Driver code
var arr = [ [ 1, 2, 1 ],
                  [ 1, 1, 0 ],
                  [ 2, 1, 1 ] ];
document.write( countWays(0, 0, arr[0][0], arr));

</script>
```

**Output:** 

```
1
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:O(n <sup>4</sup> * maxV)