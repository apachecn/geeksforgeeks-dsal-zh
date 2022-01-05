# 在 O(N)时间内打印矩阵对角线的程序

> 原文:[https://www . geesforgeks . org/program-to-print-the-of-time-in-matrix/](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix-in-on-time/)

给定一个 2D 方阵，任务是以 O(N)的时间复杂度打印这个矩阵的主对角线和次对角线。[O(N<sup>2</sup>时间请参考本文](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)。

**示例:**

```
Input: 
4
1 2 3 4
4 3 2 1
7 8 9 6
6 5 4 3
Output:
Principal Diagonal: 1, 3, 9, 3
Secondary Diagonal: 4, 2, 8, 6

Input:
3
1 1 1
1 1 1
1 1 1
Output:
Principal Diagonal: 1, 1, 1
Secondary Diagonal: 1, 1, 1
```

**进场:**

1.考虑下面的 4 X 4 输入矩阵。

```
A00 A01 A02 A03
A10 A11 A12 A13
A20 A21 A22 A23
A30 A31 A32 A33
```

2.主对角线由元素 A00、A11、A22、A33 形成。

主对角线的条件:

```
The row-column condition is row = column.
```

3.次对角线由元件 A03、A12、A21、A30 形成。

副对角线的条件:

```
The row-column condition is row = numberOfRows - column - 1.
```

在这种方法中，我们使用一个循环，即一个循环，根据下面的公式找到对角线元素:

```
principal diagonal = matrix[i][i];
secondary diagonal = matrix[i][n - i - 1];

where 0 <= i <= n
```

以下是上述方法的实现:

## C++

```
// C++ Program to print the Diagonals of a Matrix

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Function to print the Principal Diagonal
void printPrincipalDiagonal(int mat[][MAX], int n)
{
    cout << "Principal Diagonal: ";

    for (int i = 0; i < n; i++) {

        // Condition for principal diagonal
        cout << mat[i][i] << ", ";
    }
    cout << endl;
}

// Function to print the Secondary Diagonal
void printSecondaryDiagonal(int mat[][MAX], int n)
{
    cout << "Secondary Diagonal: ";

    for (int i = 0; i < n; i++) {

        // Condition for secondary diagonal
        cout << mat[i][n - i - 1] << ", ";
    }

    cout << endl;
}

// Driver code
int main()
{
    int n = 4;
    int a[][MAX] = { { 1, 2, 3, 4 },
                     { 5, 6, 7, 8 },
                     { 1, 2, 3, 4 },
                     { 5, 6, 7, 8 } };

    printPrincipalDiagonal(a, n);
    printSecondaryDiagonal(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the Diagonals of a Matrix
class GFG
{

    static final int MAX = 100;

    // Function to print the Principal Diagonal
    static void printPrincipalDiagonal(int mat[][], int n)
    {
        System.out.print("Principal Diagonal: ");

        for (int i = 0; i < n; i++)
        {

            // Condition for principal diagonal
            System.out.print(mat[i][i] + ", ");
        }
        System.out.println();
    }

    // Function to print the Secondary Diagonal
    static void printSecondaryDiagonal(int mat[][], int n)
    {
        System.out.print("Secondary Diagonal: ");

        for (int i = 0; i < n; i++)
        {

            // Condition for secondary diagonal
            System.out.print(mat[i][n - i - 1] + ", ");
        }

        System.out.println();
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 4;
        int a[][] = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 } };

        printPrincipalDiagonal(a, n);
        printSecondaryDiagonal(a, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python Program to print the Diagonals of a Matrix
MAX = 100;

# Function to print the Principal Diagonal
def printPrincipalDiagonal(mat, n):
    print("Principal Diagonal: ", end = "");

    for i in range(n):

        # Condition for principal diagonal
        print(mat[i][i], end= ", ");

    print();

# Function to print the Secondary Diagonal
def printSecondaryDiagonal(mat, n):
    print("Secondary Diagonal: ", end = "");

    for i in range(n):

        # Condition for secondary diagonal
        print(mat[i][n - i - 1], end = ", ");

    print();

# Driver code
if __name__ == '__main__':
    n = 4;
    a = [[ 1, 2, 3, 4 ],
        [ 5, 6, 7, 8 ],
        [ 1, 2, 3, 4 ],
        [ 5, 6, 7, 8 ]];

    printPrincipalDiagonal(a, n);
    printSecondaryDiagonal(a, n);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# Program to print the Diagonals of a Matrix
using System;

class GFG
{

    // Function to print the Principal Diagonal
    static void printPrincipalDiagonal(int [,]mat, int n)
    {
        Console.Write("Principal Diagonal: ");

        for (int i = 0; i < n; i++)
        {

            // Condition for principal diagonal
            Console.Write(mat[i, i] + ", ");
        }
        Console.WriteLine();
    }

    // Function to print the Secondary Diagonal
    static void printSecondaryDiagonal(int [,]mat, int n)
    {
        Console.Write("Secondary Diagonal: ");

        for (int i = 0; i < n; i++)
        {

            // Condition for secondary diagonal
            Console.Write(mat[i, n - i - 1] + ", ");
        }

        Console.WriteLine();
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        int [,]a = { { 1, 2, 3, 4 },
                     { 5, 6, 7, 8 },
                     { 1, 2, 3, 4 },
                     { 5, 6, 7, 8 } };

        printPrincipalDiagonal(a, n);
        printSecondaryDiagonal(a, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Java script Program to print the Diagonals of a Matrix
let MAX = 100;

    // Function to print the Principal Diagonal
    function printPrincipalDiagonal(mat,n)
    {
        document.write("Principal Diagonal: ");

        for (let i = 0; i < n; i++)
        {

            // Condition for principal diagonal
            document.write(mat[i][i] + ", ");
        }
        document.write("<br>");
    }

    // Function to print the Secondary Diagonal
    function printSecondaryDiagonal(mat,n)
    {
        document.write("Secondary Diagonal: ");

        for (let i = 0; i < n; i++)
        {

            // Condition for secondary diagonal
            document.write(mat[i][n - i - 1] + ", ");
        }

        document.write("<br>");
    }

    // Driver code

        let n = 4;
        let a = [[1, 2, 3, 4 ],
                        [ 5, 6, 7, 8 ],
                        [ 1, 2, 3, 4 ],
                        [ 5, 6, 7, 8 ]];

        printPrincipalDiagonal(a, n);
        printSecondaryDiagonal(a, n);

// This code is contributed by sravan kumar Gottumukklala
</script>
```

**Output:** 

```
Principal Diagonal: 1, 6, 3, 8, 
Secondary Diagonal: 4, 7, 2, 5,
```