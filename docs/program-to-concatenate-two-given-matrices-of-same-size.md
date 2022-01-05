# 程序连接两个相同大小的给定矩阵

> 原文:[https://www . geesforgeks . org/program-to-concatenate-两个给定的相同大小的矩阵/](https://www.geeksforgeeks.org/program-to-concatenate-two-given-matrices-of-same-size/)

给定大小为 **M x N** 的两个矩阵 **A** 和 **B** ，任务是将它们连接成一个矩阵。
**矩阵的串联:**将矩阵每行的元素一个接一个地追加的过程称为矩阵的串联。
**示例:**

```
Input:
A[][] = {{1, 2}, 
         {3, 4}},
B[][] = {{5, 6}, 
         {7, 8}}
Output: 
1 2 5 6
3 4 7 8
Explanation:
Elements of every row of the matrix B 
is appended into the row of matrix A.

Input: 
A[][] = {{2, 4}, 
         {3, 4}}
B[][] = {{1, 2}, 
         {1, 3}}       
Output: 
2 4 1 2 
3 4 1 3
```

**方法:**思想是声明一个大小为**N×2 * M**的矩阵，然后遍历矩阵 A 并存储矩阵前半部分的元素，然后类似地迭代矩阵 B 并存储矩阵后半部分的元素，借助于以下公式:

```
// For filling the
// first half of matrix
matrix[i][j] = A[i][j]

// For filling the
// second half of matrix
matrix[i][j+N] = A[i][j + N]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to concatenate
// two matrices of size N x M

#include <bits/stdc++.h>

using namespace std;

#define M 2
#define N 2

// Function to concatenate two
// matrices A[][] and B[][]
void mergeMatrix(int A[M][N],
                 int B[M][N])
{

    // Matrix to store
    // the result
    int C[M][2 * N];

    // Merge the two matrices
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // To store elements
            // of matrix A
            C[i][j] = A[i][j];

            // To store elements
            // of matrix B
            C[i][j + N] = B[i][j];
        }
    }

    // Print the result
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < 2 * N;
             j++)
            cout << C[i][j] << " ";
        cout << endl;
    }
}

// Driven Code
int main()
{
    int A[M][N] = { { 1, 2 },
                    { 3, 4 } };

    int B[M][N] = { { 5, 6 },
                    { 7, 8 } };

    // Find the merge of
    // the 2 matrices
    mergeMatrix(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to concatenate
// two matrices of size N x M
class GFG{

static final int M = 2;
static final int N = 2;

// Function to concatenate two
// matrices A[][] and B[][]
static void mergeMatrix(int A[][],
                        int B[][])
{

    // Matrix to store
    // the result
    int [][]C = new int[M][2 * N];

    // Merge the two matrices
    for(int i = 0; i < M; i++)
    {
       for(int j = 0; j < N; j++)
       {
          // To store elements
          // of matrix A
          C[i][j] = A[i][j];

          // To store elements
          // of matrix B
          C[i][j + N] = B[i][j];

       }
    }

    // Print the result
    for(int i = 0; i < M; i++)
    {
       for(int j = 0; j < 2 * N; j++)
          System.out.print(C[i][j] + " ");

       System.out.println();
    }
}

// Driven Code
public static void main(String[] args)
{
    int A[][] = { { 1, 2 },
                  { 3, 4 } };

    int B[][] = { { 5, 6 },
                  { 7, 8 } };

    // Find the merge of
    // the 2 matrices
    mergeMatrix(A, B);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to concatenate
# two matrices of size N x M

M = 2
N = 2

# Function to concatenate two
# matrices A[][] and B[][]
def mergeMatrix(A, B):

    # Matrix to store
    # the result
    C = [[0 for j in range(2 * N)]
            for i in range(M)]

    # Merge the two matrices
    for i in range(M):
        for j in range(N):

            # To store elements
            # of matrix A
            C[i][j] = A[i][j]

            # To store elements
            # of matrix B
            C[i][j + N] = B[i][j]

    # Print the result
    for i in range(M):
        for j in range(2 * N):    
            print(C[i][j], end = ' ')

        print()

# Driver code
if __name__=='__main__':

    A = [ [1, 2], [3, 4] ]
    B = [ [5, 6], [7, 8] ]

    # Find the merge of
    # the 2 matrices
    mergeMatrix(A, B)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to concatenate
// two matrices of size N x M
using System;

class GFG{

const int M = 2;
const int N = 2;

// Function to concatenate two
// matrices A[][] and B[][]
static void mergeMatrix(int[,] A, int[,] B)
{

    // Matrix to store
    // the result
    int[,] C = new int[M, 2 * N];

    // Merge the two matrices
    for(int i = 0; i < M; i++)
    {
       for(int j = 0; j < N; j++)
       {

          // To store elements
          // of matrix A
          C[i, j] = A[i, j];

          // To store elements
          // of matrix B
          C[i, j + N] = B[i, j];
       }
    }

    // Print the result
    for(int i = 0; i < M; i++)
    {
       for(int j = 0; j < 2 * N; j++)
          Console.Write(C[i, j] + " ");

       Console.WriteLine();
    }
}

// Driver code
static void Main()
{
    int[,] A = { { 1, 2 },
                 { 3, 4 } };

    int[,] B = { { 5, 6 },
                 { 7, 8 } };

    // Find the merge of
    // the 2 matrices
    mergeMatrix(A, B);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation to concatenate
// two matrices of size N x M
M = 2
N = 2

// Function to concatenate two
// matrices A[][] and B[][]
function mergeMatrix(A,B)
{

    // Matrix to store
    // the result
    var C = [[0,0,0,0], [0,0,0,0]]

    // Merge the two matrices
    for (var i = 0; i < M; i++)
    {
        for (var j = 0; j < N; j++)
        {

            // To store elements
            // of matrix A
            C[i][j] = A[i][j];

            // To store elements
            // of matrix B
            C[i][j + N] = B[i][j];
        }
    }

    // Print the result
    for (var i = 0; i < M; i++)
    {
        for (var j = 0; j < 2 * N;
             j++)
            document.write( C[i][j] + " ");
        document.write("<br>");
    }
}

// Driven Code
var A = [ [ 1, 2 ],
                [ 3, 4 ] ];
var B = [ [ 5, 6 ],
                [ 7, 8 ] ];

// Find the merge of
// the 2 matrices
mergeMatrix(A, B);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1 2 5 6 
3 4 7 8
```

***时间复杂度:** O(M * N)*

***辅助空间:** O(M * N)*