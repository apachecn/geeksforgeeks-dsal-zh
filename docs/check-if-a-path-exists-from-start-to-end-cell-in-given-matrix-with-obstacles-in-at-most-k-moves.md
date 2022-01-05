# 检查给定矩阵中从开始到结束单元是否存在路径，最多 K 个移动中有障碍物

> 原文:[https://www . geesforgeks . org/check-if-a-path-exists-start-to-end-cell-in-给定矩阵-最多有 k 个移动障碍/](https://www.geeksforgeeks.org/check-if-a-path-exists-from-start-to-end-cell-in-given-matrix-with-obstacles-in-at-most-k-moves/)

给定一个正整数 **K** 和一个由字符**' '组成的尺寸 **N * M** 的[矩阵网格](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**和 **'#'** ，其中**' '**代表未阻塞的单元格， **'#'** 代表阻塞的单元格，任务是检查至多 **K** 中的未阻塞单元格是否可以从矩阵的左上角单元格到达网格的右下角，以便向右或向下移动一次即可到达其相邻的单元格。

**示例:**

> **输入:**网格[][] = {{ ' . ', '.', '.'}, {'#', '.', '.'}, {'#', '#', '.'}}，K = 4
> **输出:**是
> **解释:**使用以下一组移动可以到达给定网格的右下单元格:右- >向下- >右- >向下。因此，所需的移动次数是 4，这是最小可能的，并且小于 k
> 
> **输入:**网格[][] = {{ ' . ', '.', '.', '.'}, {'.', '.', '.', '.'}, {'#', '#', '#', '#'}, {'.', '.', '.', '.'}}，K = 4
> **输出:**否
> **说明:**从给定矩阵的左上角单元格到右下角单元格没有可能的一组移动。

**方法:**通过使用[制表方法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)借助[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)可以解决给定的问题。它可以通过预计算从左上角移动到右下角所需的最小移动次数来解决，方法类似于本文[中讨论的方法。可以观察到，如果 **dp[i][j]** 代表从 **(0，0)** 到达单元格 **(i，j)** 的最小移动次数，那么 dp 关系可以表述如下:](https://www.geeksforgeeks.org/shortest-distance-two-cells-matrix-grid/)

> dp[i][j] = min(dp[i][j]，1+DP[I-1][j]，1+DP[I][j-1])

此后，如果最小移动次数最多为 **K** ，则打印“是”，否则打印“否”。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to check if it is possible
// to reach the bottom right of the grid
// from top left using atmost K moves
string canReach(vector<vector<char> >& grid, int K)
{
    int N = grid.size();
    int M = grid[0].size();

    // Stores the DP states
    vector<vector<long long> > dp(
        N, vector<long long>(M, INT_MAX));

    // Initial condition
    dp[0][0] = 0;

    // Initializing the DP table
    // in 1st row
    for (int i = 1; i < M; i++) {
        if (grid[0][i] == '.') {
            dp[0][i] = 1 + dp[0][i - 1];
        }
        else
            break;
    }

    // Initializing the DP table
    // in 1st column
    for (int i = 1; i < N; i++) {
        if (grid[i][0] == '.') {
            dp[i][0] = 1 + dp[i - 1][0];
        }
        else
            break;
    }

    // Iterate through the grid
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {

            // If current position
            // is not an obstacle,
            // update the dp state
            if (grid[i][j] == '.') {
                dp[i][j] = min(
                    dp[i][j],
                    1 + min(dp[i - 1][j],
                            dp[i][j - 1]));
            }
        }
    }

    // Return answer
    return (dp[N - 1][M - 1] <= K
                ? "Yes"
                : "No");
}

// Driver Code
int main()
{
    vector<vector<char> > grid
        = { { '.', '.', '.' },
            { '#', '.', '.' },
            { '#', '#', '.' } };
    int K = 4;
    cout << canReach(grid, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
//include "bits/stdJava.h"
import java.util.*;

class GFG
{

// Function to check if it is possible
// to reach the bottom right of the grid
// from top left using atmost K moves
static String canReach(char[][] grid, int K)
{
    int N = grid.length;
    int M = grid[0].length;

    // Stores the DP states
    int[][] dp = new int[N][M];
    for(int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++) {
            dp[i][j] = Integer.MAX_VALUE;
        }
    }

    // Initial condition
    dp[0][0] = 0;

    // Initializing the DP table
    // in 1st row
    for (int i = 1; i < M; i++) {
        if (grid[0][i] == '.') {
            dp[0][i] = 1 + dp[0][i - 1];
        }
        else
            break;
    }

    // Initializing the DP table
    // in 1st column
    for (int i = 1; i < N; i++) {
        if (grid[i][0] == '.') {
            dp[i][0] = 1 + dp[i - 1][0];
        }
        else
            break;
    }

    // Iterate through the grid
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {

            // If current position
            // is not an obstacle,
            // update the dp state
            if (grid[i][j] == '.') {
                dp[i][j] = Math.min(
                    dp[i][j],
                    1 + Math.min(dp[i - 1][j],
                            dp[i][j - 1]));
            }
        }
    }

    // Return answer
    return (dp[N - 1][M - 1] <= K
                ? "Yes"
                : "No");
}

// Driver Code
public static void main(String[] args)
{
    char[][] grid
        = { { '.', '.', '.' },
            { '/', '.', '.' },
            { '/', '/', '.' } };
    int K = 4;
    System.out.print(canReach(grid, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
INT_MAX = 2147483647

# Function to check if it is possible
# to reach the bottom right of the grid
# from top left using atmost K moves
def canReach(grid, K):

    N = len(grid)
    M = len(grid[0])

    # Stores the DP states
    dp = [[INT_MAX for _ in range(M)]
                   for _ in range(N)]

    # Initial condition
    dp[0][0] = 0

    # Initializing the DP table
    # in 1st row
    for i in range(1, M):
        if (grid[0][i] == '.'):
            dp[0][i] = 1 + dp[0][i - 1]
        else:
            break

    # Initializing the DP table
    # in 1st column
    for i in range(1, N):
        if (grid[i][0] == '.'):
            dp[i][0] = 1 + dp[i - 1][0]
        else:
            break

    # Iterate through the grid
    for i in range(1, N):
        for j in range(1, M):

            # If current position
            # is not an obstacle,
            # update the dp state
            if (grid[i][j] == '.'):
                dp[i][j] = min(dp[i][j],
                       1 + min(dp[i - 1][j],
                               dp[i][j - 1]))

    # Return answer
    if dp[N - 1][M - 1] <= K:
        return("Yes")
    else:
        return("No")

# Driver Code
if __name__ == "__main__":

    grid = [ [ '.', '.', '.' ],
             [ '#', '.', '.' ],
             [ '#', '#', '.' ] ]
    K = 4

    print(canReach(grid, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
//include "bits/stdJava.h"
using System;

class GFG
{

// Function to check if it is possible
// to reach the bottom right of the grid
// from top left using atmost K moves
static String canReach(char[,] grid, int K)
{
    int N = grid.GetLength(0);
    int M = grid.GetLength(1);

    // Stores the DP states
    int[,] dp = new int[N,M];
    for(int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++) {
            dp[i, j] = int.MaxValue;
        }
    }

    // Initial condition
    dp[0, 0] = 0;

    // Initializing the DP table
    // in 1st row
    for (int i = 1; i < M; i++) {
        if (grid[0, i] == '.') {
            dp[0, i] = 1 + dp[0, i - 1];
        }
        else
            break;
    }

    // Initializing the DP table
    // in 1st column
    for (int i = 1; i < N; i++) {
        if (grid[i, 0] == '.') {
            dp[i, 0] = 1 + dp[i - 1, 0];
        }
        else
            break;
    }

    // Iterate through the grid
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {

            // If current position
            // is not an obstacle,
            // update the dp state
            if (grid[i, j] == '.') {
                dp[i, j] = Math.Min(
                    dp[i, j],
                    1 + Math.Min(dp[i - 1, j],
                            dp[i, j - 1]));
            }
        }
    }

    // Return answer
    return (dp[N - 1, M - 1] <= K
                ? "Yes"
                : "No");
}

// Driver Code
public static void Main()
{
    char[,] grid
        = { { '.', '.', '.' },
            { '/', '.', '.' },
            { '/', '/', '.' } };
    int K = 4;
    Console.Write(canReach(grid, K));
}
}

// This code is contributed by Saurabh jaiswal
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to check if it is possible
       // to reach the bottom right of the grid
       // from top left using atmost K moves
       function canReach(grid, K) {
           let N = grid.length;
           let M = grid[0].length;

           // Stores the DP states
           let dp = new Array(N);
           for (let i = 0; i < dp.length; i++) {
               dp[i] = new Array(M).fill(Number.MAX_VALUE);
           }

           // Initial condition
           dp[0][0] = 0;

           // Initializing the DP table
           // in 1st row
           for (let i = 1; i < M; i++) {
               if (grid[0][i] == '.') {
                   dp[0][i] = 1 + dp[0][i - 1];
               }
               else
                   break;
           }

           // Initializing the DP table
           // in 1st column
           for (let i = 1; i < N; i++) {
               if (grid[i][0] == '.') {
                   dp[i][0] = 1 + dp[i - 1][0];
               }
               else
                   break;
           }

           // Iterate through the grid
           for (let i = 1; i < N; i++) {
               for (let j = 1; j < M; j++) {

                   // If current position
                   // is not an obstacle,
                   // update the dp state
                   if (grid[i][j] == '.') {
                       dp[i][j] = Math.min(
                           dp[i][j],
                           1 + Math.min(dp[i - 1][j],
                               dp[i][j - 1]));
                   }
               }
           }

           // Return answer
           return (dp[N - 1][M - 1] <= K
               ? "Yes"
               : "No");
       }

       // Driver Code
       let grid
           = [['.', '.', '.'],
           ['#', '.', '.'],
           ['#', '#', '.']];
       let K = 4;
       document.write(canReach(grid, K));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*