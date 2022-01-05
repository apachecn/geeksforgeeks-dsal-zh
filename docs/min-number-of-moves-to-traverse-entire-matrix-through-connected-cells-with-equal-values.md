# 穿过具有相等值的连接单元的整个矩阵的最小移动次数

> 原文:[https://www . geeksforgeeks . org/min-移动次数-遍历整个矩阵-通过具有相等值的连接单元/](https://www.geeksforgeeks.org/min-number-of-moves-to-traverse-entire-matrix-through-connected-cells-with-equal-values/)

给定维度为 **N*M** 的矩阵 **A[][]** ，任务是从 **(0，0)** 开始，通过在每一步遍历具有相等值的连接单元，找到遍历整个矩阵所需的最小移动次数。

> 从一个单元(I，j)开始，可以连接单元(i + 1，j)、(I–1，j)、(I，j–1)和(I，j + 1)。

**示例:**

> **输入:** arr[][] = {{1，1，2，2，1}，{1，1，2，2，1}，{1，1，1，3，2}}
> **输出:** 5
> **说明:**
> 遍历矩阵至少需要 5 步。
> 第一步:从[0，0]开始，遍历单元格[0，1]，[1，1]，[1，0]，[2，0]，[2，1]，[2，2]，因为所有这些单元格都有相同的值，1。
> 第二次移动:遍历单元格[0，2]，[0，3]，[1，3]，[1，2]，因为所有这些单元格的值都是 2。
> 第三次移动:遍历包含 1 的单元格[0，4]，[1，4]。
> 第四步:遍历包含 3 的[2，3]。
> 第五招:遍历包含 4 的【2，4】。
> 
> **输入:** arr[][] = {{2，1，3}，{1，1，2}}
> **输出:** 4
> **解释:**
> 覆盖这个二维数组至少需要 4 次移动
> 第一次移动:仅遍历[0，0]，因为没有其他连接的单元格有值 2。
> 第二次移动:遍历单元格[0，1]，[1，1]，[1，0]，因为这些单元格包含值 1。
> 第三次移动:遍历包含 3 的单元格[0，2]。
> 第四步:遍历包含 2 的单元格[1，2]。

**方法:**
按照以下步骤解决问题:

*   创建另一个矩阵，用不同的值填充每个单元格。
*   从 **(0，0)** 开始遍历矩阵 **A[][]** 。对于每个单元格 **(i，j)** ，检查其相邻单元格是否具有与**A【I】【j】**相同的值。
*   如果任何相邻单元格具有相同的值，请将 **B[][]** 中的该单元格替换为 **B[i][j]** 的值。
*   在完成对 **A[][]** 的遍历后，对 **B[][]** 矩阵中剩余的不同元素的计数给出了所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// minimum number of moves
// to traverse a given matrix

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of moves to traverse
// the given matrix
int solve(int A[][10], int N, int M)
{

    int B[N][M];
    int c = 1;
    set<int> s;

    // Constructing another matrix
    // consisting of distinct values
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++)
            B[i][j] = c++;
    }

    // Updating the array B by checking
    // the values of A that if there are
    // same values connected
    // through an edge or not
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            // Check for boundary
            // condition of the matrix
            if (i != 0) {

                // If adjacent cells have
                // same value
                if (A[i - 1][j] == A[i][j])
                    B[i - 1][j] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (i != N - 1) {

                // If adjacent cells have
                // same value
                if (A[i + 1][j] == A[i][j])
                    B[i + 1][j] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (j != 0) {

                // If adjacent cells have
                // same value
                if (A[i][j - 1] == A[i][j])
                    B[i][j - 1] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (j != M - 1) {

                // If adjacent cells have
                // same value
                if (A[i][j + 1] == A[i][j])
                    B[i][j + 1] = B[i][j];
            }
        }
    }

    // Store all distinct elements
    // in a set
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++)
            s.insert(B[i][j]);
    }

    // Return answer
    return s.size();
}

// Driver Code
int main()
{
    int N = 2, M = 3;
    int A[][10] = { { 2, 1, 3 },
                    { 1, 1, 2 } };
    // Function Call
    cout << solve(A, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum number of moves
// to traverse a given matrix
import java.util.*;

class GFG{

// Function to find the minimum
// number of moves to traverse
// the given matrix
static int solve(int A[][], int N,
                            int M)
{
    int [][]B = new int[N][M];
    int c = 1;

    HashSet<Integer> s = new HashSet<Integer>();

    // Constructing another matrix
    // consisting of distinct values
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
          B[i][j] = c++;
    }

    // Updating the array B by checking
    // the values of A that if there are
    // same values connected
    // through an edge or not
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
       {

          // Check for boundary
          // condition of the matrix
          if (i != 0)
          {

              // If adjacent cells have
              // same value
              if (A[i - 1][j] == A[i][j])
                  B[i - 1][j] = B[i][j];
          }

          // Check for boundary
          // condition of the matrix
          if (i != N - 1)
          {

              // If adjacent cells have
              // same value
              if (A[i + 1][j] == A[i][j])
                  B[i + 1][j] = B[i][j];
          }

          // Check for boundary
          // condition of the matrix
          if (j != 0)
          {

              // If adjacent cells have
              // same value
              if (A[i][j - 1] == A[i][j])
                  B[i][j - 1] = B[i][j];
          }

          // Check for boundary
          // condition of the matrix
          if (j != M - 1)
          {

              // If adjacent cells have
              // same value
              if (A[i][j + 1] == A[i][j])
                  B[i][j + 1] = B[i][j];
          }
       }
    }

    // Store all distinct elements
    // in a set
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
          s.add(B[i][j]);
    }

    // Return answer
    return s.size();
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, M = 3;
    int A[][] = { { 2, 1, 3 },
                  { 1, 1, 2 } };

    // Function Call
    System.out.print(solve(A, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the
# minimum number of moves
# to traverse a given matrix

# Function to find the minimum
# number of moves to traverse
# the given matrix
def solve(A, N, M):

    B = []
    c = 1
    s = set()

    # Constructing another matrix
    # consisting of distinct values
    for i in range(N):
        new = []
        for j in range(M):
            new.append(c)
            c = c + 1

        B.append(new)

    # Updating the array B by checking
    # the values of A that if there are
    # same values connected
    # through an edge or not
    for i in range(N):
        for j in range(M):

            # Check for boundary
            # condition of the matrix
            if i != 0:

                # If adjacent cells have
                # same value
                if A[i - 1][j] == A[i][j]:
                    B[i - 1][j] = B[i][j]

            # Check for boundary
            # condition of the matrix
            if (i != N - 1):

                # If adjacent cells have
                # same value
                if A[i + 1][j] == A[i][j]:
                    B[i + 1][j] = B[i][j]

            # Check for boundary
            # condition of the matrix
            if (j != 0):

                # If adjacent cells have
                # same value
                if A[i][j - 1] == A[i][j]:
                    B[i][j - 1] = B[i][j]

            # Check for boundary
            # condition of the matrix
            if (j != M - 1):

                # If adjacent cells have
                # same value
                if (A[i][j + 1] == A[i][j]): 
                    B[i][j + 1] = B[i][j]

    # Store all distinct elements
    # in a set
    for i in range(N):
        for j in range(M):
            s.add(B[i][j])

    # Return answer
    return len(s)

# Driver code
N = 2
M = 3
A = [ [ 2, 1, 3 ], [ 1, 1, 2 ] ]

# Function call
print(solve(A, N, M))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the
// minimum number of moves
// to traverse a given matrix
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// number of moves to traverse
// the given matrix
static int solve(int [,]A, int N,
                           int M)
{
    int [,]B = new int[N, M];
    int c = 1;

    HashSet<int> s = new HashSet<int>();

    // Constructing another matrix
    // consisting of distinct values
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
          B[i, j] = c++;
    }

    // Updating the array B by checking
    // the values of A that if there are
    // same values connected
    // through an edge or not
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
       {

          // Check for boundary
          // condition of the matrix
          if (i != 0)
          {

              // If adjacent cells have
              // same value
              if (A[i - 1, j] == A[i, j])
                  B[i - 1, j] = B[i, j];
          }

          // Check for boundary
          // condition of the matrix
          if (i != N - 1)
          {

              // If adjacent cells have
              // same value
              if (A[i + 1, j] == A[i, j])
                  B[i + 1, j] = B[i, j];
          }

          // Check for boundary
          // condition of the matrix
          if (j != 0)
          {

              // If adjacent cells have
              // same value
              if (A[i, j - 1] == A[i, j])
                  B[i, j - 1] = B[i, j];
          }

          // Check for boundary
          // condition of the matrix
          if (j != M - 1)
          {

              // If adjacent cells have
              // same value
              if (A[i, j + 1] == A[i, j])
                  B[i, j + 1] = B[i, j];
          }
       }
    }

    // Store all distinct elements
    // in a set
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
          s.Add(B[i, j]);
    }

    // Return answer
    return s.Count;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, M = 3;
    int [,]A = { { 2, 1, 3 },
                 { 1, 1, 2 } };

    // Function Call
    Console.Write(solve(A, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the
// minimum number of moves
// to traverse a given matrix

// Function to find the minimum
// number of moves to traverse
// the given matrix
function solve(A, N, M)
{

    var B = Array.from(Array(N), ()=> Array(M));
    var c = 1;
    var s = new Set();

    // Constructing another matrix
    // consisting of distinct values
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++)
            B[i][j] = c++;
    }

    // Updating the array B by checking
    // the values of A that if there are
    // same values connected
    // through an edge or not
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++) {

            // Check for boundary
            // condition of the matrix
            if (i != 0) {

                // If adjacent cells have
                // same value
                if (A[i - 1][j] == A[i][j])
                    B[i - 1][j] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (i != N - 1) {

                // If adjacent cells have
                // same value
                if (A[i + 1][j] == A[i][j])
                    B[i + 1][j] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (j != 0) {

                // If adjacent cells have
                // same value
                if (A[i][j - 1] == A[i][j])
                    B[i][j - 1] = B[i][j];
            }

            // Check for boundary
            // condition of the matrix
            if (j != M - 1) {

                // If adjacent cells have
                // same value
                if (A[i][j + 1] == A[i][j])
                    B[i][j + 1] = B[i][j];
            }
        }
    }

    // Store all distinct elements
    // in a set
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++)
            s.add(B[i][j]);
    }

    // Return answer
    return s.size;
}

// Driver Code
var N = 2, M = 3;
var A = [ [ 2, 1, 3 ],
                [ 1, 1, 2 ]];
// Function Call
document.write( solve(A, N, M));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*