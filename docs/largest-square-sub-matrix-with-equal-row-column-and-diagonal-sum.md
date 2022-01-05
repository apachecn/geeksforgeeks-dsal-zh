# 行、列、对角线和相等的最大正方形子矩阵

> 原文:[https://www . geeksforgeeks . org/最大平方子矩阵等行列对角线和/](https://www.geeksforgeeks.org/largest-square-sub-matrix-with-equal-row-column-and-diagonal-sum/)

给定尺寸为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**，任务是[找到最大正方形子矩阵](https://www.geeksforgeeks.org/maximum-size-sub-matrix-with-all-1s-in-a-binary-matrix/)的大小，使得该子矩阵中所有行、列、对角线的和相等。

**示例:**

> **输入:** N = 3，M = 4，mat[][] = [[5，1，3，1]，[9，3，3，1]，[1，3，3，8]]
> **输出:** 2
> **说明:**
> 满足所有给定条件的子矩阵以粗体显示
> 5 1 3 1
> 9**3**1
> 1**3**
> 
> **输入:** N = 4，M = 5，mat[][] = [[7，1，4，5，6]，[2，5，1，6，4]，[1，5，4，3，2]，[1，2，7，3，4]]
> **输出:** 3
> **解释:**
> 满足所有给定条件的子矩阵以粗体显示
> 7 1 4 5 6
> 2 **5 1 6**

**方法:**给定的问题可以通过找到所有行和列的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决，然后从矩阵的每个单元迭代所有可能大小的正方形子矩阵，如果存在满足给定标准的任何这样的正方形矩阵，则打印该大小的正方形矩阵。按照以下步骤解决问题:

*   维护两个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **前缀行[]** 和**前缀列[]** ，分别存储给定矩阵的行和列的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-2d-array/)
*   执行以下步骤，检查从尺寸为 **K** 的单元格 **(i，j)** 开始的任何方形矩阵是否满足给定标准:
    1.  求子矩阵 mat[i][j]到 **mat[i + K][j + K]** 的主对角线的元素之和并存储在变量中，比如**之和**。
    2.  如果**和**的值与下面提到的值相同，则返回**真**。否则，退回**假**。
        *   所有行的前缀和，即 **k** 在当时范围**【I，I+K】**内的所有值的**前缀行[K][j+K]–前缀行[K][j]【T1]的值。**
        *   所有列的前缀和，即 **k** 的所有值在当时范围**【j，j+K】**内的**prefixSumColumn[I+K][j]–prefixSumColumn[I][K]【T1]值。**
        *   反对角元素的前缀和。
*   现在，[迭代可在范围**【min(N，M)，1】**上形成的正方形矩阵](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/)的所有可能尺寸，如果存在任何可能满足上述步骤中的给定标准，则打印该尺寸的正方形矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Define the prefix sum arrays globally
int prefix_sum_row[50][51];
int prefix_sum_col[51][50];

bool is_valid(int r, int c, int size,
              vector<vector<int> >& grid)
{
    int r_end = r + size, c_end = c + size;

    // Diagonal sum
    int sum = 0;
    for (int i = r, j = c; i < r_end; i++, j++) {
        sum += grid[i][j];
    }

    // Check each row
    for (int i = r; i < r_end; i++) {
        if (prefix_sum_row[i][c_end]
                - prefix_sum_row[i]
            != sum) {
            return false;
        }
    }

    // Check each column
    for (int i = c; i < c_end; i++) {
        if (prefix_sum_col[r_end][i]
                - prefix_sum_col[r][i]
            != sum) {
            return false;
        }
    }

    // Check anti-diagonal
    int ad_sum = 0;
    for (int i = r, j = c_end - 1; i < r_end;
         i++, j--) {
        ad_sum += grid[i][j];
    }

    return ad_sum == sum;
}

int largestSquareValidMatrix(
    vector<vector<int> >& grid)
{
    // Store the size of the given grid
    int m = grid.size(), n = grid[0].size();

    // Compute the prefix sum for the rows
    for (int i = 0; i < m; i++) {
        for (int j = 1; j <= n; j++) {
            prefix_sum_row[i][j]
                = prefix_sum_row[i][j - 1]
                  + grid[i][j - 1];
        }
    }

    // Compute the prefix sum for the columns
    for (int i = 1; i <= m; i++) {
        for (int j = 0; j < n; j++) {
            prefix_sum_col[i][j]
                = prefix_sum_col[i - 1][j]
                  + grid[i - 1][j];
        }
    }

    // Check for all possible square submatrix
    for (int size = min(m, n); size > 1; size--) {
        for (int i = 0; i <= m - size; i++) {
            for (int j = 0; j <= n - size; j++) {
                if (is_valid(i, j, size, grid)) {
                    return size;
                }
            }
        }
    }

    return 1;
}

// Driver Code
int main()
{
    vector<vector<int> > grid = { { 7, 1, 4, 5, 6 },
                                  { 2, 5, 1, 6, 4 },
                                  { 1, 5, 4, 3, 2 },
                                  { 1, 2, 7, 3, 4 } };
    cout << largestSquareValidMatrix(grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Define the prefix sum arrays globally
    public static int[][] prefix_sum_row = new int[50][51];
    public static int[][] prefix_sum_col = new int[51][50];

    public static boolean is_valid(int r, int c, int size, int[][] grid) {
        int r_end = r + size, c_end = c + size;

        // Diagonal sum
        int sum = 0;
        for (int i = r, j = c; i < r_end; i++, j++) {
            sum += grid[i][j];
        }

        // Check each row
        for (int i = r; i < r_end; i++) {
            if (prefix_sum_row[i][c_end] - prefix_sum_row[i] != sum) {
                return false;
            }
        }

        // Check each column
        for (int i = c; i < c_end; i++) {
            if (prefix_sum_col[r_end][i] - prefix_sum_col[r][i] != sum) {
                return false;
            }
        }

        // Check anti-diagonal
        int ad_sum = 0;
        for (int i = r, j = c_end - 1; i < r_end; i++, j--) {
            ad_sum += grid[i][j];
        }

        return ad_sum == sum;
    }

    public static int largestSquareValidMatrix(int[][] grid) {
        // Store the size of the given grid
        int m = grid.length, n = grid[0].length;

        // Compute the prefix sum for the rows
        for (int i = 0; i < m; i++) {
            for (int j = 1; j <= n; j++) {
                prefix_sum_row[i][j] = prefix_sum_row[i][j - 1] + grid[i][j - 1];
            }
        }

        // Compute the prefix sum for the columns
        for (int i = 1; i <= m; i++) {
            for (int j = 0; j < n; j++) {
                prefix_sum_col[i][j] = prefix_sum_col[i - 1][j] + grid[i - 1][j];
            }
        }

        // Check for all possible square submatrix
        for (int size = Math.min(m, n); size > 1; size--) {
            for (int i = 0; i <= m - size; i++) {
                for (int j = 0; j <= n - size; j++) {
                    if (is_valid(i, j, size, grid)) {
                        return size;
                    }
                }
            }
        }

        return 1;
    }

    // Driver Code
    public static void main(String args[]) {
        int[][] grid = { { 7, 1, 4, 5, 6 }, { 2, 5, 1, 6, 4 }, { 1, 5, 4, 3, 2 }, { 1, 2, 7, 3, 4 } };
        System.out.println(largestSquareValidMatrix(grid));

    }

}

// This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Define the prefix sum arrays globally
    public static int[,] prefix_sum_row = new int[50,51];
    public static int[,] prefix_sum_col = new int[51,50];

    public static bool is_valid(int r, int c, int size, int[,] grid) {
        int r_end = r + size, c_end = c + size;

        // Diagonal sum
        int sum = 0;
        for (int i = r, j = c; i < r_end; i++, j++) {
            sum += grid[i,j];
        }

        // Check each row
        for (int i = r; i < r_end; i++) {
            if (prefix_sum_row[i,c_end] - prefix_sum_row[i,c] != sum) {
                return false;
            }
        }

        // Check each column
        for (int i = c; i < c_end; i++) {
            if (prefix_sum_col[r_end,i] - prefix_sum_col[r,i] != sum) {
                return false;
            }
        }

        // Check anti-diagonal
        int ad_sum = 0;
        for (int i = r, j = c_end - 1; i < r_end; i++, j--) {
            ad_sum += grid[i,j];
        }

        return ad_sum == sum;
    }

    public static int largestSquareValidMatrix(int[,] grid) {
        // Store the size of the given grid
        int m = grid.GetLength(0), n = grid.GetLength(1);

        // Compute the prefix sum for the rows
        for (int i = 0; i < m; i++) {
            for (int j = 1; j <= n; j++) {
                prefix_sum_row[i,j] = prefix_sum_row[i,j - 1] + grid[i,j - 1];
            }
        }

        // Compute the prefix sum for the columns
        for (int i = 1; i <= m; i++) {
            for (int j = 0; j < n; j++) {
                prefix_sum_col[i,j] = prefix_sum_col[i - 1,j] + grid[i - 1,j];
            }
        }

        // Check for all possible square submatrix
        for (int size = Math.Min(m, n); size > 1; size--) {
            for (int i = 0; i <= m - size; i++) {
                for (int j = 0; j <= n - size; j++) {
                    if (is_valid(i, j, size, grid)) {
                        return size;
                    }
                }
            }
        }

        return 1;
    }

    // Driver Code
    public static void Main() {
        int[,] grid = { { 7, 1, 4, 5, 6 }, { 2, 5, 1, 6, 4 },
                       { 1, 5, 4, 3, 2 }, { 1, 2, 7, 3, 4 } };
        Console.WriteLine(largestSquareValidMatrix(grid));

    }

}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Define the prefix sum arrays globally
       let prefix_sum_row = new Array(50);
       for (let i = 0; i < prefix_sum_row.length; i++) {
           prefix_sum_row[i] = new Array(51).fill(0);
       }
       let prefix_sum_col = new Array(50);
       for (let i = 0; i < prefix_sum_col.length; i++) {
           prefix_sum_col[i] = new Array(51).fill(0);
       }
       function is_valid(r, c, size, grid) {
           let r_end = r + size, c_end = c + size;

           // Diagonal sum
           let sum = 0;
           for (let i = r, j = c; i < r_end; i++, j++) {
               sum += grid[i][j];
           }
           // Check each row
           for (let i = r; i < r_end; i++) {
               if (prefix_sum_row[i][c_end]
                   - prefix_sum_row[i]
                   != sum) {
                   return false;
               }
           }

           // Check each column
           for (let i = c; i < c_end; i++) {
               if (prefix_sum_col[r_end][i]
                   - prefix_sum_col[r][i]
                   != sum) {
                   return false;
               }
           }

           // Check anti-diagonal
           let ad_sum = 0;
           for (let i = r, j = c_end - 1; i < r_end;
               i++, j--) {
               ad_sum += grid[i][j];
           }

           return ad_sum == sum;
       }

       function largestSquareValidMatrix(grid) {
           // Store the size of the given grid
           let m = grid.length, n = grid[0].length;

           // Compute the prefix sum for the rows
           for (let i = 0; i < m; i++) {
               for (let j = 1; j <= n; j++) {
                   prefix_sum_row[i][j]
                       = prefix_sum_row[i][j - 1]
                       + grid[i][j - 1];
               }
           }

           // Compute the prefix sum for the columns
           for (let i = 1; i <= m; i++) {
               for (let j = 0; j < n; j++) {
                   prefix_sum_col[i][j]
                       = prefix_sum_col[i - 1][j]
                       + grid[i - 1][j];
               }
           }

           // Check for all possible square submatrix
           for (let size = Math.min(m, n); size > 1; size--) {
               for (let i = 0; i <= m - size; i++) {
                   for (let j = 0; j <= n - size; j++) {
                       if (is_valid(i, j, size, grid)) {
                           return size;
                       }
                   }
               }
           }

           return 1;
       }

       // Driver Code

       let grid = [[7, 1, 4, 5, 6],
       [2, 5, 1, 6, 4],
       [1, 5, 4, 3, 2],
       [1, 2, 7, 3, 4]];
       document.write(largestSquareValidMatrix(grid));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*M*min(N，M)<sup>2</sup>)*
*T8】辅助空间: O(N*M)*