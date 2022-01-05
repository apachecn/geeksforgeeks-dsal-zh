# 给定矩阵左上第 Kth 条对角线

> 原文:[https://www . geeksforgeeks . org/kth-从给定矩阵的左上角开始对角化/](https://www.geeksforgeeks.org/kth-diagonal-from-the-top-left-of-a-given-matrix/)

给定一个 **N * N** 维度的平方矩阵 **M[ ][ ]** ，任务是找到矩阵的 **K <sup>第</sup>** 条对角线，从**左上角**开始向**右下角**移动，并打印其内容。
**示例:**

> **输入:** N = 3，K = 2，M[ ][ ] = {{4，7，8}，{9，2，3}，{0，4，1}
> **输出:** 9 7
> **说明:**
> 给定矩阵从左上角到右下角的 5 条可能对角线为:
> 1 - > {4}
> 2 - > {9，7}
> 3 - >
> **输入:** N = 2，K = 2，M[ ][ ] = {1，5}，{9，4}}
> **输出:** 1
> **解释:**
> 对于给定矩阵，从左下到右上开始的 3 种可能对角线为:
> 1 - > {1}
> 2 - > {9，5}
> 3 - > {4}

**天真方法:**
解决这个问题最简单的方法是从给定矩阵的左上角到右下角生成所有对角线。生成第 K <sup>条</sup>对角线后，打印其内容。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
**高效途径:**
以上途径可以通过避免遍历矩阵来优化。相反，找到 **K <sup>第</sup>** 对角线的边界，即左下和右上索引。获得这些索引后，只需遍历对角线的索引即可打印所需的对角线。
需要以下观察来找到对角线的位置:

> 如果**((K–1)<N)**:对角线为上对角线
> 左下边界=**M【K–1】【0】**
> 右上边界=**M【0】【K–1】**
> 如果 **(K？N)** :对角线为下对角线。
> 左下边界= **M[N-1][K-N]**
> 右上边界= **M[K-N][N-1]**

按照以下步骤解决问题:

*   如果**(K–1)**<**N**，设置起始行，**起始行**为**K–1**，列，**起始列**为 **0** 。
*   否则，将 **startRow** 设置为**N–1**， **startCol** 设置为**K–N**。
*   最后从**M【startRow】【startCol】**开始打印对角线的元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns required diagonal
void printDiagonal(int K, int N,
                vector<vector<int> >& M)
{
    int startrow, startcol;

    // Initialize values to
    // print upper diagonals
    if (K - 1 < N) {
        startrow = K - 1;
        startcol = 0;
    }

    // Initialize values to
    // print lower diagonals
    else {
        startrow = N - 1;
        startcol = K - N;
    }

    // Traverse the diagonal
    for (; startrow >= 0 && startcol < N;
        startrow--, startcol++) {

        // Print its contents
        cout << M[startrow][startcol]
            << " ";
    }
}

// Driver Code
int main()
{
    int N = 3, K = 4;
    vector<vector<int> > M = { { 4, 7, 8 },
                            { 9, 2, 3 },
                            { 0, 4, 1 } };

    printDiagonal(K, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function returns required diagonal
static void printDiagonal(int K, int N,
                          int [][]M)
{
    int startrow, startcol;

    // Initialize values to
    // print upper diagonals
    if (K - 1 < N)
    {
        startrow = K - 1;
        startcol = 0;
    }

    // Initialize values to
    // print lower diagonals
    else
    {
        startrow = N - 1;
        startcol = K - N;
    }

    // Traverse the diagonal
    for(; startrow >= 0 && startcol < N;
          startrow--, startcol++)
    {

        // Print its contents
        System.out.print(M[startrow][startcol] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, K = 4;
    int[][] M = { { 4, 7, 8 },
                  { 9, 2, 3 },
                  { 0, 4, 1 } };

    printDiagonal(K, N, M);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
def printDiagonal(K, N, M):

    startrow, startcol = 0, 0

    # Initialize values to prupper
    # diagonals
    if K - 1 < N:
        startrow = K - 1
        startcol = 0
    else:
        startrow = N - 1
        startcol = K - N

    # Traverse the diagonals
    while startrow >= 0 and startcol < N:

        # Print its contents
        print(M[startrow][startcol], end = " ")
        startrow -= 1
        startcol += 1

# Driver code
if __name__ == '__main__':

    N, K = 3, 4
    M = [ [ 4, 7, 8 ],
          [ 9, 2, 3 ],
          [ 0, 4, 1 ] ]

    printDiagonal(K, N, M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function returns required diagonal
static void printDiagonal(int K, int N,
                          int [,]M)
{
    int startrow, startcol;

    // Initialize values to
    // print upper diagonals
    if (K - 1 < N)
    {
        startrow = K - 1;
        startcol = 0;
    }

    // Initialize values to
    // print lower diagonals
    else
    {
        startrow = N - 1;
        startcol = K - N;
    }

    // Traverse the diagonal
    for(; startrow >= 0 && startcol < N;
          startrow--, startcol++)
    {

        // Print its contents
        Console.Write(M[startrow,startcol] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3, K = 4;
    int[,] M = { { 4, 7, 8 },
                 { 9, 2, 3 },
                 { 0, 4, 1 } };

    printDiagonal(K, N, M);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Function returns required diagonal
function printDiagonal(K,N,M)
{
    let startrow, startcol;

    // Initialize values to
    // print upper diagonals
    if (K - 1 < N)
    {
        startrow = K - 1;
        startcol = 0;
    }

    // Initialize values to
    // print lower diagonals
    else
    {
        startrow = N - 1;
        startcol = K - N;
    }

    // Traverse the diagonal
    for(; startrow >= 0 && startcol < N;
          startrow--, startcol++)
    {

        // Print its contents
        document.write(M[startrow][startcol] + " ");
    }
}

// Driver Code
let N = 3, K = 4;
let M = [[ 4, 7, 8 ],
    [ 9, 2, 3 ],
    [ 0, 4, 1 ]];

printDiagonal(K, N, M);

// This code is contributed by patel2127

</script>
```

**输出:**

```
4 3 
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*