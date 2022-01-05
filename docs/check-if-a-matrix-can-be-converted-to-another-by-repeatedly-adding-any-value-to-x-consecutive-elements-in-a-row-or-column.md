# 通过对一行或一列中的 X 个连续元素重复添加任何值来检查一个矩阵是否可以转换成另一个矩阵

> 原文:[https://www . geeksforgeeks . org/check-if-a-matrix-可以通过在一行或一列中向 x 个连续元素重复添加任意值来转换为另一个元素/](https://www.geeksforgeeks.org/check-if-a-matrix-can-be-converted-to-another-by-repeatedly-adding-any-value-to-x-consecutive-elements-in-a-row-or-column/)

给定两个大小为 **M × N** 的[矩阵](https://www.geeksforgeeks.org/adjoint-inverse-matrix/)**A【】【】**和**B【】【】**以及一个整数 **X** ，任务是检查是否有可能将矩阵**A【】【】【】**转换为矩阵**B【】【】**通过将任意值添加到同一行或同一列中任意次数的 **X** 连续单元格中(*可能为零*)。

**示例:**

> **输入:** A[][] = { {0，0}，{0，0}}，B[][] = {{1，2}，{0，1}}，X = 2
> **输出:**是
> **解释:**
> 操作 1:将 1 添加到 A[0][0]，A[0][1]将 A[][]修改为{{1，1}，{0，0}}。
> 操作 2:将 1 添加到 A[0][1]和 A[1][1]会将 A[][]修改为{{1，2}，{0，1}}。
> 执行这两个操作后，矩阵 A[][]和 B[][]相等。
> 
> **输入:** A= {{0，0，0}，{0，0，0}}，B = {{1，2，3}，{4，5，6}}，X = 4
> T3】输出:假

**方法:**这个问题可以通过[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)执行所有水平操作，然后是垂直操作来解决。
按照以下步骤解决问题:

*   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)执行水平操作，在范围**【0，M–1】**和**【0，N–X】**上使用变量 **i** 和 **j** ，并执行以下操作:
    *   如果 **A[i][j]** 不等于 **B[i][j]** ，则将同一行中的下一个 **X** 元素增加**A[I][j]–B[I][j]**。
*   现在，[遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)执行垂直操作，在范围**【0，M–X】**和**【0，N–1】**上使用变量 **i** 和 **j** ，并执行以下操作:
    *   检查 **A[i][j]** 是否等于 **B[i][j]** 。
    *   如果发现为假，将同一列中的下一个 **X** 元素增加**A[I][j]–B[I][j]**。
*   如果矩阵 A[][]和 B[][]相等，则打印**“真”** [。否则，打印**“假”**。](https://www.geeksforgeeks.org/program-to-check-if-two-given-matrices-are-identical/)

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether Matrix A[][]
// can be transformed to Matrix B[][] or not
bool Check(int A[][2], int B[][2],
           int M, int N, int X)
{
    // Traverse the matrix to perform
    // horizontal operations
    for (int i = 0; i < M; i++) {
        for (int j = 0; j <= N - X; j++) {

            if (A[i][j] != B[i][j]) {

                // Calculate difference
                int diff = B[i][j] - A[i][j];

                for (int k = 0; k < X; k++) {

                    // Update next X elements
                    A[i][j + k] = A[i][j + k] + diff;
                }
            }
        }
    }

    // Traverse the matrix to perform
    // vertical operations
    for (int i = 0; i <= M - X; i++) {
        for (int j = 0; j < N; j++) {

            if (A[i][j] != B[i][j]) {

                // Calculate difference
                int diff = B[i][j] - A[i][j];
                for (int k = 0; k < X; k++) {

                    // Update next K elements
                    A[i + k][j] = A[i + k][j] + diff;
                }
            }
        }
    }

    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // A[i][j] is not equal to B[i][j]
            if (A[i][j] != B[i][j]) {

                // Conversion is not possible
                return 0;
            }
        }
    }

    // Conversion is possible
    return 1;
}

// Driver Code
int main()
{
    // Input
    int M = 2, N = 2, X = 2;
    int A[2][2] = { { 0, 0 }, { 0, 0 } };
    int B[2][2] = { { 1, 2 }, { 0, 1 } };

    if (Check(A, B, M, N, X)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check whether Matrix A[][]
// can be transformed to Matrix B[][] or not
static int Check(int A[][], int B[][],
                 int M, int N, int X)
{

    // Traverse the matrix to perform
    // horizontal operations
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j <= N - X; j++)
        {
            if (A[i][j] != B[i][j])
            {

                // Calculate difference
                int diff = B[i][j] - A[i][j];

                for(int k = 0; k < X; k++)
                {

                    // Update next X elements
                    A[i][j + k] = A[i][j + k] + diff;
                }
            }
        }
    }

    // Traverse the matrix to perform
    // vertical operations
    for(int i = 0; i <= M - X; i++)
    {
        for(int j = 0; j < N; j++)
        {
            if (A[i][j] != B[i][j])
            {

                // Calculate difference
                int diff = B[i][j] - A[i][j];
                for(int k = 0; k < X; k++)
                {

                    // Update next K elements
                    A[i + k][j] = A[i + k][j] + diff;
                }
            }
        }
    }

    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // A[i][j] is not equal to B[i][j]
            if (A[i][j] != B[i][j])
            {

                // Conversion is not possible
                return 0;
            }
        }
    }

    // Conversion is possible
    return 1;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int M = 2, N = 2, X = 2;
    int A[][] = { { 0, 0 }, { 0, 0 } };
    int B[][] = { { 1, 2 }, { 0, 1 } };

    if (Check(A, B, M, N, X) != 0)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether Matrix A[][]
# can be transformed to Matrix B[][] or not
def Check(A, B, M, N, X):

    # Traverse the matrix to perform
    # horizontal operations
    for i in range(M):
        for j in range(N - X + 1):
            if (A[i][j] != B[i][j]):

                # Calculate difference
                diff = B[i][j] - A[i][j]

                for k in range(X):

                    # Update next X elements
                    A[i][j + k] = A[i][j + k] + diff

    # Traverse the matrix to perform
    # vertical operations
    for i in range(M - X + 1):
        for j in range(N):
            if (A[i][j] != B[i][j]):

                # Calculate difference
                diff = B[i][j] - A[i][j]
                for k in range(X):

                    # Update next K elements
                    A[i + k][j] = A[i + k][j] + diff

    for i in range(M):
        for j in range(N):

            # A[i][j] is not equal to B[i][j]
            if (A[i][j] != B[i][j]):

                # Conversion is not possible
                return 0

    # Conversion is possible
    return 1

# Driver Code
if __name__ == '__main__':

    # Input
    M, N, X = 2, 2, 2
    A = [ [ 0, 0 ], [ 0, 0 ] ]
    B = [ [ 1, 2 ], [ 0, 1 ] ]

    if (Check(A, B, M, N, X)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check whether Matrix A[][]
// can be transformed to Matrix B[][] or not
static int Check(int [,]A, int [,]B,
                 int M, int N, int X)
{

    // Traverse the matrix to perform
    // horizontal operations
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j <= N - X; j++)
        {
            if (A[i, j] != B[i, j])
            {

                // Calculate difference
                int diff = B[i, j] - A[i, j];

                for(int k = 0; k < X; k++)
                {

                    // Update next X elements
                    A[i, j + k] = A[i, j + k] + diff;
                }
            }
        }
    }

    // Traverse the matrix to perform
    // vertical operations
    for(int i = 0; i <= M - X; i++)
    {
        for(int j = 0; j < N; j++)
        {
            if (A[i, j] != B[i, j])
            {

                // Calculate difference
                int diff = B[i,j] - A[i,j];
                for(int k = 0; k < X; k++)
                {

                    // Update next K elements
                    A[i + k, j] = A[i + k, j] + diff;
                }
            }
        }
    }

    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // A[i][j] is not equal to B[i][j]
            if (A[i, j] != B[i, j])
            {

                // Conversion is not possible
                return 0;
            }
        }
    }

    // Conversion is possible
    return 1;
}

// Driver Code
public static void Main()
{

    // Input
    int M = 2, N = 2, X = 2;
    int [,]A = { { 0, 0 }, { 0, 0 } };
    int [,]B = { { 1, 2 }, { 0, 1 } };

    if (Check(A, B, M, N, X) == 1)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
//Javascript program for the above approach

// Function to check whether Matrix A[][]
// can be transformed to Matrix B[][] or not
function Check( A, B,M, N, X)
{
    // Traverse the matrix to perform
    // horizontal operations
    for (var i = 0; i < M; i++) {
        for (var j = 0; j <= N - X; j++) {

            if (A[i][j] != B[i][j]) {

                // Calculate difference
                var diff = B[i][j] - A[i][j];

                for (var k = 0; k < X; k++) {

                    // Update next X elements
                    A[i][j + k] = A[i][j + k] + diff;
                }
            }
        }
    }

    // Traverse the matrix to perform
    // vertical operations
    for (var i = 0; i <= M - X; i++) {
        for (var j = 0; j < N; j++) {

            if (A[i][j] != B[i][j]) {

                // Calculate difference
                var diff = B[i][j] - A[i][j];
                for (var k = 0; k < X; k++) {

                    // Update next K elements
                    A[i + k][j] = A[i + k][j] + diff;
                }
            }
        }
    }

    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++) {

            // A[i][j] is not equal to B[i][j]
            if (A[i][j] != B[i][j]) {

                // Conversion is not possible
                return 0;
            }
        }
    }

    // Conversion is possible
    return 1;
}

var M = 2, N = 2, X = 2;
    var A = [ [ 0, 0 ], [ 0, 0 ]];
    var B = [ [ 1, 2 ], [ 0, 1 ] ];

    if (Check(A, B, M, N, X)) {
       document.write( "Yes" + "<br>");
    }
    else {
        document.write( "No" + "<br>");
    }

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(M * N * X)*
T5**辅助空间:** O(1)