# 顺时针方向将除对角线以外的所有矩阵元素旋转 90 度

> 原文:[https://www . geesforgeks . org/rotate-所有矩阵元素-除了-对角线-k-乘以-90 度-顺时针方向/](https://www.geeksforgeeks.org/rotate-all-matrix-elements-except-the-diagonal-k-times-by-90-degrees-in-clockwise-direction/)

给定尺寸为 **N** 的[正方形矩阵**mat【】【】**T3】和整数 **K** ，任务是将矩阵旋转 90 度 **K** 次，而不改变对角元素的位置。](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/)

**示例:**

> **输入:** mat[][] = {{1，2，3，4，5}，{6，7，8，9，10}，{11，12，13，14，15}，{16，17，18，19，20}，{21，22，23，24，25}}，K = 1
> **输出:**
> 1 16 11 6 5
> 22 7 12 9 2
> 22
> 
> **输入:** mat[][] = {{10，11}，{12，13}}，K = 2
> T3】输出:T5】10 11
> 12 13

**方法:**利用本文[讨论的思路](https://www.geeksforgeeks.org/rotate-a-matrix-by-90-degree-in-clockwise-direction-without-using-any-extra-space/)和矩阵顺时针旋转 4 次后恢复的事实，可以解决给定的问题。按照以下步骤解决给定的问题:

*   将 **K** 的值更新为 **K % 4** 。
*   迭代直到 [**K** 为正](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-sum-of-k-distinct-positive-integers/)并执行以下步骤:
    *   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，对于范围**【0，N/2】**和范围**【0，N–I–1】**上的 **i** ，执行以下步骤:
    *   如果**的值我！= j** 和 **(i + j)！=(N–1)**，然后执行以下步骤:
        *   将**mat【I】【j】**的值存储在临时变量 **temp** 中。
        *   将 **mat[i][j]** 的值更新为**mat[N–1–j][I]**。
        *   将**mat[N–1–j][I]**的值更新为**mat[N–1-I][N–1–j]**。
        *   将**mat[N–1–I][N–1–j]**的值更新为**mat[j][N–1–I]**。
        *   将**mat[j][N–1–I]**的值更新为**温度**。
*   完成上述步骤后，打印获得的更新矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the matrix
void print(vector<vector<int> >& mat)
{
    // Iterate over the rows
    for (int i = 0; i < mat.size(); i++) {

        // Iterate over the columns
        for (int j = 0; j < mat[0].size(); j++)

            // Print the value
            cout << setw(3) << mat[i][j];
        cout << "\n";
    }
}

// Function to perform the swapping of
// matrix elements in clockwise manner
void performSwap(vector<vector<int> >& mat,
                 int i, int j)
{
    int N = mat.size();

    // Stores the last row
    int ei = N - 1 - i;

    // Stores the last column
    int ej = N - 1 - j;

    // Perform the swaps
    int temp = mat[i][j];
    mat[i][j] = mat[ej][i];
    mat[ej][i] = mat[ei][ej];
    mat[ei][ej] = mat[j][ei];
    mat[j][ei] = temp;
}

// Function to rotate non - diagonal
// elements of the matrix K times in
// clockwise direction
void rotate(vector<vector<int> >& mat,
            int N, int K)
{
    // Update K to K % 4
    K = K % 4;

    // Iterate until K is positive
    while (K--) {

        // Iterate each up to N/2-th row
        for (int i = 0; i < N / 2; i++) {

            // Iterate each column
            // from i to N - i - 1
            for (int j = i;
                 j < N - i - 1; j++) {

                // Check if the element
                // at i, j is not a
                // diagonal element
                if (i != j
                    && (i + j) != N - 1) {

                    // Perform the swapping
                    performSwap(mat, i, j);
                }
            }
        }
    }

    // Print the matrix
    print(mat);
}

// Driver Code
int main()
{
    int K = 5;
    vector<vector<int> > mat = {
        { 1, 2, 3, 4 },
        { 6, 7, 8, 9 },
        { 11, 12, 13, 14 },
        { 16, 17, 18, 19 },
    };
    int N = mat.size();
    rotate(mat, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to print the matrix
    static void print(int mat[][])
    {
        // Iterate over the rows
        for (int i = 0; i < mat.length; i++) {

            // Iterate over the columns
            for (int j = 0; j < mat[0].length; j++)

                // Print the value
                System.out.print(mat[i][j] + " ");

            System.out.println();
        }
    }

    // Function to perform the swapping of
    // matrix elements in clockwise manner
    static void performSwap(int mat[][], int i, int j)
    {
        int N = mat.length;

        // Stores the last row
        int ei = N - 1 - i;

        // Stores the last column
        int ej = N - 1 - j;

        // Perform the swaps
        int temp = mat[i][j];
        mat[i][j] = mat[ej][i];
        mat[ej][i] = mat[ei][ej];
        mat[ei][ej] = mat[j][ei];
        mat[j][ei] = temp;
    }

    // Function to rotate non - diagonal
    // elements of the matrix K times in
    // clockwise direction
    static void rotate(int mat[][], int N, int K)
    {
        // Update K to K % 4
        K = K % 4;

        // Iterate until K is positive
        while (K-- > 0) {

            // Iterate each up to N/2-th row
            for (int i = 0; i < N / 2; i++) {

                // Iterate each column
                // from i to N - i - 1
                for (int j = i; j < N - i - 1; j++) {

                    // Check if the element
                    // at i, j is not a
                    // diagonal element
                    if (i != j && (i + j) != N - 1) {

                        // Perform the swapping
                        performSwap(mat, i, j);
                    }
                }
            }
        }

        // Print the matrix
        print(mat);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int K = 5;
        int mat[][] = {
            { 1, 2, 3, 4 },
            { 6, 7, 8, 9 },
            { 11, 12, 13, 14 },
            { 16, 17, 18, 19 },
        };

        int N = mat.length;
        rotate(mat, N, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the matrix
def printMat(mat):

    # Iterate over the rows
    for i in range(len(mat)):

        # Iterate over the columns
        for j in range(len(mat[0])):

            # Print the value
            print(mat[i][j], end = " ")

        print()

# Function to perform the swapping of
# matrix elements in clockwise manner
def performSwap(mat, i, j):

    N = len(mat)

    # Stores the last row
    ei = N - 1 - i

    # Stores the last column
    ej = N - 1 - j

    # Perform the swaps
    temp = mat[i][j]
    mat[i][j] = mat[ej][i]
    mat[ej][i] = mat[ei][ej]
    mat[ei][ej] = mat[j][ei]
    mat[j][ei] = temp

# Function to rotate non - diagonal
# elements of the matrix K times in
# clockwise direction
def rotate(mat, N, K):

    # Update K to K % 4
    K = K % 4

    # Iterate until K is positive
    while (K > 0):

        # Iterate each up to N/2-th row
        for i in range(int(N / 2)):

            # Iterate each column
            # from i to N - i - 1
            for j in range(i, N - i - 1):

                # Check if the element
                # at i, j is not a
                # diagonal element
                if (i != j and (i + j) != N - 1):

                    # Perform the swapping
                    performSwap(mat, i, j)

        K -= 1

    # Print the matrix
    printMat(mat)

# Driver Code
K = 5
mat = [ [ 1, 2, 3, 4 ],
        [ 6, 7, 8, 9 ],
        [ 11, 12, 13, 14 ],
        [ 16, 17, 18, 19 ] ]
N = len(mat)

rotate(mat, N, K)

# This code is contributed by Dharanendra L V.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to print the matrix
    static void print(int[, ] mat)
    {
        // Iterate over the rows
        for (int i = 0; i < mat.GetLength(0); i++) {

            // Iterate over the columns
            for (int j = 0; j < mat.GetLength(1); j++)

                // Print the value
                Console.Write(mat[i, j] + " ");

            Console.WriteLine();
        }
    }

    // Function to perform the swapping of
    // matrix elements in clockwise manner
    static void performSwap(int[, ] mat, int i, int j)
    {
        int N = mat.GetLength(0);

        // Stores the last row
        int ei = N - 1 - i;

        // Stores the last column
        int ej = N - 1 - j;

        // Perform the swaps
        int temp = mat[i, j];
        mat[i, j] = mat[ej, i];
        mat[ej, i] = mat[ei, ej];
        mat[ei, ej] = mat[j, ei];
        mat[j, ei] = temp;
    }

    // Function to rotate non - diagonal
    // elements of the matrix K times in
    // clockwise direction
    static void rotate(int[, ] mat, int N, int K)
    {
        // Update K to K % 4
        K = K % 4;

        // Iterate until K is positive
        while (K-- > 0) {

            // Iterate each up to N/2-th row
            for (int i = 0; i < N / 2; i++) {

                // Iterate each column
                // from i to N - i - 1
                for (int j = i; j < N - i - 1; j++) {

                    // Check if the element
                    // at i, j is not a
                    // diagonal element
                    if (i != j && (i + j) != N - 1) {

                        // Perform the swapping
                        performSwap(mat, i, j);
                    }
                }
            }
        }

        // Print the matrix
        print(mat);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int K = 5;
        int[, ] mat = {
            { 1, 2, 3, 4 },
            { 6, 7, 8, 9 },
            { 11, 12, 13, 14 },
            { 16, 17, 18, 19 },
        };

        int N = mat.GetLength(0);
        rotate(mat, N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

   // Function to print the matrix
    function print(mat)
    {
        // Iterate over the rows
        for (let i = 0; i < mat.length; i++) {

            // Iterate over the columns
            for (let j = 0; j < mat[0].length; j++)

                // Print the value
                document.write(mat[i][j] + " ");

            document.write("<br/>");
        }
    }

    // Function to perform the swapping of
    // matrix elements in clockwise manner
    function performSwap(mat, i, j)
    {
        let N = mat.length;

        // Stores the last row
        let ei = N - 1 - i;

        // Stores the last column
        let ej = N - 1 - j;

        // Perform the swaps
        let temp = mat[i][j];
        mat[i][j] = mat[ej][i];
        mat[ej][i] = mat[ei][ej];
        mat[ei][ej] = mat[j][ei];
        mat[j][ei] = temp;
    }

    // Function to rotate non - diagonal
    // elements of the matrix K times in
    // clockwise direction
    function rotate(mat, N, K)
    {
        // Update K to K % 4
        K = K % 4;

        // Iterate until K is positive
        while (K-- > 0) {

            // Iterate each up to N/2-th row
            for (let i = 0; i < N / 2; i++) {

                // Iterate each column
                // from i to N - i - 1
                for (let j = i; j < N - i - 1; j++) {

                    // Check if the element
                    // at i, j is not a
                    // diagonal element
                    if (i != j && (i + j) != N - 1) {

                        // Perform the swapping
                        performSwap(mat, i, j);
                    }
                }
            }
        }

        // Print the matrix
        print(mat);
    }

  // Driver Code

     let K = 5;
        let mat = [
            [ 1, 2, 3, 4 ],
            [ 6, 7, 8, 9 ],
            [ 11, 12, 13, 14 ],
            [ 16, 17, 18, 19 ],
        ];

        let N = mat.length;
        rotate(mat, N, K);

</script>
```

**Output:** 

```
  1 11  6  4
 17  7  8  2
 18 12 13  3
 16 14  9 19
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*