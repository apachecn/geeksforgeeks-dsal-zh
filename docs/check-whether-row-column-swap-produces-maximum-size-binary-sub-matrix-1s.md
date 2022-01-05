# 检查行或列交换是否产生全为 1 的最大尺寸二进制子矩阵

> 原文:[https://www . geesforgeks . org/check-是否-row-column-swap-products-maximum-size-binary-sub-matrix-1s/](https://www.geeksforgeeks.org/check-whether-row-column-swap-produces-maximum-size-binary-sub-matrix-1s/)

给定一个二进制矩阵，任务是找出是行交换还是列交换给出全为 1 的最大尺寸子矩阵。在行交换中，我们可以交换任意两行。在列交换中，我们可以交换任意两列。输出“行交换”或“列交换”以及最大大小。

**示例:**

```
Input : 1 1 1
        1 0 1
Output : Column Swap
         4
By swapping column 1 and column 2(0-based indexing), 
index (0, 0) to (1, 1) makes the largest binary 
sub-matrix.

Input : 0 0 0
        1 1 0
        1 1 0
        0 0 0
        1 1 0 
Output : Row Swap
         6

Input : 1 1 0
        0 0 0
        0 0 0
        1 1 0
        1 1 0
        0 0 0
        1 1 0 
Output : Row Swap
         8

```

想法是找到行交换和列交换最大大小的二进制子矩阵并进行比较。

要找到允许行交换的最大二进制子矩阵，制作一个二维数组，比如 dp[i][j]。dp[i][j]的每个值包含第 I 行(I，j)右侧的连续 1 的数量。现在，将一维临时数组中的每一列逐个存储，比如 b[]和排序，并找到最大 b[i]*(n–I)，因为 b[I]表示子矩阵宽度，(n–I)表示子矩阵高度。

同样，要找到允许列交换的最大大小二进制子矩阵，请找到 dp[i][j]，其中每个值都包含第 j 列中(I，j)以下的连续 1 的数量。同样，将每一行逐个存储在一维临时数组中，比如 b[]和 sort。求最大 b[i]*(m–I)，因为 b[I]表示子矩阵高度，而(n–I)表示子矩阵宽度。

以下是该方法的实现:

## C++

```
// C++ program to find maximum binary sub-matrix
// with row swaps and column swaps.
#include <bits/stdc++.h>
#define R 5
#define C 3
using namespace std;

// Precompute the number of consecutive 1 below the
// (i, j) in j-th column and the number of consecutive 1s
// on right side of (i, j) in i-th row.
void precompute(int mat[R][C], int ryt[][C + 2],
                               int dwn[R + 2][C + 2])
{
    // Travesing the 2d matrix from top-right.
    for (int j=C-1; j>=0; j--)
    {
        for (int i=0; i<R; ++i)
        {
            // If (i,j) contain 0, do nothing
            if (mat[i][j] == 0)
                ryt[i][j] = 0;

            // Counting consecutive 1 on right side
            else
                ryt[i][j] = ryt[i][j + 1] + 1;
        }
    }

    // Travesing the 2d matrix from bottom-left.
    for (int i = R - 1; i >= 0; i--)
    {
        for (int j = 0; j < C; ++j)
        {
            // If (i,j) contain 0, do nothing
            if (mat[i][j] == 0)
                dwn[i][j] = 0;

            // Counting consecutive 1 down to (i,j).
            else
                dwn[i][j] = dwn[i + 1][j] + 1;
        }
    }
}

// Return maximum size submatrix with row swap allowed.
int solveRowSwap(int ryt[R + 2][C + 2])
{
    int b[R] = { 0 }, ans = 0;

    for (int j=0; j<C; j++)
    {
        // Copying the column
        for (int i=0; i<R; i++)
            b[i] = ryt[i][j];

        // Sort the copied array
        sort(b, b + R);

        // Find maximum submatrix size.
        for (int i = 0; i < R; ++i)
            ans = max(ans, b[i] * (R - i));
    }

    return ans;
}

// Return maximum size submatrix with column
// swap allowed.
int solveColumnSwap(int dwn[R + 2][C + 2])
{
    int b[C] = { 0 }, ans = 0;

    for (int i = 0; i < R; ++i)
    {
        // Copying the row.
        for (int j = 0; j < C; ++j)
            b[j] = dwn[i][j];

        // Sort the copied array
        sort(b, b + C);

        // Find maximum submatrix size.
        for (int i = 0; i < C; ++i)
            ans = max(ans, b[i] * (C - i));
    }

    return ans;
}

void findMax1s(int mat[R][C])
{
    int ryt[R + 2][C + 2], dwn[R + 2][C + 2];
    memset(ryt, 0, sizeof ryt);
    memset(dwn, 0, sizeof dwn);

    precompute(mat, ryt, dwn);

    // Solving for row swap and column swap
    int rswap = solveRowSwap(ryt);
    int cswap = solveColumnSwap(dwn);

    // Comparing both.
    (rswap > cswap)? (cout << "Row Swap\n" << rswap << endl):
                     (cout << "Column Swap\n" << cswap << endl);
}

// Driven Program
int main()
{
    int mat[R][C] = {{ 0, 0, 0 },
                     { 1, 1, 0 },
                     { 1, 1, 0 },
                     { 0, 0, 0 },
                     { 1, 1, 0 }};

    findMax1s(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to find maximum binary sub-matrix
// with row swaps and column swaps.
class GFG {

    static int R = 5;
    static int C = 3;

// Precompute the number of consecutive 1 below the
// (i, j) in j-th column and the number of consecutive 1s
// on right side of (i, j) in i-th row.
    static void precompute(int mat[][], int ryt[][],
            int dwn[][]) {
        // Travesing the 2d matrix from top-right.
        for (int j = C - 1; j >= 0; j--) {
            for (int i = 0; i < R; ++i) {
                // If (i,j) contain 0, do nothing
                if (mat[i][j] == 0) {
                    ryt[i][j] = 0;
                } // Counting consecutive 1 on right side
                else {
                    ryt[i][j] = ryt[i][j + 1] + 1;
                }
            }
        }

        // Travesing the 2d matrix from bottom-left.
        for (int i = R - 1; i >= 0; i--) {
            for (int j = 0; j < C; ++j) {
                // If (i,j) contain 0, do nothing
                if (mat[i][j] == 0) {
                    dwn[i][j] = 0;
                } // Counting consecutive 1 down to (i,j).
                else {
                    dwn[i][j] = dwn[i + 1][j] + 1;
                }
            }
        }
    }

// Return maximum size submatrix with row swap allowed.
    static int solveRowSwap(int ryt[][]) {
        int b[] = new int[R], ans = 0;

        for (int j = 0; j < C; j++) {
            // Copying the column
            for (int i = 0; i < R; i++) {
                b[i] = ryt[i][j];
            }

            // Sort the copied array
            Arrays.sort(b);

            // Find maximum submatrix size.
            for (int i = 0; i < R; ++i) {
                ans = Math.max(ans, b[i] * (R - i));
            }
        }

        return ans;
    }

// Return maximum size submatrix with column
// swap allowed.
    static int solveColumnSwap(int dwn[][]) {
        int b[] = new int[C], ans = 0;

        for (int i = 0; i < R; ++i) {
            // Copying the row.
            for (int j = 0; j < C; ++j) {
                b[j] = dwn[i][j];
            }

            // Sort the copied array
            Arrays.sort(b);

            // Find maximum submatrix size.
            for (int k = 0; k < C; ++k) {
                ans = Math.max(ans, b[k] * (C - k));
            }
        }

        return ans;
    }

    static void findMax1s(int mat[][]) {
        int ryt[][] = new int[R + 2][C + 2], dwn[][] = new int[R + 2][C + 2];

        precompute(mat, ryt, dwn);

        // Solving for row swap and column swap
        int rswap = solveRowSwap(ryt);
        int cswap = solveColumnSwap(dwn);

        // Comparing both.
        if (rswap > cswap) {
            System.out.println("Row Swap\n" + rswap);
        } else {
            System.out.println("Column Swap\n" + cswap);
        }
    }

// Driven Program 
    public static void main(String[] args) {
        int mat[][] = {{0, 0, 0},
        {1, 1, 0},
        {1, 1, 0},
        {0, 0, 0},
        {1, 1, 0}};

        findMax1s(mat);
    }
}

/* This Java code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 program to find maximum binary
# sub-matrix with row swaps and column swaps.
R, C = 5, 3

# Precompute the number of consecutive 1 
# below the (i, j) in j-th column and the 
# number of consecutive 1s on right side 
# of (i, j) in i-th row.
def precompute(mat, ryt, dwn):

    # Travesing the 2d matrix from top-right.
    for j in range(C - 1, -1, -1):

        for i in range(0, R):

            # If (i,j) contain 0, do nothing
            if mat[i][j] == 0:
                ryt[i][j] = 0

            # Counting consecutive 1 on right side
            else:
                ryt[i][j] = ryt[i][j + 1] + 1

    # Travesing the 2d matrix from bottom-left.
    for i in range(R - 1, -1, -1):

        for j in range(0, C):

            # If (i,j) contain 0, do nothing
            if mat[i][j] == 0:
                dwn[i][j] = 0

            # Counting consecutive 1 down to (i,j).
            else:
                dwn[i][j] = dwn[i + 1][j] + 1

# Return maximum size submatrix 
# with row swap allowed.
def solveRowSwap(ryt):

    b = [0] * R
    ans = 0

    for j in range(0, C):

        # Copying the column
        for i in range(0, R):
            b[i] = ryt[i][j]

        # Sort the copied array
        b.sort()

        # Find maximum submatrix size.
        for i in range(0, R):
            ans = max(ans, b[i] * (R - i))

    return ans

# Return maximum size submatrix
# with column swap allowed.
def solveColumnSwap(dwn):

    b = [0] * C
    ans = 0

    for i in range(0, R):

        # Copying the row.
        for j in range(0, C):
            b[j] = dwn[i][j]

        # Sort the copied array
        b.sort()

        # Find maximum submatrix size.
        for i in range(0, C):
            ans = max(ans, b[i] * (C - i))

    return ans

def findMax1s(mat):

    ryt = [[0 for i in range(C + 2)] 
              for j in range(R + 2)]
    dwn = [[0 for i in range(C + 2)] 
              for j in range(R + 2)]

    precompute(mat, ryt, dwn)

    # Solving for row swap and column swap
    rswap = solveRowSwap(ryt)
    cswap = solveColumnSwap(dwn)

    # Comparing both.
    if rswap > cswap: print("Row Swap\n", rswap)
    else: print("Column Swap\n", cswap)

# Driver Code
if __name__ == "__main__":

    mat = [[0, 0, 0],
           [1, 1, 0],
           [1, 1, 0],
           [0, 0, 0],
           [1, 1, 0]] 

    findMax1s(mat)

# This code is contributed by Rituraj Jain
```

## C#

```

// C# program to find maximum binary sub-matrix
// with row swaps and column swaps.
using System;
public class GFG {

    static int R = 5;
    static int C = 3;

// Precompute the number of consecutive 1 below the
// (i, j) in j-th column and the number of consecutive 1s
// on right side of (i, j) in i-th row.
    static void precompute(int [,]mat, int [,]ryt,
            int [,]dwn) {
        // Travesing the 2d matrix from top-right.
        for (int j = C - 1; j >= 0; j--) {
            for (int i = 0; i < R; ++i) {
                // If (i,j) contain 0, do nothing
                if (mat[i,j] == 0) {
                    ryt[i,j] = 0;
                } // Counting consecutive 1 on right side
                else {
                    ryt[i,j] = ryt[i,j + 1] + 1;
                }
            }
        }

        // Travesing the 2d matrix from bottom-left.
        for (int i = R - 1; i >= 0; i--) {
            for (int j = 0; j < C; ++j) {
                // If (i,j) contain 0, do nothing
                if (mat[i,j] == 0) {
                    dwn[i,j] = 0;
                } // Counting consecutive 1 down to (i,j).
                else {
                    dwn[i,j] = dwn[i + 1,j] + 1;
                }
            }
        }
    }

// Return maximum size submatrix with row swap allowed.
    static int solveRowSwap(int [,]ryt) {
        int []b = new int[R]; int ans = 0;

        for (int j = 0; j < C; j++) {
            // Copying the column
            for (int i = 0; i < R; i++) {
                b[i] = ryt[i,j];
            }

            // Sort the copied array
            Array.Sort(b);

            // Find maximum submatrix size.
            for (int i = 0; i < R; ++i) {
                ans = Math.Max(ans, b[i] * (R - i));
            }
        }

        return ans;
    }

// Return maximum size submatrix with column
// swap allowed.
    static int solveColumnSwap(int [,]dwn) {
        int []b = new int[C];int ans = 0;

        for (int i = 0; i < R; ++i) {
            // Copying the row.
            for (int j = 0; j < C; ++j) {
                b[j] = dwn[i,j];
            }

            // Sort the copied array
            Array.Sort(b);

            // Find maximum submatrix size.
            for (int k = 0; k < C; ++k) {
                ans = Math.Max(ans, b[k] * (C - k));
            }
        }

        return ans;
    }

    static void findMax1s(int [,]mat) {
        int [,]ryt = new int[R + 2,C + 2];
        int [,]dwn = new int[R + 2,C + 2];

        precompute(mat, ryt, dwn);

        // Solving for row swap and column swap
        int rswap = solveRowSwap(ryt);
        int cswap = solveColumnSwap(dwn);

        // Comparing both.
        if (rswap > cswap) {
            Console.WriteLine("Row Swap\n" + rswap);
        } else {
            Console.WriteLine("Column Swap\n" + cswap);
        }
    }

// Driven Program 
    public static void Main() {
        int [,]mat = {{0, 0, 0},
        {1, 1, 0},
        {1, 1, 0},
        {0, 0, 0},
        {1, 1, 0}};

        findMax1s(mat);
    }
}

/* This C# code is contributed by PrinciRaj1992*/
```

**Output:**

```
Row Swap
6

```

本文由 **[Anuj Chauhan](https://www.facebook.com/anuj0503)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。