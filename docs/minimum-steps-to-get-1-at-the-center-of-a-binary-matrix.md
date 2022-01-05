# 在二元矩阵中心得到 1 的最小步数

> 原文:[https://www . geeksforgeeks . org/二进制矩阵中心最少获得 1 步/](https://www.geeksforgeeks.org/minimum-steps-to-get-1-at-the-center-of-a-binary-matrix/)

给定一个 **N * N** 矩阵，其中 **N** 与所有 0 值都是奇数，只有一个单元格的值为 1。任务是找到最小可能的移动，当在一次移动中，任何两个连续的行或两个连续的列可以交换时，将这个 1 移动到矩阵的中心。
**例:**

> **输入:** mat[][] = {
> {0，0，1，0，0}、
> {0，0，0，0，0}、
> {0，0，0，0，0，0}、
> {0，0，0，0，0，0}、
> {0，0，0，0，0，0，0}}
> **输出:** 2
> 操作 1:交换第一行和第二行。
> 操作 2:交换第二排和第三排。
> **输入:** mat[][] = {
> {0，0，0}，
> {0，1，0}，
> {0，0，0}}
> **输出:** 0

**进场:**

*   计算矩阵中心的位置为 **(cI，cJ) = (⌊N / 2⌋，⌊N / 2⌋)** 。
*   找到 **1** 在矩阵中的位置，存储在 **(oneI，oneJ)** 中。
*   现在，最小可能的移动将是**ABS(cI–OneI)+ABS(Cj–OneJ)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int N = 5;

// Function to return the
// minimum moves required
int minMoves(int mat[N][N])
{

    // Center of the matrix
    int cI = N / 2, cJ = N / 2;

    // Find the position of the 1
    int oneI = 0, oneJ = 0;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                oneI = i;
                oneJ = j;
                break;
            }
        }
    }

    return (abs(cI - oneI) + abs(cJ - oneJ));
}

// Driver code
int main()
{
    int mat[N][N] = { { 0, 0, 0, 0, 0 },
                      { 0, 0, 0, 0, 0 },
                      { 0, 0, 0, 0, 0 },
                      { 0, 0, 0, 0, 0 },
                      { 0, 0, 1, 0, 0 } };

    cout << minMoves(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int N = 5;

// Function to return the
// minimum moves required
static int minMoves(int mat[][])
{

    // Center of the matrix
    int cI = N / 2, cJ = N / 2;

    // Find the position of the 1
    int oneI = 0, oneJ = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            if (mat[i][j] == 1)
            {
                oneI = i;
                oneJ = j;
                break;
            }
        }
    }

    return (Math.abs(cI - oneI) + Math.abs(cJ - oneJ));
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 1, 0, 0 } };

    System.out.print(minMoves(mat));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 5

# Function to return the
# minimum moves required
def minMoves(mat):

    # Center of the matrix
    cI = N // 2
    cJ = N // 2

    # Find the position of the 1
    oneI = 0
    oneJ = 0
    for i in range(N):
        for j in range(N):
            if (mat[i][j] == 1):
                oneI = i
                oneJ = j
                break

    return (abs(cI - oneI) + abs(cJ - oneJ))

# Driver code
mat = [[0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0],
       [0, 0, 1, 0, 0]]

print(minMoves(mat))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int N = 5;

// Function to return the
// minimum moves required
static int minMoves(int [,]mat)
{

    // Center of the matrix
    int cI = N / 2, cJ = N / 2;

    // Find the position of the 1
    int oneI = 0, oneJ = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            if (mat[i, j] == 1)
            {
                oneI = i;
                oneJ = j;
                break;
            }
        }
    }
    return (Math.Abs(cI - oneI) +
            Math.Abs(cJ - oneJ));
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = {{ 0, 0, 0, 0, 0 },
                  { 0, 0, 0, 0, 0 },
                  { 0, 0, 0, 0, 0 },
                  { 0, 0, 0, 0, 0 },
                  { 0, 0, 1, 0, 0 }};

    Console.Write(minMoves(mat));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

const N = 5;

// Function to return the
// minimum moves required
function minMoves(mat)
{

    // Center of the matrix
    let cI = parseInt(N / 2), cJ = parseInt(N / 2);

    // Find the position of the 1
    let oneI = 0, oneJ = 0;
    for (let i = 0; i < N; i++) {
        for (let j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                oneI = i;
                oneJ = j;
                break;
            }
        }
    }

    return (Math.abs(cI - oneI) + Math.abs(cJ - oneJ));
}

// Driver code
    let mat = [ [ 0, 0, 0, 0, 0 ],
                      [ 0, 0, 0, 0, 0 ],
                      [ 0, 0, 0, 0, 0 ],
                      [ 0, 0, 0, 0, 0 ],
                      [ 0, 0, 1, 0, 0 ] ];

    document.write(minMoves(mat));

</script>
```

**Output:** 

```
2
```