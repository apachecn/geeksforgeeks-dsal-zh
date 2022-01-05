# 矩阵中从入口到出口的路径和最大路径和

> 原文:[https://www . geesforgeks . org/path-从矩阵中的入口到出口-最大路径-sum/](https://www.geeksforgeeks.org/paths-from-entry-to-exit-in-matrix-and-maximum-path-sum/)

给定一个迷宫，它是一个 **N * N** 网格**网格[][]** 。迷宫的每个单元包含数字 **1** 、 **2** 或 **3** ，其定义动作为:

*   如果**格子[i][j] = 1** ，那么唯一有效的移动就是**格子[i][j + 1]** 。
*   如果**格子[i][j] = 2** ，那么唯一有效的移动就是**格子[i + 1][j]** 。
*   如果**格子[i][j] = 3** ，那么有效的移动是**格子[i][j + 1]** 和**格子[i + 1][j]** 。

现在，任务是找到从**网格【0】【0】**到**网格【N–1】【N–1】**的所有路径的计数，以及所有路径中的最大可能和，即当访问单元的所有值加到和上时。
**例:**

> **输入:**网格[][] = {
> {3，2}，
> {3，1}}
> **输出:**
> 总路径:2
> 最大和:7
> 两个有效路径为
> (0，0)-(T26)【0，1)-(T27】(1，1)，和为 3 + 2 + 1 = 6
> 和(0，0)-(T28)【1，0)-(T29】(1 1)以和为 3 + 3 + 1 = 7
> **输入:**网格[][] = {
> {1，1，3，2，1}，
> {3，2，2，1，2}，
> {1，3，3，1，3}，
> {1，2，3，1，2}，
> {1，1，3，1}}
> **输出:**
> 总计

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。
要计算路径数，创建一个 **dp[][]** 数组，其中 **dp[i][j]** 将存储从**网格[i][j]** 到**网格[N–1][N–1]**的路径数，循环关系为:

1.  如果**网格[i][j] = 1** ，那么 dp[i][j] = dp[i][j + 1]。
2.  如果**网格[i][j] = 2** ，那么 dp[i][j] = dp[i + 1][j]。
3.  如果**网格[i][j] = 1** ，那么 dp[i][j] = dp[i][j + 1] + dp[i + 1][j]。

而终止条件将是当源和目的地相同时，即**DP[N–1][N–1]= 1**。
现在，为了找到最大和路径，可以创建另一个 **dp[][]** 数组，其中 **dp[i][j]** 将存储从**网格[i][j]** 到**网格[N–1][N–1]**的路径的最大和，并且递归关系为:

1.  如果**网格[i][j] = 1** ，那么 dp[i][j] =网格[i][j] + dp[i][j + 1]。
2.  如果**网格[i][j] = 2** ，那么 dp[i][j] =网格[i][j] + dp[i + 1][j]。
3.  如果**网格[i][j] = 1** ，那么 dp[i][j] =网格[i][j] +最大值(dp[i][j + 1] + dp[i + 1][j])。

而终止条件将再次是当源和目的地相同时，即**DP[N–1][N–1]=网格[N–1][N–1]**。

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
#define COL 5
#define ROW 5
using namespace std;

// Recursive function to return the total
// paths from grid[i][j] to grid[n - 1][n - 1]
int totalPaths(int i, int j, int n,
                int grid[][COL], int dp[][COL])
{

    // Out of bounds
    if (i < 0 || j < 0 || i >= n || j >= n)
        return 0;

    // If the current state hasn't been solved before
    if (dp[i][j] == -1)
    {

        // Only valid move is right
        if (grid[i][j] == 1)
            dp[i][j] = totalPaths(i, j + 1, n, grid, dp);

        // Only valid move is down
        else if (grid[i][j] == 2)
            dp[i][j] = totalPaths(i + 1, j, n, grid, dp);

        // Right and down, both are valid moves
        else
            dp[i][j] = totalPaths(i, j + 1, n, grid, dp)
                    + totalPaths(i + 1, j, n, grid, dp);
    }
    return dp[i][j];
}

// Recursive function to return the maximum
// sum along the path from grid[i][j] to grid[n - 1][n - 1]
int maxSumPath(int i, int j, int n,
                int grid[ROW][COL], int dp[ROW][COL])
{

    // Out of bounds
    if (i < 0 || j < 0 || i >= n || j >= n)
        return 0;

    // If the current state hasn't been solved before
    if (dp[i][j] == -1)
    {

        // Only valid move is right
        if (grid[i][j] == 1)
            dp[i][j] = grid[i][j] + maxSumPath(i,
                                    j + 1, n, grid, dp);

        // Only valid move is down
        else if (grid[i][j] == 2)
            dp[i][j] = grid[i][j] + maxSumPath(i + 1,
                                    j, n, grid, dp);

        // Right and down, both are valid moves
        else
            dp[i][j] = grid[i][j]
                    + max(maxSumPath(i, j + 1, n, grid, dp),
                        maxSumPath(i + 1, j, n, grid, dp));
    }
    return dp[i][j];
}

// Driver code
int main()
{
    int grid[ROW][COL] = { { 1, 1, 3, 2, 1 },
                           { 3, 2, 2, 1, 2 },
                           { 1, 3, 3, 1, 3 },
                           { 1, 2, 3, 1, 2 },
                           { 1, 1, 1, 3, 1 } };
    int n = ROW;

    // Fill the dp[][] array with -1
    int dp[ROW][COL];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        dp[i][j] = -1;
    }

    // When source and destination are same
    // then there is only 1 path
    dp[n - 1][n - 1] = 1;

    // Print the count of paths from
    // grid[0][0] to grid[n - 1][n - 1]
    cout<<"Total paths: "
        << totalPaths(0, 0, n, grid, dp) << endl;

    // Fill the dp[][] array again with -1
    //for (int i = 0; i < n; i++)
    // Arrays.fill(dp[i], -1);
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        dp[i][j] = -1;
    }

    // When source and destination are same
    // then the sum is grid[n - 1][n - 1]
    dp[n - 1][n - 1] = grid[n - 1][n - 1];

    // Print the maximum sum among all the paths
    // from grid[0][0] to grid[n - 1][n - 1]
    cout<< "Maximum sum: "
        << maxSumPath(0, 0, n, grid, dp)<<endl;
    return 0;
}

// This code is contribiuted by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG {

    // Recursive function to return the total
    // paths from grid[i][j] to grid[n - 1][n - 1]
    static int totalPaths(int i, int j, int n, int grid[][], int dp[][])
    {

        // Out of bounds
        if (i < 0 || j < 0 || i >= n || j >= n)
            return 0;

        // If the current state hasn't been solved before
        if (dp[i][j] == -1) {

            // Only valid move is right
            if (grid[i][j] == 1)
                dp[i][j] = totalPaths(i, j + 1, n, grid, dp);

            // Only valid move is down
            else if (grid[i][j] == 2)
                dp[i][j] = totalPaths(i + 1, j, n, grid, dp);

            // Right and down, both are valid moves
            else
                dp[i][j] = totalPaths(i, j + 1, n, grid, dp)
                           + totalPaths(i + 1, j, n, grid, dp);
        }
        return dp[i][j];
    }

    // Recursive function to return the maximum
    // sum along the path from grid[i][j] to grid[n - 1][n - 1]
    static int maxSumPath(int i, int j, int n, int grid[][], int dp[][])
    {

        // Out of bounds
        if (i < 0 || j < 0 || i >= n || j >= n)
            return 0;

        // If the current state hasn't been solved before
        if (dp[i][j] == -1) {

            // Only valid move is right
            if (grid[i][j] == 1)
                dp[i][j] = grid[i][j] + maxSumPath(i, j + 1, n, grid, dp);

            // Only valid move is down
            else if (grid[i][j] == 2)
                dp[i][j] = grid[i][j] + maxSumPath(i + 1, j, n, grid, dp);

            // Right and down, both are valid moves
            else
                dp[i][j] = grid[i][j]
                           + Math.max(maxSumPath(i, j + 1, n, grid, dp),
                                      maxSumPath(i + 1, j, n, grid, dp));
        }
        return dp[i][j];
    }

    // Driver code
    public static void main(String[] args)
    {
        int grid[][] = { { 1, 1, 3, 2, 1 },
                         { 3, 2, 2, 1, 2 },
                         { 1, 3, 3, 1, 3 },
                         { 1, 2, 3, 1, 2 },
                         { 1, 1, 1, 3, 1 } };
        int n = grid.length;

        // Fill the dp[][] array with -1
        int dp[][] = new int[n][n];
        for (int i = 0; i < n; i++)
            Arrays.fill(dp[i], -1);

        // When source and destination are same
        // then there is only 1 path
        dp[n - 1][n - 1] = 1;

        // Print the count of paths from
        // grid[0][0] to grid[n - 1][n - 1]
        System.out.println("Total paths: "
                           + totalPaths(0, 0, n, grid, dp));

        // Fill the dp[][] array again with -1
        for (int i = 0; i < n; i++)
            Arrays.fill(dp[i], -1);

        // When source and destination are same
        // then the sum is grid[n - 1][n - 1]
        dp[n - 1][n - 1] = grid[n - 1][n - 1];

        // Print the maximum sum among all the paths
        // from grid[0][0] to grid[n - 1][n - 1]
        System.out.println("Maximum sum: "
                           + maxSumPath(0, 0, n, grid, dp));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to return the total
# paths from grid[i][j] to grid[n - 1][n - 1]
def totalPaths(i, j, n, grid, dp):

    # Out of bounds
    if (i < 0 or j < 0 or i >= n or j >= n):
        return 0

    # If the current state
    # hasn't been solved before
    if (dp[i][j] == -1):

        # Only valid move is right
        if (grid[i][j] == 1):
            dp[i][j] = totalPaths(i, j + 1, n, grid, dp)

        # Only valid move is down
        elif (grid[i][j] == 2):
            dp[i][j] = totalPaths(i + 1, j, n, grid, dp)

        # Right and down, both are valid moves
        else:
            dp[i][j] = totalPaths(i, j + 1, n, grid, dp) +\
                       totalPaths(i + 1, j, n, grid, dp)

    return dp[i][j]

# Recursive function to return the maximum
# sum along the path from grid[i,j] to grid[n - 1,n - 1]
def maxSumPath(i, j, n, grid, dp):

    # Out of bounds
    if (i < 0 or j < 0 or i >= n or j >= n):
        return 0

    # If the current state
    # hasn't been solved before
    if (dp[i][j] == -1):

        # Only valid move is right
        if (grid[i][j] == 1):
            dp[i][j] = grid[i][j] + \
                       maxSumPath(i, j + 1, n, grid, dp)

        # Only valid move is down
        elif (grid[i][j] == 2):
            dp[i][j] = grid[i][j] + \
                       maxSumPath(i + 1, j, n, grid, dp)

        # Right and down, both are valid moves
        else:
            dp[i][j] = grid[i][j] + \
                       max(maxSumPath(i, j + 1, n, grid, dp),
                           maxSumPath(i + 1, j, n, grid, dp))

    return dp[i][j]

# Driver code
if __name__ == '__main__':

    grid = [[ 1, 1, 3, 2, 1 ],
            [ 3, 2, 2, 1, 2 ],
            [ 1, 3, 3, 1, 3 ],
            [ 1, 2, 3, 1, 2 ],
            [ 1, 1, 1, 3, 1 ]]

    n = len(grid[0])

    # Fill the dp[n][n] array with -1
    dp= [[-1] * n] * n

    # When source and destination are same
    # then there is only 1 path
    dp[n - 1][n - 1] = 1

    # Print the count of paths from
    # grid[0,0] to grid[n - 1][n - 1]
    print("Total paths:",
           totalPaths(0, 0, n, grid, dp))

    # Fill the dp[n][n] array again with -1
    dp= [[-1] * n] * n

    # When source and destination are same
    # then the sum is grid[n - 1][n - 1]
    dp[n - 1][n - 1] = grid[n - 1][n - 1]

    # Print the maximum sum among all the paths
    # from grid[0,0] to grid[n - 1][n - 1]
    print("Maximum sum:",
           maxSumPath(0, 0, n, grid, dp))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Recursive function to return the total
// paths from grid[i][j] to grid[n - 1][n - 1]
static int totalPaths(int i, int j, int n,
                      int [,]grid, int [,]dp)
{

    // Out of bounds
    if (i < 0 || j < 0 || i >= n || j >= n)
        return 0;

    // If the current state
    // hasn't been solved before
    if (dp[i, j] == -1)
    {

        // Only valid move is right
        if (grid[i, j] == 1)
            dp[i, j] = totalPaths(i, j + 1, n, grid, dp);

        // Only valid move is down
        else if (grid[i, j] == 2)
            dp[i, j] = totalPaths(i + 1, j, n, grid, dp);

        // Right and down, both are valid moves
        else
            dp[i, j] = totalPaths(i, j + 1, n, grid, dp) +
                      totalPaths(i + 1, j, n, grid, dp);
    }
    return dp[i, j];
}

// Recursive function to return the maximum
// sum along the path from grid[i,j] to grid[n - 1,n - 1]
static int maxSumPath(int i, int j, int n,
                      int [,]grid, int [,]dp)
{

    // Out of bounds
    if (i < 0 || j < 0 || i >= n || j >= n)
        return 0;

    // If the current state
    // hasn't been solved before
    if (dp[i, j] == -1)
    {

        // Only valid move is right
        if (grid[i, j] == 1)
            dp[i, j] = grid[i, j] + maxSumPath(i, j + 1,
                                               n, grid, dp);

        // Only valid move is down
        else if (grid[i,j] == 2)
            dp[i, j] = grid[i, j] + maxSumPath(i + 1, j,
                                               n, grid, dp);

        // Right and down, both are valid moves
        else
            dp[i, j] = grid[i, j] +
                       Math.Max(maxSumPath(i, j + 1, n, grid, dp),
                                maxSumPath(i + 1, j, n, grid, dp));
    }
    return dp[i, j];
}

// Driver code
public static void Main(String[] args)
{
    int [,]grid = { { 1, 1, 3, 2, 1 },
                    { 3, 2, 2, 1, 2 },
                    { 1, 3, 3, 1, 3 },
                    { 1, 2, 3, 1, 2 },
                    { 1, 1, 1, 3, 1 } };
    int n = grid.GetLength(0);

    // Fill the dp[,] array with -1
    int [,]dp = new int[n, n];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dp[i, j] = -1;

    // When source and destination are same
    // then there is only 1 path
    dp[n - 1, n - 1] = 1;

    // Print the count of paths from
    // grid[0,0] to grid[n - 1,n - 1]
    Console.WriteLine("Total paths: " +
                       totalPaths(0, 0, n, grid, dp));

    // Fill the dp[,] array again with -1
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dp[i, j] = -1;

    // When source and destination are same
    // then the sum is grid[n - 1,n - 1]
    dp[n - 1, n - 1] = grid[n - 1, n - 1];

    // Print the maximum sum among all the paths
    // from grid[0,0] to grid[n - 1,n - 1]
    Console.WriteLine("Maximum sum: " +
                       maxSumPath(0, 0, n, grid, dp));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Recursive function to return the total
    // paths from grid[i][j] to grid[n - 1][n - 1]
    function totalPaths(i, j, n, grid, dp)
    {

        // Out of bounds
        if (i < 0 || j < 0 || i >= n || j >= n)
            return 0;

        // If the current state hasn't been solved before
        if (dp[i][j] == -1) {

            // Only valid move is right
            if (grid[i][j] == 1)
                dp[i][j] = totalPaths(i, j + 1, n, grid, dp);

            // Only valid move is down
            else if (grid[i][j] == 2)
                dp[i][j] = totalPaths(i + 1, j, n, grid, dp);

            // Right and down, both are valid moves
            else
                dp[i][j] = totalPaths(i, j + 1, n, grid, dp)
                           + totalPaths(i + 1, j, n, grid, dp);
        }
        return dp[i][j];
    }

    // Recursive function to return the maximum
    // sum along the path from grid[i][j] to grid[n - 1][n - 1]
    function maxSumPath(i, j, n, grid, dp)
    {

        // Out of bounds
        if (i < 0 || j < 0 || i >= n || j >= n)
            return 0;

        // If the current state hasn't been solved before
        if (dp[i][j] == -1) {

            // Only valid move is right
            if (grid[i][j] == 1)
                dp[i][j] = grid[i][j] + maxSumPath(i, j + 1, n, grid, dp);

            // Only valid move is down
            else if (grid[i][j] == 2)
                dp[i][j] = grid[i][j] + maxSumPath(i + 1, j, n, grid, dp);

            // Right and down, both are valid moves
            else
                dp[i][j] = grid[i][j]
                           + Math.max(maxSumPath(i, j + 1, n, grid, dp),
                                      maxSumPath(i + 1, j, n, grid, dp));
        }
        return dp[i][j];
    }

    let grid = [ [ 1, 1, 3, 2, 1 ],
                [ 3, 2, 2, 1, 2 ],
                [ 1, 3, 3, 1, 3 ],
                [ 1, 2, 3, 1, 2 ],
                [ 1, 1, 1, 3, 1 ] ];
  let n = grid.length;

  // Fill the dp[][] array with -1
  let dp = new Array(n);
  for (let i = 0; i < n; i++)
  {
      dp[i] = new Array(n);
      for (let j = 0; j < n; j++)
    {
        dp[i][j] = -1;
    }
  }

  // When source and destination are same
  // then there is only 1 path
  dp[n - 1][n - 1] = 1;

  // Print the count of paths from
  // grid[0][0] to grid[n - 1][n - 1]
  document.write("Total paths: " + totalPaths(0, 0, n, grid, dp) + "</br>");

  // Fill the dp[][] array again with -1
  for (let i = 0; i < n; i++)
  {
      for (let j = 0; j < n; j++)
    {
        dp[i][j] = -1;
    }
  }

  // When source and destination are same
  // then the sum is grid[n - 1][n - 1]
  dp[n - 1][n - 1] = grid[n - 1][n - 1];

  // Print the maximum sum among all the paths
  // from grid[0][0] to grid[n - 1][n - 1]
  document.write("Maximum sum: " + maxSumPath(0, 0, n, grid, dp));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
Total paths: 4
Maximum sum: 18
```

**时间复杂度:**O(n<sup>2</sup>)
T5】空间复杂度: O(n <sup>2</sup> )