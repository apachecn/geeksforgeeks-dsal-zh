# 仅用 0 填充二进制子矩阵所需的最小翻转计数查询

> 原文:[https://www . geesforgeks . org/query-to-count-minimum-flips-required-to-fill-a-binary-submatrix-with-0s-only/](https://www.geeksforgeeks.org/queries-to-count-minimum-flips-required-to-fill-a-binary-submatrix-with-0s-only/)

给定一个大小为 **M * N** 和 **Q** 的 **{pi，pj，qi，qj}** 形式的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/) **mat[][]** ，每个查询的任务是统计子矩阵中从单元格 **(pi，pj)** 到 **(qi，qj)** 的 **0** s 的数量。

**示例:**

> **输入:** mat[][] = {{0，1，0，1，1，0}，{1，0，1，1，0，1}，{1，1，0，0，1，1，1，0}，{1，1，1，1，1，0，1}，{0，0，1，0，1，1，1}，{1，1，0，1，0，1 }，Q[] = {{0，1，3，2}，{ 2 }
> 从索引(2，2)到(4，5)的子矩阵包含 4 个 0。
> 从索引(4，3)到(5，6)的子矩阵包含 2 个 0。
> 
> **输入:** mat[][] = {{0，1，0}，{1，0，1}}，Q[] = {{0，0，2，2}}
> **输出:** 3

**天真方法:**解决问题最简单的方法是通过迭代子矩阵计算每个查询的 **0** 的个数，并打印每个查询的个数。

***时间复杂度:**O(M * N * Q)*
T5**辅助空间:** O(1)

**高效方法:**为了优化上述方法，思路是对给定矩阵 **mat[][]** 进行预处理。创建一个计数矩阵，比如说**前缀【M】【N】**，这样**前缀 _ CNT【I】【j】**在索引 **(0，0)** 到 **(i，j)** 内的子矩阵中存储 **0** s 的计数。按照以下步骤计算**前缀[][]** :

*   如果 **mat[i][j]** 为 **0** ，则用 **1** 初始化**前缀【I][j】**。否则，用 **0** 初始化。
*   找到每行每列的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，并相应更新矩阵。

一旦计算出矩阵**prefixcont[][]**，任何子矩阵中的 **0s** 的计数可以在 ***O(1)时间*** 中计算。下面是计算从 **(pi，pj)** 到 **(qi，qj)** 的每个子矩阵中 **0s** 的表达式，可以计算为:

> cnt =前缀[qi][QJ]-CNT 前缀[pi-1][QJ]-CNT 前缀[qi][pj-1]+CNT 前缀[pi-1][pj-1]

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define M 6
#define N 7

// Function to compute the matrix
// prefixCnt[M][N] from mat[M][N] such
// that prefixCnt[i][j] stores the
// count of 0's from (0, 0) to (i, j)
void preCompute(int mat[M][N],
                int prefixCnt[M][N])
{
    for (int i = 0; i < M; i++) {

        for (int j = 0; j < N; j++) {

            // Initialize prefixCnt[i][j]
            // with 1 if mat[i][j] is 0
            if (mat[i][j] == 0) {
                prefixCnt[i][j] = 1;
            }

            // Otherwise, assign with 0
            else {
                prefixCnt[i][j] = 0;
            }
        }
    }

    // Calculate prefix sum for each row
    for (int i = 0; i < M; i++)
        for (int j = 1; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i][j - 1];

    // Calculate prefix sum for each column
    for (int i = 1; i < M; i++)
        for (int j = 0; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i - 1][j];
}

// Function to compute count of 0's
// in submatrix from (pi, pj) to
// (qi, qj) from prefixCnt[M][N]
int countQuery(int prefixCnt[M][N],
               int pi, int pj,
               int qi, int qj)
{
    // Initialize that count of 0's
    // in the sub-matrix within
    // indices (0, 0) to (qi, qj)
    int cnt = prefixCnt[qi][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (pi-1, qj)
    if (pi > 0)
        cnt -= prefixCnt[pi - 1][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (qi, pj-1)
    if (pj > 0)
        cnt -= prefixCnt[qi][pj - 1];

    // Add prefixCnt[pi - 1][pj - 1]
    // because its value has been added
    // once but subtracted twice
    if (pi > 0 && pj > 0)
        cnt += prefixCnt[pi - 1][pj - 1];

    return cnt;
}

// Function to count the 0s in the
// each given submatrix
void count0s(int mat[M][N], int Q[][4],
             int sizeQ)
{

    // Stores the prefix sum of each
    // row and column
    int prefixCnt[M][N];

    // Compute matrix prefixCnt[][]
    preCompute(mat, prefixCnt);

    for (int i = 0; i < sizeQ; i++) {

        // Function Call for each query
        cout << countQuery(prefixCnt, Q[i][0],
                           Q[i][1], Q[i][2],
                           Q[i][3])
             << ' ';
    }
}

// Driver Code
int main()
{
    // Given matrix
    int mat[M][N] = {
        { 0, 1, 0, 1, 1, 1, 0 },
        { 1, 0, 1, 1, 1, 0, 1 },
        { 1, 1, 0, 0, 1, 1, 0 },
        { 1, 1, 1, 1, 1, 0, 1 },
        { 0, 0, 1, 0, 1, 1, 1 },
        { 1, 1, 0, 1, 1, 0, 1 }
    };

    int Q[][4] = { { 0, 1, 3, 2 },
                   { 2, 2, 4, 5 },
                   { 4, 3, 5, 6 } };

    int sizeQ = sizeof(Q) / sizeof(Q[0]);

    // Function Call
    count0s(mat, Q, sizeQ);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

final static int M = 6;
final static int N  = 7;

// Function to compute the matrix
// prefixCnt[M][N] from mat[M][N] such
// that prefixCnt[i][j] stores the
// count of 0's from (0, 0) to (i, j)
static void preCompute(int mat[][], int prefixCnt[][])
{
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Initialize prefixCnt[i][j]
            // with 1 if mat[i][j] is 0
            if (mat[i][j] == 0)
            {
                prefixCnt[i][j] = 1;
            }

            // Otherwise, assign with 0
            else
            {
                prefixCnt[i][j] = 0;
            }
        }
    }

    // Calculate prefix sum for each row
    for(int i = 0; i < M; i++)
        for(int j = 1; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i][j - 1];

    // Calculate prefix sum for each column
    for(int i = 1; i < M; i++)
        for(int j = 0; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i - 1][j];
}

// Function to compute count of 0's
// in submatrix from (pi, pj) to
// (qi, qj) from prefixCnt[M][N]
static int countQuery(int prefixCnt[][],
                      int pi, int pj,
                      int qi, int qj)
{

    // Initialize that count of 0's
    // in the sub-matrix within
    // indices (0, 0) to (qi, qj)
    int cnt = prefixCnt[qi][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (pi-1, qj)
    if (pi > 0)
        cnt -= prefixCnt[pi - 1][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (qi, pj-1)
    if (pj > 0)
        cnt -= prefixCnt[qi][pj - 1];

    // Add prefixCnt[pi - 1][pj - 1]
    // because its value has been added;
    // once but subtracted twice
    if (pi > 0 && pj > 0)
        cnt += prefixCnt[pi - 1][pj - 1];

    return cnt;
}

// Function to count the 0s in the
// each given submatrix
static void count0s(int mat[][], int Q[][],
                    int sizeQ)
{

    // Stores the prefix sum of each
    // row and column
    int prefixCnt[][] = new int[M][N];

    // Compute matrix prefixCnt[][]
    preCompute(mat, prefixCnt);

    for(int i = 0; i < sizeQ; i++)
    {

        // Function Call for each query
        System.out.print(countQuery(prefixCnt, Q[i][0],
                                               Q[i][1],
                                               Q[i][2],
                                               Q[i][3]) + " ");
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given matrix
    int mat[][] = { { 0, 1, 0, 1, 1, 1, 0 },
                    { 1, 0, 1, 1, 1, 0, 1 },
                    { 1, 1, 0, 0, 1, 1, 0 },
                    { 1, 1, 1, 1, 1, 0, 1 },
                    { 0, 0, 1, 0, 1, 1, 1 },
                    { 1, 1, 0, 1, 1, 0, 1 } };

    int Q[][] = { { 0, 1, 3, 2 },
                  { 2, 2, 4, 5 },
                  { 4, 3, 5, 6 } };

    int sizeQ = Q.length;

    // Function Call
    count0s(mat, Q, sizeQ);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

M = 6
N = 7

# Function to compute the matrix
# prefixCnt[M][N] from mat[M][N] such
# that prefixCnt[i][j] stores the
# count of 0's from (0, 0) to (i, j)
def preCompute(mat, prefixCnt):
    for i in range(M):

        for j in range(N):

            # Initialize prefixCnt[i][j]
            # with 1 if mat[i][j] is 0
            if (mat[i][j] == 0):
                prefixCnt[i][j] = 1

            # Otherwise, assign with 0
            else:
                prefixCnt[i][j] = 0

    # Calculate prefix sum for each row
    for i in range(M):
        for j in range(1, N):
            prefixCnt[i][j] += prefixCnt[i][j - 1]

    # Calculate prefix sum for each column
    for i in range(1, M):
        for j in range(N):
            prefixCnt[i][j] += prefixCnt[i - 1][j]
    return prefixCnt

# Function to compute count of 0's
# in submatrix from (pi, pj) to
# (qi, qj) from prefixCnt[M][N]
def countQuery(prefixCnt, pi, pj, qi, qj):

    # Initialize that count of 0's
    # in the sub-matrix within
    # indices (0, 0) to (qi, qj)
    cnt = prefixCnt[qi][qj]

    # Subtract count of 0's within
    # indices (0, 0) and (pi-1, qj)
    if (pi > 0):
        cnt -= prefixCnt[pi - 1][qj]

    # Subtract count of 0's within
    # indices (0, 0) and (qi, pj-1)
    if (pj > 0):
        cnt -= prefixCnt[qi][pj - 1]

    # Add prefixCnt[pi - 1][pj - 1]
    # because its value has been added
    # once but subtracted twice
    if (pi > 0 and pj > 0):
        cnt += prefixCnt[pi - 1][pj - 1]

    return cnt

# Function to count the 0s in the
# each given submatrix
def count0s(mat, Q, sizeQ):

    # Stores the prefix sum of each
    # row and column
    prefixCnt = [[ 0 for i in range(N)] for i in range(M)]

    # Compute matrix prefixCnt[][]
    prefixCnt = preCompute(mat, prefixCnt)

    for i in range(sizeQ):

        # Function Call for each query
        print(countQuery(prefixCnt, Q[i][0], Q[i][1], Q[i][2], Q[i][3]), end=" ")

# Driver Code
if __name__ == '__main__':

    # Given matrix
    mat = [[ 0, 1, 0, 1, 1, 1, 0 ],
        [ 1, 0, 1, 1, 1, 0, 1 ],
        [ 1, 1, 0, 0, 1, 1, 0 ],
        [ 1, 1, 1, 1, 1, 0, 1 ],
        [ 0, 0, 1, 0, 1, 1, 1 ],
        [ 1, 1, 0, 1, 1, 0, 1 ] ]

    Q= [ [ 0, 1, 3, 2 ],
        [ 2, 2, 4, 5 ],
        [ 4, 3, 5, 6 ] ]

    sizeQ = len(Q)

    # Function Call
    count0s(mat, Q, sizeQ)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

static int M = 6;
static int N  = 7;

// Function to compute the matrix
// prefixCnt[M][N] from mat[M][N] such
// that prefixCnt[i][j] stores the
// count of 0's from (0, 0) to (i, j)
static void preCompute(int [,]mat, int [,]prefixCnt)
{
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Initialize prefixCnt[i][j]
            // with 1 if mat[i,j] is 0
            if (mat[i, j] == 0)
            {
                prefixCnt[i, j] = 1;
            }

            // Otherwise, assign with 0
            else
            {
                prefixCnt[i, j] = 0;
            }
        }
    }

    // Calculate prefix sum for each row
    for(int i = 0; i < M; i++)
        for(int j = 1; j < N; j++)
            prefixCnt[i, j] += prefixCnt[i, j - 1];

    // Calculate prefix sum for each column
    for(int i = 1; i < M; i++)
        for(int j = 0; j < N; j++)
            prefixCnt[i, j] += prefixCnt[i - 1, j];
}

// Function to compute count of 0's
// in submatrix from (pi, pj) to
// (qi, qj) from prefixCnt[M][N]
static int countQuery(int [,]prefixCnt,
                      int pi, int pj,
                      int qi, int qj)
{

    // Initialize that count of 0's
    // in the sub-matrix within
    // indices (0, 0) to (qi, qj)
    int cnt = prefixCnt[qi, qj];

    // Subtract count of 0's within
    // indices (0, 0) and (pi-1, qj)
    if (pi > 0)
        cnt -= prefixCnt[pi - 1, qj];

    // Subtract count of 0's within
    // indices (0, 0) and (qi, pj-1)
    if (pj > 0)
        cnt -= prefixCnt[qi, pj - 1];

    // Add prefixCnt[pi - 1][pj - 1]
    // because its value has been added;
    // once but subtracted twice
    if (pi > 0 && pj > 0)
        cnt += prefixCnt[pi - 1, pj - 1];

    return cnt;
}

// Function to count the 0s in the
// each given submatrix
static void count0s(int [,]mat, int [,]Q,
                    int sizeQ)
{

    // Stores the prefix sum of each
    // row and column
    int [,]prefixCnt = new int[M, N];

    // Compute matrix prefixCnt[,]
    preCompute(mat, prefixCnt);

    for(int i = 0; i < sizeQ; i++)
    {

        // Function Call for each query
        Console.Write(countQuery(prefixCnt, Q[i, 0],
                                               Q[i, 1],
                                               Q[i, 2],
                                               Q[i, 3]) + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given matrix
    int [,]mat = { { 0, 1, 0, 1, 1, 1, 0 },
                    { 1, 0, 1, 1, 1, 0, 1 },
                    { 1, 1, 0, 0, 1, 1, 0 },
                    { 1, 1, 1, 1, 1, 0, 1 },
                    { 0, 0, 1, 0, 1, 1, 1 },
                    { 1, 1, 0, 1, 1, 0, 1 } };

    int [,]Q = { { 0, 1, 3, 2 },
                  { 2, 2, 4, 5 },
                  { 4, 3, 5, 6 } };

    int sizeQ = Q.GetLength(0);

    // Function Call
    count0s(mat, Q, sizeQ);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// javascript program of the above approach

let M = 6;
let N  = 7;

// Function to compute the matrix
// prefixCnt[M][N] from mat[M][N] such
// that prefixCnt[i][j] stores the
// count of 0's from (0, 0) to (i, j)
function preCompute(mat, prefixCnt)
{
    for(let i = 0; i < M; i++)
    {
        for(let j = 0; j < N; j++)
        {

            // Initialize prefixCnt[i][j]
            // with 1 if mat[i][j] is 0
            if (mat[i][j] == 0)
            {
                prefixCnt[i][j] = 1;
            }

            // Otherwise, assign with 0
            else
            {
                prefixCnt[i][j] = 0;
            }
        }
    }

    // Calculate prefix sum for each row
    for(let i = 0; i < M; i++)
        for(let j = 1; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i][j - 1];

    // Calculate prefix sum for each column
    for(let i = 1; i < M; i++)
        for(let j = 0; j < N; j++)
            prefixCnt[i][j] += prefixCnt[i - 1][j];
}

// Function to compute count of 0's
// in submatrix from (pi, pj) to
// (qi, qj) from prefixCnt[M][N]
function countQuery(prefixCnt,
                      pi, pj,
                      qi, qj)
{

    // Initialize that count of 0's
    // in the sub-matrix within
    // indices (0, 0) to (qi, qj)
    let cnt = prefixCnt[qi][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (pi-1, qj)
    if (pi > 0)
        cnt -= prefixCnt[pi - 1][qj];

    // Subtract count of 0's within
    // indices (0, 0) and (qi, pj-1)
    if (pj > 0)
        cnt -= prefixCnt[qi][pj - 1];

    // Add prefixCnt[pi - 1][pj - 1]
    // because its value has been added;
    // once but subtracted twice
    if (pi > 0 && pj > 0)
        cnt += prefixCnt[pi - 1][pj - 1];

    return cnt;
}

// Function to count the 0s in the
// each given submatrix
function count0s(mat, Q,
                    sizeQ)
{

    // Stores the prefix sum of each
    // row and column
    let prefixCnt = new Array(M);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < prefixCnt.length; i++) {
        prefixCnt[i] = new Array(2);
    }

    // Compute matrix prefixCnt[][]
    preCompute(mat, prefixCnt);

    for(let i = 0; i < sizeQ; i++)
    {

        // Function Call for each query
        document.write(countQuery(prefixCnt, Q[i][0],
                                               Q[i][1],
                                               Q[i][2],
                                               Q[i][3]) + " ");
    }
}

    // Driver Code

     // Given matrix
    let mat = [[ 0, 1, 0, 1, 1, 1, 0 ],
                    [ 1, 0, 1, 1, 1, 0, 1 ],
                    [ 1, 1, 0, 0, 1, 1, 0 ],
                    [ 1, 1, 1, 1, 1, 0, 1 ],
                    [ 0, 0, 1, 0, 1, 1, 1 ],
                    [ 1, 1, 0, 1, 1, 0, 1 ]];

    let Q = [[ 0, 1, 3, 2 ],
                  [ 2, 2, 4, 5 ],
                  [ 4, 3, 5, 6 ]];

    let sizeQ = Q.length;

    // Function Call
    count0s(mat, Q, sizeQ);

// This code is contributed by target_2.
</script>
```

**Output:** 

```
3 4 2
```

***时间复杂度:**O(M * N+Q)*
T5**辅助空间:** O(M*N)