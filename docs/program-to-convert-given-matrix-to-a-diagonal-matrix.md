# 将给定矩阵转换为对角矩阵的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-给定矩阵转对角矩阵/](https://www.geeksforgeeks.org/program-to-convert-given-matrix-to-a-diagonal-matrix/)

给定一个 N*N 矩阵。任务是将矩阵转换成**对角矩阵**。也就是将矩阵的非对角线元素的值更改为 0。
**对角矩阵**:如果一个矩阵的所有非对角元素都为零，这个矩阵叫做对角矩阵。
**例:**

```
Input : mat[][] = {{ 2, 1, 7 },
                   { 3, 7, 2 },
                   { 5, 4, 9 }}
Output : {{2, 0, 7},
          {0, 7, 0},
          {5, 0, 9}}

Input :  mat[][] = {{1, 3, 5, 6, 7},
                    {3, 5, 3, 2, 1},
                    {1, 2, 3, 4, 5},
                    {7, 9, 2, 1, 6},
                    {9, 1, 5, 3, 2}}
Output : {{1, 0, 0, 0, 7},
          {0, 5, 0, 2, 0},
          {0, 0, 3, 0, 0},
          {0, 9, 0, 1, 0},
          {9, 0, 0, 0, 2}}
```

使用两个嵌套循环遍历矩阵的所有非对角线元素，如下代码所示，并使它们为零。
下面是将矩阵的所有非对角元素置零的程序:

## C++

```
// C++ program to change the value of
// non-diagonal elements of a matrix to 0

#include <iostream>
using namespace std;

const int MAX = 100;

// Function to print the resultant matrix
void print(int mat[][MAX], int n, int m)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to change the values of all
// non-diagonal elements to 0
void makenondiagonalzero(int mat[][MAX], int n, int m)
{
    // Traverse all non-diagonal elements
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (i != j && i + j + 1 != n)

                // Change all non-diagonal
                // elements to zero
                mat[i][j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver Code
int main()
{
    int mat[][MAX] = { { 2, 1, 7 },
                       { 3, 7, 2 },
                       { 5, 4, 9 } };

    makenondiagonalzero(mat, 3, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change the value of
// non-diagonal elements of a matrix to 0
import java.io.*;

class GFG
{
static int MAX = 100;

// Function to print the resultant matrix
static void print(int mat[][], int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            System.out.print( mat[i][j] + " ");
        }
        System.out.println();
    }
}

// Function to change the values of all
// non-diagonal elements to 0
static void makenondiagonalzero(int mat[][],
                                int n, int m)
{
    // Traverse all non-diagonal elements
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (i != j && i + j + 1 != n)

                // Change all non-diagonal
                // elements to zero
                mat[i][j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver Code
public static void main (String[] args)
{
    int mat[][] = { { 2, 1, 7 },
                    { 3, 7, 2 },
                    { 5, 4, 9 } };

    makenondiagonalzero(mat, 3, 3);
}
}

// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to change the value of
# non-diagonal elements of a matrix to 0

# Function to print the resultant matrix
def printmatrix(mat, n, m) :

    for i in range(n) :
        for j in range(m) :
            print(mat[i][j], end = " ")

        print()

# Function to change the values
# of all non-diagonal elements to 0
def makenondiagonalzero(mat, n, m) :

    # Traverse all non-diagonal elements
    for i in range(n) :
        for j in range(m) :
            if i != j and i + j + 1 != n :

                # Change all non-diagonal
                # elements to zero
                mat[i][j] = 0

    # print resultant matrix
    printmatrix(mat, n, m)

# Driver code
if __name__ == "__main__" :

    mat = [ [2, 1, 7],
            [3, 7, 2],
            [5, 4, 9] ]

    makenondiagonalzero(mat, 3, 3)

# This code is contributed by Ryuga
```

## C#

```
// C# program to change the value
// of non-diagonal elements of a
// matrix to 0
using System;

class GFG
{

// static int MAX = 100;

// Function to print the resultant
// matrix
static void print(int [,]mat,
                  int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            Console.Write(mat[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to change the values of all
// non-diagonal elements to 0
static void makenondiagonalzero(int [,]mat,
                                int n, int m)
{
    // Traverse all non-diagonal elements
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (i != j && i + j + 1 != n)

                // Change all non-diagonal
                // elements to zero
                mat[i, j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver Code
public static void Main ()
{
    int [,]mat = { { 2, 1, 7 },
                   { 3, 7, 2 },
                   { 5, 4, 9 } };

    makenondiagonalzero(mat, 3, 3);
}
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change the value of
// non-diagonal elements of a matrix to 0

// Function to print the resultant matrix
function print1($mat, $n, $m)
{
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {
            echo $mat[$i][$j] . " ";
        }
        echo "\n";
    }
}

// Function to change the values of
// all non-diagonal elements to 0
function makenondiagonalzero($mat, $n, $m)
{
    // Traverse all non-diagonal elements
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {
            if ($i != $j && $i + $j + 1 != $n)

                // Change all non-diagonal
                // elements to zero
                $mat[$i][$j] = 0;
        }
    }

    // print resultant matrix
    print1($mat, $n, $m);
}

// Driver Code
$mat = array( array( 2, 1, 7 ),
              array( 3, 7, 2 ),
              array( 5, 4, 9 ) );

makenondiagonalzero($mat, 3, 3);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>
// Java Script program to change the value of
// non-diagonal elements of a matrix to 0
let MAX = 100;

// Function to print the resultant matrix
function print(mat,n,m)
{
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < m; j++)
        {
            document.write( mat[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Function to change the values of all
// non-diagonal elements to 0
function makenondiagonalzero(mat,n,m)
{
    // Traverse all non-diagonal elements
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < m; j++)
        {
            if (i != j && i + j + 1 != n)

                // Change all non-diagonal
                // elements to zero
                mat[i][j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver Code

    let mat = [[ 2, 1, 7 ],
                    [ 3, 7, 2 ],
                    [ 5, 4, 9 ]];

    makenondiagonalzero(mat, 3, 3);

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
2 0 7 
0 7 0 
5 0 9
```

**时间复杂度:** O(n*m)