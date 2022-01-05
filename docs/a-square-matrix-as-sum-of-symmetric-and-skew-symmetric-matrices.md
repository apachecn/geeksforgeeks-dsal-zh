# 作为对称矩阵和反对称矩阵之和的方阵

> 原文:[https://www . geesforgeks . org/a-方阵作为对称和反对称矩阵之和/](https://www.geeksforgeeks.org/a-square-matrix-as-sum-of-symmetric-and-skew-symmetric-matrices/)

假设 **A** 是一个包含所有实数条目的方阵。求两个**对称矩阵 P** 和**斜对称矩阵 Q** 使得 P + Q = A.
**对称矩阵:-** 如果矩阵的转置与原矩阵相同，则称方阵为对称矩阵。
**斜对称矩阵:-** 若矩阵的负转置与原矩阵相同，则称方阵为斜对称矩阵。
**示例:**

```
Input :
          {{ 2, -2, -4},
     mat=  {-1,  3,  4},
           { 1, -2, -3}};
Output :
Symmetric matrix-
        2  -1.5 -1.5
      -1.5   3    1
      -1.5   1   -3
Skew Symmetric Matrix-
       0 -0.5 -2.5
     0.5   0   3
     2.5  -3   0
Explanation : The first matrix is symmetric as
transpose of it is same as the given matrix. The
second matrix is Skew Symmetric as negative transpose
is same as this matrix. Also sum of the two matrices
is same as mat[][].

Input:
          {{5, 6, 8},
     mat = {3, 4, 9},
           {7, 2, 3}};
Output :
Symmetric matrix-
       5   4.5   7.5
      4.5   4    5.5
      7.5  5.5    3
Skew Symmetric Matrix-
      0   1.5   0.5
    -1.5   0    3.5
    -0.5 -3.5    0
```

设 A 为正方形矩阵，则
**A =(1/2)*(A+A’)+(1/2)*(A–A’)**其中 A’为 A 的转置矩阵，上式**(1/2)*(A+A’)**代表**对称矩阵**，**(1/2)*(A–A’)**代表**斜对称矩阵**。如果我们仔细观察，我们可以注意到这两个矩阵是对称的和斜对称的(我们基本上是将两个单元值的一半分配给两者)。

## C++

```
// C++ program for distribute a square matrix into
// symmetric and skew symmetric matrix.
#include <bits/stdc++.h>
#define N 3
using namespace std;

/* Below functions can be used to verify result
// Returns true if matrix is skew symmetric,
// else false.
bool isSymmetric(float mat[N][N])
{
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            if (mat[i][j] != mat[j][i])
                return false;
    return true;
}

// Returns true if matrix is skew symmetric,
// else false.
bool isSkewSymmetric(float mat[N][N])
{
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            if (mat[i][j] != -mat[j][i])
                return false;
    return true;
} */

void printMatrix(float mat[N][N])
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            cout << mat[i][j] << "   ";
        cout << endl;
    }
}

void printDistribution(float mat[N][N])
{
    // tr is the transpose of matrix mat.
    float tr[N][N];

    // Find transpose of matrix.
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            tr[i][j] = mat[j][i];

    // Declare two square matrix symm and
    // skewsymm of size N.
    float symm[N][N], skewsymm[N][N];

    // Loop to find symmetric and skew symmetric
    // and store it into symm and skewsymm matrix.
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            symm[i][j] = (mat[i][j] + tr[i][j]) / 2;
            skewsymm[i][j] = (mat[i][j] - tr[i][j]) / 2;
        }
    }

    cout << "Symmetric matrix-" << endl;
    printMatrix(symm);

    cout << "Skew Symmetric matrix-" << endl;
    printMatrix(skewsymm);
}

// Driver function.
int main()
{
    // mat is the N * N square matrix.
    float mat[N][N] = { { 2, -2, -4 },
                        { -1, 3, 4 },
                        { 1, -2, -3 } };
    printDistribution(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for distribute
// a square matrix into
// symmetric and skew symmetric
// matrix.

import java.io.*;
import java.util.*;

class GFG {
static void printMatrix(float mat[][])
{
    for (int i = 0; i < mat.length; i++) {
        for (int j = 0; j < mat[i].length; j++)
            System.out.print(mat[i][j] + "   ");
        System.out.println();
    }
}

static void printDistribution(float mat[][])
{
    // tr is the transpose of matrix mat.
    int N=mat.length;
    float[][] tr = new float[N][N];

    // Find transpose of matrix.
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            tr[i][j] = mat[j][i];

    // Declare two square matrix symm and
    // skewsymm of size N.
    float[][] symm=new float[N][N];
    float[][] skewsymm=new float[N][N];

    // Loop to find symmetric and skew symmetric
    // and store it into symm and skewsymm matrix.
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            symm[i][j] = (mat[i][j] + tr[i][j]) / 2;
            skewsymm[i][j] = (mat[i][j] - tr[i][j]) / 2;
        }
    }

    System.out.println("Symmetric matrix-" );
    printMatrix(symm);

    System.out.println("Skew Symmetric matrix-" );
    printMatrix(skewsymm);
}
    public static void main (String[] args) {

    // mat is the N * N square matrix.
    float mat[][] = { { 2, -2, -4 },
                        { -1, 3, 4 },
                        { 1, -2, -3 } };
    printDistribution(mat);
     }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to distribute a
# square matrix into symmetric
# and skew symmetric matrix.
N = 3;

def printMatrix(mat):

    for i in range(N):
        for j in range(N):
            print(mat[i][j], end = " ");
        print("");

def printDistribution(mat):

    # tr is the transpose
    # of matrix mat.
    tr = [[0 for x in range(N)]
             for y in range(N)];

    # Find transpose of matrix.
    for i in range(N):
        for j in range(N):
            tr[i][j] = mat[j][i];

    # Declare two square
    # matrix symm and
    # skewsymm of size N.
    symm = [[0 for x in range(N)]
               for y in range(N)] ;
    skewsymm = [[0 for x in range(N)]
                   for y in range(N)];

    # Loop to find symmetric
    # and skew symmetric and
    # store it into symm and
    # skewsymm matrix.
    for i in range(N):
        for j in range(N):
            symm[i][j] = (mat[i][j] + tr[i][j]) / 2;
            skewsymm[i][j] = (mat[i][j] - tr[i][j]) / 2;

    print("Symmetric matrix-");
    printMatrix(symm);

    print("Skew Symmetric matrix");
    printMatrix(skewsymm);

# Driver Code

# mat is the N * N
# square matrix.
mat = [[2, -2, -4], [-1, 3, 4], [1, -2, -3]];
printDistribution(mat);

# This code is contributed by mits.
```

## C#

```
// C# program for distribute
// a square matrix into
// symmetric and skew
// symmetric matrix.
using System;

class GFG
{

static int N = 3;
static void printMatrix(float[,] mat)
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            Console.Write(mat[i, j] + " ");
        System.Console.WriteLine();
    }
}

static void printDistribution(float[,] mat)
{
    // tr is the transpose
    // of matrix mat.
    float[,] tr = new float[N, N];

    // Find transpose of matrix.
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            tr[i, j] = mat[j, i];

    // Declare two square matrix symm and
    // skewsymm of size N.
    float[,] symm = new float[N, N];
    float[,] skewsymm = new float[N, N];

    // Loop to find symmetric and skew symmetric
    // and store it into symm and skewsymm matrix.
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            symm[i, j] = (mat[i, j] +
                           tr[i, j]) / 2;
            skewsymm[i, j] = (mat[i, j] -
                               tr[i, j]) / 2;
        } 
    }

    System.Console.WriteLine("Symmetric matrix-" );
    printMatrix(symm);

    System.Console.WriteLine("Skew Symmetric matrix-" );
    printMatrix(skewsymm);
}

// Driver code
public static void Main()
{
    // mat is the N * N
    // square matrix.
    float[,] mat = new float[,]{{ 2, -2, -4},
                                {-1, 3, 4},
                                {1, -2, -3}};
    printDistribution(mat);
}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to distribute a 
// square matrix into symmetric
// and skew symmetric matrix.
$N = 3;

function printMatrix($mat)
{
    global $N;
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
            echo $mat[$i][$j]. " ";
        echo "\n";
    }
}

function printDistribution($mat)
{
    global $N;

    // tr is the transpose
    // of matrix mat.
    $tr;

    // Find transpose of matrix.
    for ($i = 0; $i < $N; $i++)
        for ($j = 0; $j < $N; $j++)
            $tr[$i][$j] = $mat[$j][$i];

    // Declare two square
    // matrix symm and
    // skewsymm of size N.
    $symm;
    $skewsymm;

    // Loop to find symmetric
    // and skew symmetric and
    // store it into symm and
    // skewsymm matrix.
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {
            $symm[$i][$j] = ($mat[$i][$j] +
                             $tr[$i][$j]) / 2;
            $skewsymm[$i][$j] = ($mat[$i][$j] -
                                 $tr[$i][$j]) / 2;
        }
    }

    echo "Symmetric matrix-\n";
    printMatrix($symm);

    echo "Skew Symmetric matrix-\n";
    printMatrix($skewsymm);
}

// Driver Code

// mat is the N * N
// square matrix.
$mat = array(array(2, -2, -4),
             array(-1, 3, 4),
             array(1, -2, -3));
printDistribution($mat);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// javascript program for distribute
// a square matrix into
// symmetric and skew symmetric
// matrix.
function printMatrix(mat)
{
    for (var i = 0; i < mat.length; i++) {
        for (var j = 0; j < mat[i].length; j++)
            document.write(mat[i][j] + "   ");
        document.write('<br>');
    }
}

function printDistribution(mat)
{

    // tr is the transpose of matrix mat.
    var N=mat.length;
    var tr = Array(N).fill(0).map(x => Array(N).fill(0));

    // Find transpose of matrix.
    for (var i = 0; i < N; i++)
        for (var j = 0; j < N; j++)
            tr[i][j] = mat[j][i];

    // Declare two square matrix symm and
    // skewsymm of size N.
    var symm=Array(N).fill(0).map(x => Array(N).fill(0));
    var skewsymm=Array(N).fill(0).map(x => Array(N).fill(0));

    // Loop to find symmetric and skew symmetric
    // and store it into symm and skewsymm matrix.
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < N; j++) {
            symm[i][j] = (mat[i][j] + tr[i][j]) / 2;
            skewsymm[i][j] = (mat[i][j] - tr[i][j]) / 2;
        }
    }

    document.write("Symmetric matrix-<br>" );
    printMatrix(symm);

    document.write("Skew Symmetric matrix-<br>" );
    printMatrix(skewsymm);
}

    // mat is the N * N square matrix.
    var mat = [ [ 2, -2, -4 ],
                        [ -1, 3, 4 ],
                        [ 1, -2, -3 ] ];
    printDistribution(mat);

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
Symmetric matrix-
2 -1.5 -1.5 
-1.5 3 1 
-1.5 1 -3 
Skew Symmetric matrix-
0 -0.5 -2.5 
0.5 0 3 
2.5 -3 0 
```