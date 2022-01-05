# 检查是否可以通过给定功率的矩阵

> 原文:[https://www . geesforgeks . org/check-可能-交叉矩阵-给定-power/](https://www.geeksforgeeks.org/check-possible-cross-matrix-given-power/)

给定一个由**N×M**组成的矩阵，每个单元格由一个整数组成。我们有 **K** 的初始力量，我们可以向右、向下或对角移动。当我们移动到任何一个细胞时，我们吸收了 mat[i][j]值，并从你的能量中释放了那么多。如果我们的力量在任何时候都小于 0，我们就不能再进一步。现在，我们的任务是找出从(1，1)到(n，m)是否有我们可以用幂 k 覆盖的路径，如果可能，输出我们可以吸收的最大值，否则如果没有路径打印“-1”。

示例:

```
Input : N = 3, M = 3, K = 7
        mat[][] = { { 2, 3, 1 },
                    { 6, 1, 9 },
                    { 8, 2, 3 } };
Output : 6
Path (1, 1) -> (2, 2) -> (3, 3) to complete
journey to absorb 6 value.

Input : N = 3, M = 4, K = 9
        mat[][] = { 
                    { 2, 3, 4, 1 },
                    { 6, 5, 5, 3 },
                    { 5, 2, 3, 4 }
                  };
Output : -1

```

这个想法是用动态规划来解决这个问题。
**进场:**

*   用 N*M*(K+1)维声明一个布尔 3D 矩阵，比如 dp[ ][ ][ ]，使得 dp[ i ][ j ][ k ]为真，如果有可能到达 i <sup>第</sup>行和 j <sup>第</sup>列中的平方，正好是到目前为止收集的 K 值。
*   We can write the recurrence dp[ i ][ j ][ k ] = true if either

    ```
    dp[i-1][j][k-mat[i][j]] *or* 
    dp[i][j-1][k-mat[i][j]] *or* 
    dp[i-1][j-1][k-mat[i][j]] 
    ```

    也就是我们可能采取的三种行动。

*   我们有基本情况 dp[0][0][0]为真。
*   如果 dp[n-1][m-1][k]对于 0 和 k+1 之间的所有 k 都为假，则答案为-2。
*   否则，答案是最大 k，使得 dp[n-1][m-1][k]为真。

下面是这种方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find if it is possible to cross
// the matrix with given power
#include <bits/stdc++.h>
#define N 105
#define R 3
#define C 4
using namespace std;

int maximumValue(int n, int m, int p, int grid[R][C])
{
    bool dp[N][N][N];

    // Initializing array dp with false value.
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            for (int k = 0; k < N; k++)
                dp[i][j][k] = false;
        }
    }

    // For each value of dp[i][j][k]
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            for (int k = grid[i][j]; k <= p; k++) {

                // For first cell and for each value of k
                if (i == 0 && j == 0) {
                    if (k == grid[i][j])
                        dp[i][j][k] = true;
                }

                // For first cell of each row
                else if (i == 0) {
                    dp[i][j][k] = (dp[i][j][k] || 
                        dp[i][j - 1][k - grid[i][j]]);
                }

                // For first cell of each column
                else if (j == 0) {
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j][k - grid[i][j]]);
                }

                // For rest of the cell
                else {

                    // Down movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i][j - 1][k - grid[i][j]]);

                    // Right movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j][k - grid[i][j]]);

                    // Diagonal movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j - 1][k - grid[i][j]]);
                }
            }
        }
    }

    // Finding maximum k.
    int ans = 0;
    for (ans = k; ans >= 0; ans--)
        if (dp[n - 1][m - 1][ans])
            break;

    return ans;
}

// Driver Code
int main()
{
    int n = 3, m = 4, p = 9;
    int grid[R][C] = {
        { 2, 3, 4, 1 },
        { 6, 5, 5, 3 },
        { 5, 2, 3, 4 }
    };

    cout << maximumValue(n, m, p, grid) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if it 
// is possible to cross the matrix
// with given power
class GFG
{

static final int N = 105;
static final int R = 3;
static final int C = 4;

static int maximumValue(int n, int m, int p,
                                int grid[][])
{
    boolean dp[][][] = new boolean[N][N][N];
    int i, j, k;

    // Initializing array dp with false value.
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++) {
            for (k = 0; k < N; k++)
                dp[i][j][k] = false;
        }
    }

    // For each value of dp[i][j][k]
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            for (k = grid[i][j]; k <= p; k++) {

                // For first cell and for 
                // each value of k
                if (i == 0 && j == 0) {
                    if (k == grid[i][j])
                        dp[i][j][k] = true;
                }

                // For first cell of each row
                else if (i == 0) {
                    dp[i][j][k] = (dp[i][j][k] || 
                        dp[i][j - 1][k - grid[i][j]]);
                }

                // For first cell of each column
                else if (j == 0) {
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j][k - grid[i][j]]);
                }

                // For rest of the cell
                else {

                    // Down movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i][j - 1][k - grid[i][j]]);

                    // Right movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j][k - grid[i][j]]);

                    // Diagonal movement.
                    dp[i][j][k] = (dp[i][j][k] ||
                        dp[i - 1][j - 1][k - grid[i][j]]);
                }
            }
        }
    }
    k = p;

    // Finding maximum k.
    int ans = 0;
    for (ans = k; ans >= 0; ans--)
        if (dp[n - 1][m - 1][ans])
            break;

    return ans;
}

// Driver code 
public static void main (String[] args)
{
    int n = 3, m = 4, p = 9;
    int grid[][] = {{ 2, 3, 4, 1 },
                    { 6, 5, 5, 3 },
                    { 5, 2, 3, 4 }};

    System.out.println(maximumValue(n, m, p, grid));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find if it is possible to cross
# the matrix with given power
N = 105
R = 3
C = 4

def maximumValue(n, m, p, grid):

    dp = [[[False for i in range(N)] for j in range(N)] for k in range(N)]

    # For each value of dp[i][j][k]
    for i in range(n):
        for j in range(m):
            k = grid[i][j] 
            while(k <= p):

                # For first cell and for each value of k
                if (i == 0 and j == 0):
                    if (k == grid[i][j]):
                        dp[i][j][k] = True

                # For first cell of each row
                elif (i == 0):
                    dp[i][j][k] = (dp[i][j][k] or 
                    dp[i][j - 1][k - grid[i][j]])

                # For first cell of each column
                elif (j == 0):
                    dp[i][j][k] = (dp[i][j][k] or 
                    dp[i - 1][j][k - grid[i][j]])

                # For rest of the cell
                else:

                    # Down movement.
                    dp[i][j][k] = (dp[i][j][k] or 
                    dp[i][j - 1][k - grid[i][j]])

                    # Right movement.
                    dp[i][j][k] = (dp[i][j][k] or 
                    dp[i - 1][j][k - grid[i][j]])

                    # Diagonal movement.
                    dp[i][j][k] = (dp[i][j][k] or 
                    dp[i - 1][j - 1][k - grid[i][j]])
                k += 1

    # Finding maximum k.
    ans = k
    while(ans >= 0):
        if (dp[n - 1][m - 1][ans]):
            break
        ans -= 1

    return ans

# Driver Code
n = 3
m = 4
p = 9
grid = [[2, 3, 4, 1],[6, 5, 5, 3 ],[5, 2, 3, 4]]

print(maximumValue(n, m, p, grid))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find if it
// is possible to cross the matrix
// with given power
using System;

class GFG {

    static int N = 105;
    // static int R = 3;
    // static int C = 4;

    static int maximumValue(int n, int m, int p,
                                   int[, ] grid)
    {
        bool[,, ] dp = new bool[N, N, N];
        int i, j, k;

        // Initializing array dp with false value.
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++) {
                for (k = 0; k < N; k++)
                    dp[i, j, k] = false;
            }
        }

        // For each value of dp[i][j][k]
        for (i = 0; i < n; i++) {
            for (j = 0; j < m; j++) {
                for (k = grid[i, j]; k <= p; k++) {

                    // For first cell and for
                    // each value of k
                    if (i == 0 && j == 0) {
                        if (k == grid[i, j])
                            dp[i, j, k] = true;
                    }

                    // For first cell of each row
                    else if (i == 0) {
                        dp[i, j, k] = (dp[i, j, k] || 
                        dp[i, j - 1, k - grid[i, j]]);
                    }

                    // For first cell of each column
                    else if (j == 0) {
                        dp[i, j, k] = (dp[i, j, k] || 
                        dp[i - 1, j, k - grid[i, j]]);
                    }

                    // For rest of the cell
                    else {

                        // Down movement.
                        dp[i, j, k] = (dp[i, j, k] || 
                        dp[i, j - 1, k - grid[i, j]]);

                        // Right movement.
                        dp[i, j, k] = (dp[i, j, k] || 
                        dp[i - 1, j, k - grid[i, j]]);

                        // Diagonal movement.
                        dp[i, j, k] = (dp[i, j, k] ||
                        dp[i - 1, j - 1, k - grid[i, j]]);
                    }
                }
            }
        }
        k = p;

        // Finding maximum k.
        int ans = 0;
        for (ans = k; ans >= 0; ans--)
            if (dp[n - 1, m - 1, ans])
                break;

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 3, m = 4, p = 9;
        int[, ] grid = { { 2, 3, 4, 1 },
                         { 6, 5, 5, 3 },
                         { 5, 2, 3, 4 } };

        Console.WriteLine(maximumValue(n, m, p, grid));
    }
}

// This code is contributed by vt_m.
```

**输出:**

```
-1

```

**时间复杂度:** O(n <sup>3</sup>

本文由 anuj0503 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](https://contribute.geeksforgeeks.org/)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。