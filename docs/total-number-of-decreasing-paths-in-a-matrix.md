# 矩阵中递减路径的总数

> 原文:[https://www . geesforgeks . org/矩阵中路径总数减少/](https://www.geeksforgeeks.org/total-number-of-decreasing-paths-in-a-matrix/)

给定一个整数矩阵**N×N**。任务是找出矩阵中递减路径的个数。你可以从任何一个单元开始，从(I，j)单元开始，你可以移动到 **(i + 1，j)，(I–1，j)，(I，j + 1)和(I，j–1)**单元。
**例:**

```
Input : m[][] = { { 1, 2 }, 
                  { 1, 3 } }
Output : 8
Explanation : Decreasing paths are { 1 }, { 1 }, { 2 }, { 3 },
              { 2, 1 }, { 3, 1 }, { 3, 2 }, { 3, 2, 1 }

Input : m[][] = { { 1, 2, 3 },
                  { 1, 3, 4 },
                  { 1, 5, 6 } }
Output : 41
```

解决这个问题的思路是使用动态规划。声明一个 **dp[][]** 数组，其中 **dp[i][j]存储从单元(I，j)** 可以形成的递减路径的数量。因此，我们将定义一个递归函数来计算带有参数的递减路径数，比如 I，j，当前单元格的行号和列号。从单元格(I，j)中进行所有可能的移动，并记录路径总数。首先，我们将在函数中检查输入位置(I，j)的递减路径数是否已经计算。如果是，返回值 **dp[i][j]** 否则找到四个方向允许的递减顺序数并返回值。同时，我们还将存储中间单元格的递减数。由于 DP[i][j]存储每个单元的递减路径数，因此 DP[][]的所有单元的总和将对应于完整矩阵中递减路径的计数。
以下是上述方法的实现:

## C++

```
// CPP program to count number
// of decreasing path in a matrix
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Function that returns the number of
// decreasing paths from a cell(i, j)
int CountDecreasingPathsCell(int mat[MAX][MAX], int dp[MAX][MAX],
                                              int n, int x, int y)
{
    // checking if already calculated
    if (dp[x][y] != -1)
        return dp[x][y];

    // all possible paths
    int delta[4][2] = { { 0, 1 }, { 1, 0 }, { -1, 0 }, { 0, -1 } };
    int newx, newy;

    // counts the total number of paths
    int ans = 1;

    // In all four allowed direction.
    for (int i = 0; i < 4; i++) {

        // new co-ordinates
        newx = x + delta[i][0];
        newy = y + delta[i][1];

        // Checking if not going out of matrix and next
        // cell value is less than current cell value.
        if (newx >= 0 && newx < n && newy >= 0
            && newy < n && mat[newx][newy] < mat[x][y]) {
            ans += CountDecreasingPathsCell(mat, dp, n, newx, newy);
        }
    }
    // function that returns the answer
    return dp[x][y] = ans;
}

// Function that counts the total
// decreasing path in the matrix
int countDecreasingPathsMatrix(int n,
                               int mat[MAX][MAX])
{
    int dp[MAX][MAX];

    // Initialising dp[][] to -1.
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dp[i][j] = -1;

    int sum = 0;

    // Calculating number of decreasing path from each cell.
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += CountDecreasingPathsCell(mat, dp, n, i, j);

    return sum;
}

// Driver Code
int main()
{
    int n = 2;

    int mat[MAX][MAX] = { { 1, 2 }, { 1, 3 } };
    // function call that returns the
    // count of decreasing paths in a matrix
    cout << countDecreasingPathsMatrix(n, mat)
         << endl;
    return 0;
}
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-1">爪哇</gfg-tab>T2】

```
 // Java program to count number
// of decreasing path in a matrix
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
public static Scanner scn = 
      new Scanner(System.in);

// Function that returns the number of
// decreasing paths from a cell(i, j)
public static int CountDecreasingPathsCell(int mat[][], int dp[][], 
                                           int n, int x, int y)
    {
        // checking if already calculated
        if (dp[x][y] != -1)
            return dp[x][y];

        // all possible paths
        int delta[][] = { { 0, 1 }, { 1, 0 }, 
                          { -1, 0}, { 0, -1}};
        int newx, newy;

        // counts the total
        // number of paths
        int ans = 1;

        // In all four allowed direction.
        for (int i = 0; i < 4; i++) 
        {

            // new co-ordinates
            newx = x + delta[i][0];
            newy = y + delta[i][1];

            // Checking if not going out 
            // of matrix and next cell 
            // value is less than current 
            // cell value.
            if (newx >= 0 && newx < n && newy >= 0 && 
                newy < n && mat[newx][newy] < mat[x][y]) 
            {
                ans += CountDecreasingPathsCell(mat, dp, n, 
                                                newx, newy);
            }
        }

        // function that 
        // returns the answer
        return dp[x][y] = ans;
    }

// Function that counts the total
// decreasing path in the matrix
public static int countDecreasingPathsMatrix(int n, 
                                             int mat[][])
    {
        int dp[][] = new int[n][n];

        // Initialising dp[][] to -1.
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                dp[i][j] = -1;

        int sum = 0;

        // Calculating number of 
        // decreasing path from each cell.
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                sum += CountDecreasingPathsCell(mat, dp, 
                                                n, i, j);

        return sum;
    }

// Driver Code
public static void main(String[] args) 
{
    int n = 2;

    int mat[][]= {{1, 2}, 
                  {1, 3}};

    // function call that returns the
    // count of decreasing paths in a matrix
    System.out.println(countDecreasingPathsMatrix(n, mat));

} 
}

// This code is contributed by khyati grover 
```

## 蟒蛇 3

```
# Python3 program to count number
# of decreasing path in a matrix
MAX = 100

# Function that returns the number of
# decreasing paths from a cell(i, j)
def CountDecreasingPathsCell(mat, dp, n, x, y):

    # checking if already calculated
    if (dp[x][y] != -1):
        return dp[x][y]

    # all possible paths
    delta = [[0, 1], [1, 0],
             [-1, 0], [0, -1]]
    newx, newy = 0, 0

    # counts the total number of paths
    ans = 1

    # In all four allowed direction.
    for i in range(4):

        # new co-ordinates
        newx = x + delta[i][0]
        newy = y + delta[i][1]

        # Checking if not going out of matrix and next
        # cell value is less than current cell value.
        if (newx >= 0 and newx < n and newy >= 0 and
            newy < n and mat[newx][newy] < mat[x][y]):
            ans += CountDecreasingPathsCell(mat, dp, n,
                                            newx, newy)

    # function that returns the answer
    dp[x][y] = ans
    return dp[x][y]

# Function that counts the total
# decreasing path in the matrix
def countDecreasingPathsMatrix(n,mat):
    dp = []

    # Initialising dp[][] to -1.
    for i in range(n):
        l = []
        for j in range(n):
            l.append(-1)
        dp.append(l)
    sum = 0

    # Calculating number of decreasing
    # path from each cell.
    for i in range(n):
        for j in range(n):
            sum += CountDecreasingPathsCell(mat, dp,
                                            n, i, j)
    return sum

# Driver Code
n = 2
mat = [[1, 2], [1, 3]]

# function call that returns the
# count of decreasing paths in a matrix
print(countDecreasingPathsMatrix(n, mat))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to count number
// of decreasing path in a matrix
using System;

class GFG
{

// Function that returns
// the number of decreasing
// paths from a cell(i, j)
public static int CountDecreasingPathsCell(int[,] mat, int[,] dp,
                                           int n, int x, int y)
{
    // checking if already
    // calculated
    if (dp[x, y] != -1)
        return dp[x, y];

    // all possible paths
    int[,] delta = {{0, 1}, {1, 0},
                    {-1, 0},{0, -1}};
    int newx, newy;

    // counts the total
    // number of paths
    int ans = 1;

    // In all four
    // allowed direction.
    for (int i = 0; i < 4; i++)
    {

        // new co-ordinates
        newx = x + delta[i,0];
        newy = y + delta[i,1];

        // Checking if not going out
        // of matrix and next cell
        // value is less than current
        // cell value.
        if (newx >= 0 && newx < n &&
            newy >= 0 && newy < n &&
            mat[newx,newy] < mat[x,y])
        {
            ans += CountDecreasingPathsCell(mat, dp, n,
                                            newx, newy);
        }
    }

    // function that
    // returns the answer
    return dp[x,y] = ans;
}

// Function that counts the total
// decreasing path in the matrix
public static int countDecreasingPathsMatrix(int n,
                                        int[,] mat)
{
    int[,] dp = new int[n, n];

    // Initialising dp[][] to -1.
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dp[i, j] = -1;

    int sum = 0;

    // Calculating number of
    // decreasing path from each cell.
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += CountDecreasingPathsCell(mat, dp,
                                            n, i, j);

    return sum;
}

// Driver code
static public void Main ()
{
    int n = 2;

    int[,] mat= {{1, 2},
                {1, 3}};

    // function call that returns the
    // count of decreasing paths in a matrix
    Console.WriteLine(countDecreasingPathsMatrix(n, mat));
}
}

// This code is contributed by vij.
```

## java 描述语言

```
<script>

// Javascript program to count number
// of decreasing path in a matrix
var MAX = 100

// Function that returns the number of
// decreasing paths from a cell(i, j)
function CountDecreasingPathsCell(mat, dp, n, x, y)
{
    // checking if already calculated
    if (dp[x][y] != -1)
        return dp[x][y];

    // all possible paths
    var delta = [ [ 0, 1 ], [ 1, 0 ], [ -1, 0 ],
    [ 0, -1 ] ];
    var newx, newy;

    // counts the total number of paths
    var ans = 1;

    // In all four allowed direction.
    for (var i = 0; i < 4; i++) {

        // new co-ordinates
        newx = x + delta[i][0];
        newy = y + delta[i][1];

        // Checking if not going out of matrix and next
        // cell value is less than current cell value.
        if (newx >= 0 && newx < n && newy >= 0
            && newy < n && mat[newx][newy] < mat[x][y])
            {
            ans += CountDecreasingPathsCell
            (mat, dp, n, newx, newy);
        }
    }
    // function that returns the answer
    dp[x][y] = ans;
    return ans;
}

// Function that counts the total
// decreasing path in the matrix
function countDecreasingPathsMatrix(n, mat)
{
    var dp = Array.from(Array(MAX),
    ()=> Array(MAX));

    // Initialising dp[][] to -1.
    for (var i = 0; i < n; i++)
        for (var j = 0; j < n; j++)
            dp[i][j] = -1;

    var sum = 0;

    // Calculating number of decreasing
    // path from each cell.
    for (var i = 0; i < n; i++)
        for (var j = 0; j < n; j++)
            sum += CountDecreasingPathsCell
            (mat, dp, n, i, j);

    return sum;
}

// Driver Code

var n = 2;
var mat = [ [ 1, 2 ], [ 1, 3 ] ];

// function call that returns the
// count of decreasing paths in a matrix
document.write( countDecreasingPathsMatrix(n, mat));

</script>
```

**Output:** 

```
8
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N <sup>2</sup> )