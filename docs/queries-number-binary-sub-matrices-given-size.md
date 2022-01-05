# 对给定大小的二进制子矩阵数量的查询

> 原文:[https://www . geesforgeks . org/query-number-binary-sub-matrix-给定-size/](https://www.geeksforgeeks.org/queries-number-binary-sub-matrices-given-size/)

给定一个大小为 **N X M** 的二进制矩阵，任务是回答以下类型的 **Q** 查询；

> 查询(a，b):找到大小为 **a X a** 的子矩阵的数量，其每个元素由二进制数 **b** 组成。

我们基本上需要找到给定大小的全 1 或全 0 的子矩阵。

**示例:**

```
Input : N = 5, M = 4
        m[][] = { { 0, 0, 1, 1 },
                  { 0, 0, 1, 0 },
                  { 0, 1, 1, 1 },
                  { 1, 1, 1, 1 },
                  { 0, 1, 1, 1 }
                }
        Q = 2
        Query 1 : a = 2, b = 1
        Query 2 : a = 2, b = 0 
Output : 4 1

Explanation:
For Query 1,
0011  0011  0011  0011
0010  0010  0010  0010
0111  0111  0111  0111
1111  1111  1111  1111
0111  0111  0111  0111

For Query 2,
0011
0010
0111
1111
0111

Input : N = 5, M = 4
        m[][] = { { 0, 0, 1, 1 },
                  { 0, 0, 1, 0 },
                  { 0, 1, 1, 1 },
                  { 1, 1, 1, 1 },
                  { 0, 1, 1, 1 }
                }

        Q = 1
        Query 1 : a = 3, b = 1
Output : 1
```

思路是用**动态规划**解决问题。首先声明一个 2D 数组 **dp[][]** ，其中 dp[i][j]处的值(比如 K)表示可以形成的最大正方形子矩阵(K X K)的大小，其所有元素等于 m[i][j]，并且(I，j)是子矩阵的最后一个元素(东南)。现在，dp[i][j]可以定义为:

> 1) **如果 i = 0 OR j = 0** 在这种情况下，dp[i][j] = 1，因为只有 1 X 1 是唯一可以在第 0 行或第 0 列形成的方阵，其所有元素都等于
> 到 m[i][j]，最后一个元素是(I，0)或(0，j)。
> 2) **如果 m[i][j]= m[i-1][j]= m[i][j-1]= m[i-1][j-1]**DP[I][j]= min(DP[I][j-1]、dp[i-1][j]、dp[i-1][j-1]) + 1，如果 m[I][j]处的二进制数等于 m[I-1][j]、m[I-1][j-1]和 m[I]处的二进制数因为如果当前二进制数等于所有三个二进制数，它将形成一个所有元素都相等的 2×2 平方子矩阵。此外，它将在位置 m[i-1][j]、m[i-1][j-1]和 m[i][j-1]处为正方形矩阵贡献 1 行和 1 列所有相等的元素。
> dp[i][j] = 1，如果上述条件不满足，因为单个单元将总是贡献 1×1 子矩阵。

现在，遍历 2D dp[][]数组，计算所有不同值的频率(元素 0 的 freq0[]，元素 1 的 freq1[])，即 0 和 1 的正方形子矩阵的不同大小。

注意，要计算大小为 Y X Y 的正方形子矩阵，那么 Y+1 X Y+1 也将贡献 1 个计数。假设我们需要计算 2 X 2 矩阵和 dp[][]=

```
...22
...23
```

这里，2 的频率是 3，但是观察元素，其中 dp[i][j] = 3 也贡献了 2×2 平方子矩阵。
所以，求 freq0[]和 freq1[]的频率的累计和。

下面是该方法的实现:

## C++

```
// CPP Program to answer queries on number of
// submatrix of given size
#include <bits/stdc++.h>
using namespace std;

#define MAX 100
#define N 5
#define M 4

// Return the minimum of three numbers
int min(int a, int b, int c)
{
    return min(a, min(b, c));
}

// Solve each query on matrix
void solveQuery(int n, int m, int mat[N][M], int q,
                             int a[], int binary[])
{
    int dp[n][m], max = 1;

    // For each of the cell.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // finding submatrix size of oth row
            // and column.
            if (i == 0 || j == 0)
                dp[i][j] = 1;

            // intermediate cells.
            else if ((mat[i][j] == mat[i - 1][j]) &&
                     (mat[i][j] == mat[i][j - 1]) &&
                     (mat[i][j] == mat[i - 1][j - 1])) {

                dp[i][j] = min(dp[i - 1][j], dp[i - 1][j - 1],
                               dp[i][j - 1])
                           + 1;

                if (max < dp[i][j])
                    max = dp[i][j];
            }

            else
                dp[i][j] = 1;
        }
    }

    int freq0[MAX] = { 0 }, freq1[MAX] = { 0 };

    // Find frequency of each distinct size
    // for 0s and 1s.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (mat[i][j] == 0)
                freq0[dp[i][j]]++;
            else
                freq1[dp[i][j]]++;
        }
    }

    // Find the Cumulative Sum.
    for (int i = max - 1; i >= 0; i--) {
        freq0[i] += freq0[i + 1];
        freq1[i] += freq1[i + 1];
    }

    // Output the answer for each query
    for (int i = 0; i < q; i++) {
        if (binary[i] == 0)
            cout << freq0[a[i]] << endl;
        else
            cout << freq1[a[i]] << endl;
    }
}

// Driver Program
int main()
{
    int n = 5, m = 4;
    int mat[N][M] = {
        { 0, 0, 1, 1 },
        { 0, 0, 1, 0 },
        { 0, 1, 1, 1 },
        { 1, 1, 1, 1 },
        { 0, 1, 1, 1 }
    };
    int q = 2;
    int a[] = { 2, 2 };
    int binary[] = { 1, 0 };

    solveQuery(n, m, mat, q, a, binary);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to answer queries on number of
// submatrix of given size
import java.io.*;

class GFG {

    static int MAX = 100;
    static int N = 5;
    static int M = 4;

    // Return the minimum of three numbers
    static int min(int a, int b, int c)
    {
        return Math.min(a, Math.min(b, c));
    }

    // Solve each query on matrix
    static void solveQuery(int n, int m, int mat[][],
                        int q, int a[], int binary[])
    {
        int dp[][] = new int[n][m];
        int max = 1;

        // For each of the cell.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // finding submatrix size of oth row
                // and column.
                if (i == 0 || j == 0)
                    dp[i][j] = 1;

                // intermediate cells.
                else if ((mat[i][j] == mat[i - 1][j])
                      && (mat[i][j] == mat[i][j - 1])
                 && (mat[i][j] == mat[i - 1][j - 1]))
                 {

                    dp[i][j] = min(dp[i - 1][j],
                               dp[i - 1][j - 1],
                                dp[i][j - 1]) + 1;

                    if (max < dp[i][j])
                        max = dp[i][j];
                }

                else
                    dp[i][j] = 1;
            }
        }

        int freq0[] = new int[MAX];
        int freq1[] = new int[MAX];

        // Find frequency of each distinct size
        // for 0s and 1s.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (mat[i][j] == 0)
                    freq0[dp[i][j]]++;
                else
                    freq1[dp[i][j]]++;
            }
        }

        // Find the Cumulative Sum.
        for (int i = max - 1; i >= 0; i--) {
            freq0[i] += freq0[i + 1];
            freq1[i] += freq1[i + 1];
        }

        // Output the answer for each query
        for (int i = 0; i < q; i++) {
            if (binary[i] == 0)
                System.out.println( freq0[a[i]]);
            else
                System.out.println( freq1[a[i]]);
        }
    }

    // Driver Program

    public static void main (String[] args)
    {
        int n = 5, m = 4;
        int mat[][] = { { 0, 0, 1, 1 },
                        { 0, 0, 1, 0 },
                        { 0, 1, 1, 1 },
                        { 1, 1, 1, 1 },
                        { 0, 1, 1, 1 } };
        int q = 2;
        int a[] = { 2, 2 };
        int binary[] = { 1, 0 };

        solveQuery(n, m, mat, q, a, binary);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to answer queries on number of
# submatrix of given size
MAX = 100
N = 5
M = 4

# Solve each query on matrix
def solveQuery(n, m, mat, q,
               a, binary):

    dp = [[0 for x in range(m)]for y in range(n)]
    max = 1

    # For each of the cell.
    for i in range(n):
        for j in range(m):

            # finding submatrix size of oth row
            # and column.
            if (i == 0 or j == 0):
                dp[i][j] = 1

            # intermediate cells.
            elif ((mat[i][j] == mat[i - 1][j]) and
                  (mat[i][j] == mat[i][j - 1]) and
                  (mat[i][j] == mat[i - 1][j - 1])):

                dp[i][j] = (min(dp[i - 1][j], min(dp[i - 1][j - 1],
                                                  dp[i][j - 1])) + 1)

                if (max < dp[i][j]):
                    max = dp[i][j]

            else:
                dp[i][j] = 1

    freq0 = [0] * MAX
    freq1 = [0] * MAX

    # Find frequency of each distinct size
    # for 0s and 1s.
    for i in range(n):
        for j in range(m):
            if (mat[i][j] == 0):
                freq0[dp[i][j]] += 1
            else:
                freq1[dp[i][j]] += 1

    # Find the Cumulative Sum.
    for i in range(max - 1, -1, -1):
        freq0[i] += freq0[i + 1]
        freq1[i] += freq1[i + 1]

    # Output the answer for each query
    for i in range(q):
        if (binary[i] == 0):
            print(freq0[a[i]])
        else:
            print(freq1[a[i]])

# Driver Program
if __name__ == "__main__":

    n = 5
    m = 4
    mat = [
        [0, 0, 1, 1],
        [0, 0, 1, 0],
        [0, 1, 1, 1],
        [1, 1, 1, 1],
        [0, 1, 1, 1]
    ]
    q = 2
    a = [2, 2]
    binary = [1, 0]

    solveQuery(n, m, mat, q, a, binary)

    # This code is contributed by ukasp.
```

## C#

```
// C# Program to answer
// queries on number of
// submatrix of given size
using System;

class GFG
{
    static int MAX = 100;
    // static int N = 5;
    // static int M = 4;

    // Return the minimum
    // of three numbers
    static int min(int a,
                   int b,
                   int c)
    {
        return Math.Min(a, Math.Min(b, c));
    }

    // Solve each query on matrix
    static void solveQuery(int n, int m,
                           int [,]mat, int q,
                           int []a, int []binary)
    {
        int [,]dp = new int[n, m];
        int max = 1;

        // For each of the cell.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // finding submatrix size
                // of oth row and column.
                if (i == 0 || j == 0)
                    dp[i, j] = 1;

                // intermediate cells.
                else if ((mat[i, j] == mat[i - 1, j]) &&
                         (mat[i, j] == mat[i, j - 1]) &&
                         (mat[i, j] == mat[i - 1, j - 1]))
                {

                    dp[i, j] = min(dp[i - 1, j],
                                   dp[i - 1, j - 1],
                                   dp[i, j - 1]) + 1;

                    if (max < dp[i, j])
                        max = dp[i, j];
                }

                else
                    dp[i, j] = 1;
            }
        }

        int []freq0 = new int[MAX];
        int []freq1 = new int[MAX];

        // Find frequency of each
        // distinct size for 0s and 1s.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (mat[i, j] == 0)
                    freq0[dp[i, j]]++;
                else
                    freq1[dp[i, j]]++;
            }
        }

        // Find the Cumulative Sum.
        for (int i = max - 1; i >= 0; i--)
        {
            freq0[i] += freq0[i + 1];
            freq1[i] += freq1[i + 1];
        }

        // Output the answer
        // for each query
        for (int i = 0; i < q; i++)
        {
            if (binary[i] == 0)
                Console.WriteLine(freq0[a[i]]);
            else
                Console.WriteLine(freq1[a[i]]);
        }
    }

    // Driver Code
    public static void Main ()
    {
        int n = 5, m = 4;
        int [,]mat = {{0, 0, 1, 1},
                      {0, 0, 1, 0},
                      {0, 1, 1, 1},
                      {1, 1, 1, 1},
                      {0, 1, 1, 1}};
        int q = 2;
        int []a = {2, 2};
        int []binary = {1, 0};

        solveQuery(n, m, mat,
                   q, a, binary);
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>

// Javascript Program to answer queries on number of
// submatrix of given size

var MAX = 100
var N = 5
var M = 4

// Return the minimum of three numbers
function min(a, b, c)
{
    return Math.min(a, Math.min(b, c));
}

// Solve each query on matrix
function solveQuery(n, m, mat, q, a, binary)
{
    var dp = Array.from(Array(n),()=>Array(m));
    var max = 1;

    // For each of the cell.
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {

            // finding submatrix size of oth row
            // and column.
            if (i == 0 || j == 0)
                dp[i][j] = 1;

            // intermediate cells.
            else if ((mat[i][j] == mat[i - 1][j]) &&
                     (mat[i][j] == mat[i][j - 1]) &&
                     (mat[i][j] == mat[i - 1][j - 1])) {

                dp[i][j] = Math.min(dp[i - 1][j], dp[i - 1][j - 1],
                               dp[i][j - 1])
                           + 1;

                if (max < dp[i][j])
                    max = dp[i][j];
            }

            else
                dp[i][j] = 1;
        }
    }

    var freq0 = Array(MAX).fill(0);
    var freq1 = Array(MAX).fill(0);

    // Find frequency of each distinct size
    // for 0s and 1s.
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {
            if (mat[i][j] == 0)
                freq0[dp[i][j]]++;
            else
                freq1[dp[i][j]]++;
        }
    }

    // Find the Cumulative Sum.
    for (var i = max - 1; i >= 0; i--) {
        freq0[i] += freq0[i + 1];
        freq1[i] += freq1[i + 1];
    }

    // Output the answer for each query
    for (var i = 0; i < q; i++) {
        if (binary[i] == 0)
            document.write( freq0[a[i]] + "<br>");
        else
            document.write( freq1[a[i]] + "<br>") ;
    }
}

// Driver Program
var n = 5, m = 4;
var mat = [
    [ 0, 0, 1, 1 ],
    [ 0, 0, 1, 0 ],
    [ 0, 1, 1, 1 ],
    [ 1, 1, 1, 1 ],
    [ 0, 1, 1, 1 ]
];
var q = 2;
var a = [ 2, 2 ];
var binary = [ 1, 0 ];
solveQuery(n, m, mat, q, a, binary);

</script>
```

**Output:** 

```
4
1
```

上述算法的时间复杂度为 **O(n * m)**