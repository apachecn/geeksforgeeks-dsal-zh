# 将矩阵元素相乘 N 次后打印矩阵

> 原文:[https://www . geesforgeks . org/print-matrix-乘法后-matrix-elements-n-times/](https://www.geeksforgeeks.org/print-matrix-after-multiplying-matrix-elements-n-times/)

给定一个正方形[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**和一个整数 **N** ，任务是将矩阵**乘以**后[打印矩阵](https://www.geeksforgeeks.org/print-2-d-array-matrix-java/)。

**示例:**

> **输入:** mat[][] = {{1，2，3}，{3，4，5}，{6，7，9}}，N = 2
> T3】输出:T5】25 31 40
> 45 57 74
> 81 103 134
> 
> **输入:** mat[][] = {{1，2}，{3，4}}，N = 3
> T3】输出:T5】37 54
> 81 118

**进场:**思路是使用[矩阵乘法](https://www.geeksforgeeks.org/strassens-matrix-multiplication/) [身份矩阵](https://en.wikipedia.org/wiki/Identity_matrix)。即 **A = IA** 、 **A = AI** ，其中 **A** 为 **N * M** 阶次尺寸的矩阵， **I** 为尺寸 **M * N** 的恒等式矩阵，其中 **N** 为总行数， **M** 为矩阵中的总列数。

其思路是迭代范围**【1，N】**，用 **A.I** 更新**身份矩阵**，这样在计算出**A<sup>2</sup>T9】的值后= **A.A** ，**A<sup>3</sup>T15】就可以计算为**A . A<sup>2</sup>T19】等等，直到 **A 【T21********

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function for matrix multiplication
void power(vector<vector<int>>& I,
           vector<vector<int>>& a,
           int rows, int cols)
{

    // Stores the resultant matrix
    // after multiplying a[][] by I[][]
    vector<vector<int>> res(rows, vector<int>(cols));

    // Matrix multiplication
    for(int i = 0; i < rows; ++i)
    {
        for(int j = 0; j < cols; ++j)
        {
            for(int k = 0; k < rows; ++k)
            {
                res[i][j] += a[i][k] * I[k][j];
            }
        }
    }

    // Updating identity element
    // of a matrix
    for(int i = 0; i < rows; ++i)
    {
        for(int j = 0; j < cols; ++j)
        {
            I[i][j] = res[i][j];
        }
    }
}

// Function to print the given matrix
void print(vector<vector<int> >& a)
{

    // Traverse the row
    for(int i = 0; i < a.size(); ++i)
    {

        // Traverse the column
        for(int j = 0; j < a[0].size(); ++j)
        {
            cout << a[i][j] << " ";
        }
        cout << "\n";
    }
}

// Function to multiply the given
// matrix N times
void multiply(vector<vector<int> >& arr, int N)
{

    // Identity element of matrix
    vector<vector<int>> I(arr.size(),
                          vector<int>(arr[0].size()));

    // Update the Identity Matrix
    for(int i = 0; i < arr.size(); ++i)
    {
        for(int j = 0; j < arr[0].size(); ++j)
        {

            // For the diagonal element
            if (i == j)
            {
                I[i][j] = 1;
            }
            else
            {
                I[i][j] = 0;
            }
        }
    }

    // Multiply the matrix N times
    for(int i = 1; i <= N; ++i)
    {
        power(I, arr, arr.size(), arr[0].size());
    }

    // Update the matrix arr[i] to
    // to identity matrix
    for(int i = 0; i < arr.size(); ++i)
    {
        for(int j = 0; j < arr[0].size(); ++j)
        {
            arr[i][j] = I[i][j];
        }
    }

    // Print the matrix
    print(arr);
}

// Driver Code
int main()
{

    // Given 2d array
    vector<vector<int>> arr = { { 1, 2, 3 },
                                { 3, 4, 5 },
                                { 6, 7, 9 } };

    // Given N
    int N = 2;

    // Function Call
    multiply(arr, N);
    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function for matrix multiplication
    static void power(int I[][], int a[][],
                      int rows, int cols)
    {
        // Stores the resultant matrix
        // after multiplying a[][] by I[][]
        int res[][] = new int[rows][cols];

        // Matrix multiplication
        for (int i = 0; i < rows; ++i) {
            for (int j = 0;
                 j < cols; ++j) {
                for (int k = 0;
                     k < rows; ++k) {

                    res[i][j] += a[i][k]
                                 * I[k][j];
                }
            }
        }

        // Updating identity element
        // of a matrix
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                I[i][j] = res[i][j];
            }
        }
    }

    // Function to print the given matrix
    static void print(int a[][])
    {
        // Traverse the row
        for (int i = 0;
             i < a.length; ++i) {

            // Traverse the column
            for (int j = 0;
                 j < a[0].length; ++j) {
                System.out.print(a[i][j]
                                 + " ");
            }
            System.out.println();
        }
    }

    // Function to multiply the given
    // matrix N times
    public static void multiply(
        int arr[][], int N)
    {
        // Identity element of matrix
        int I[][]
            = new int[arr.length][arr[0].length];

        // Update the Identity Matrix
        for (int i = 0; i < arr.length; ++i) {

            for (int j = 0;
                 j < arr[0].length; ++j) {

                // For the diagonal element
                if (i == j) {
                    I[i][j] = 1;
                }
                else {
                    I[i][j] = 0;
                }
            }
        }

        // Multiply the matrix N times
        for (int i = 1; i <= N; ++i) {
            power(I, arr, arr.length,
                  arr[0].length);
        }

        // Update the matrix arr[i] to
        // to identity matrix
        for (int i = 0;
             i < arr.length; ++i) {

            for (int j = 0;
                 j < arr[0].length; ++j) {
                arr[i][j] = I[i][j];
            }
        }
        // Print the matrix
        print(arr);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given 2d array
        int arr[][]
            = { { 1, 2, 3 },
                { 3, 4, 5 },
                { 6, 7, 9 } };

        // Given N
        int N = 2;

        // Function Call
        multiply(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for matrix multiplication
def power(I, a, rows, cols):

    # Stores the resultant matrix
    # after multiplying a[][] by I[][]
    res = [[0 for i in range(cols)]
              for j in range(rows)]

    # Matrix multiplication
    for i in range(0, rows):
        for j in range(0, cols):
            for k in range(0, rows):
                res[i][j] += a[i][k] * I[k][j]

    # Updating identity element
    # of a matrix
    for i in range(0, rows):
        for j in range(0, cols):
            I[i][j] = res[i][j]

# Function to print the given matrix
def prints(a):

    # Traverse the row
    for i in range(0, len(a)):

        # Traverse the column
        for j in range(0, len(a[0])):
            print(a[i][j], end = ' ')

        print()

# Function to multiply the given
# matrix N times
def multiply(arr, N):

    # Identity element of matrix
    I = [[1 if i == j else 0 for i in range(
                  len(arr))] for j in range(
                  len(arr[0]))]

    # Multiply the matrix N times
    for i in range(1, N + 1):
        power(I, arr, len(arr), len(arr[0]))

    # Update the matrix arr[i] to
    # to identity matrix
    for i in range(0, len(arr)):
        for j in range(0, len(arr[0])):
            arr[i][j] = I[i][j]

    # Print the matrix
    prints(arr)

# Driver Code
if __name__ == '__main__':

    # Given 2d array
    arr = [ [ 1, 2, 3 ],
            [ 3, 4, 5 ],
            [ 6, 7, 9 ] ]

    # Given N
    N = 2

    # Function Call
    multiply(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function for matrix multiplication
static void power(int[,] I, int[,] a,
                  int rows, int cols)
{

    // Stores the resultant matrix
    // after multiplying a[][] by I[][]
    int[,] res = new int[rows, cols];

    // Matrix multiplication
    for(int i = 0; i < rows; ++i)
    {
        for(int j = 0; j < cols; ++j)
        {
            for(int k = 0; k < rows; ++k)
            {
                res[i, j] += a[i, k] * I[k, j];
            }
        }
    }

    // Updating identity element
    // of a matrix
    for(int i = 0; i < rows; ++i)
    {
        for(int j = 0; j < cols; ++j)
        {
            I[i, j] = res[i, j];
        }
    }
}

// Function to print the given matrix
static void print(int[, ] a)
{

    // Traverse the row
    for(int i = 0; i < a.GetLength(0); ++i)
    {

        // Traverse the column
        for(int j = 0; j < a.GetLength(1); ++j)
        {
            Console.Write(a[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to multiply the given
// matrix N times
public static void multiply(int[, ] arr, int N)
{

    // Identity element of matrix
    int[, ] I = new int[arr.GetLength(0),
                        arr.GetLength(1)];

    // Update the Identity Matrix
    for(int i = 0; i < arr.GetLength(0); ++i)
    {
        for(int j = 0; j < arr.GetLength(1); ++j)
        {

            // For the diagonal element
            if (i == j)
            {
                I[i, j] = 1;
            }
            else
            {
                I[i, j] = 0;
            }
        }
    }

    // Multiply the matrix N times
    for(int i = 1; i <= N; ++i)
    {
        power(I, arr, arr.GetLength(0),
                      arr.GetLength(1));
    }

    // Update the matrix arr[i] to
    // to identity matrix
    for(int i = 0; i < arr.GetLength(0); ++i)
    {
        for(int j = 0; j < arr.GetLength(1); ++j)
        {
            arr[i, j] = I[i, j];
        }
    }

    // Print the matrix
    print(arr);
}

// Driver Code
public static void Main()
{

    // Given 2d array
    int[, ] arr = { { 1, 2, 3 },
                    { 3, 4, 5 },
                    { 6, 7, 9 } };

    // Given N
    int N = 2;

    // Function Call
    multiply(arr, N);
}
}

// This code is contributed by akhilsaini
```

**Output:** 

```
25 31 40 
45 57 74 
81 103 134

```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*