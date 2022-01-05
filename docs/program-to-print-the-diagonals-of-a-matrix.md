# 打印矩阵对角线的程序

> 原文:[https://www . geesforgeks . org/program-to-print-a-matrix 的对角线/](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)

给定一个 2D 方阵，打印主对角线和次对角线。

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

例如，考虑下面的 4 X 4 输入矩阵。

```
A00 A01 A02 A03
A10 A11 A12 A13
A20 A21 A22 A23
A30 A31 A32 A33
```

*   主对角线由元素 A00、A11、A22、A33 形成。
    主对角线的条件:

```
The row-column condition is row = column.
```

*   次对角线由元件 A03、A12、A21、A30 形成。
    二次对角线的条件:

```
The row-column condition is row = numberOfRows - column -1.
```

**<u>方法 1:</u>**
在这个方法中，我们使用两个循环，即列循环和行循环，在内部循环中，我们检查上述条件。

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
        for (int j = 0; j < n; j++) {

            // Condition for principal diagonal
            if (i == j)
                cout << mat[i][j] << ", ";
        }
    }
    cout << endl;
}

// Function to print the Secondary Diagonal
void printSecondaryDiagonal(int mat[][MAX], int n)
{
    cout << "Secondary Diagonal: ";

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // Condition for secondary diagonal
            if ((i + j) == (n - 1))
                cout << mat[i][j] << ", ";
        }
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
class GFG {
    static int MAX = 100;

    // Function to print the Principal Diagonal
    static void printPrincipalDiagonal(int mat[][], int n)
    {
        System.out.print("Principal Diagonal: ");

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Condition for principal diagonal
                if (i == j) {
                    System.out.print(mat[i][j] + ", ");
                }
            }
        }
        System.out.println("");
    }

    // Function to print the Secondary Diagonal
    static void printSecondaryDiagonal(int mat[][], int n)
    {
        System.out.print("Secondary Diagonal: ");

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Condition for secondary diagonal
                if ((i + j) == (n - 1)) {
                    System.out.print(mat[i][j] + ", ");
                }
            }
        }
        System.out.println("");
    }

    // Driver code
    public static void main(String args[])
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

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to print the Diagonals of a Matrix
MAX = 100

# Function to print the Principal Diagonal
def printPrincipalDiagonal(mat, n):
    print("Principal Diagonal: ", end = "")

    for i in range(n):
        for j in range(n):

            # Condition for principal diagonal
            if (i == j):
                print(mat[i][j], end = ", ")
    print()

# Function to print the Secondary Diagonal
def printSecondaryDiagonal(mat, n):
    print("Secondary Diagonal: ", end = "")

    for i in range(n):
        for j in range(n):

            # Condition for secondary diagonal
            if ((i + j) == (n - 1)):
                print(mat[i][j], end = ", ")
    print()

# Driver code
n = 4
a = [[ 1, 2, 3, 4 ],
     [ 5, 6, 7, 8 ],
     [ 1, 2, 3, 4 ],
     [ 5, 6, 7, 8 ]]

printPrincipalDiagonal(a, n)
printSecondaryDiagonal(a, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to print the Diagonals of a Matrix
using System;

class GFG {
    static int MAX = 100;

    // Function to print the Principal Diagonal
    static void printPrincipalDiagonal(int[, ] mat, int n)
    {
        Console.Write("Principal Diagonal: ");

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Condition for principal diagonal
                if (i == j) {
                    Console.Write(mat[i, j] + ", ");
                }
            }
        }
        Console.WriteLine("");
    }

    // Function to print the Secondary Diagonal
    static void printSecondaryDiagonal(int[, ] mat, int n)
    {
        Console.Write("Secondary Diagonal: ");

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Condition for secondary diagonal
                if ((i + j) == (n - 1)) {
                    Console.Write(mat[i, j] + ", ");
                }
            }
        }
        Console.WriteLine("");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4;
        int[, ] a = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 } };

        printPrincipalDiagonal(a, n);
        printSecondaryDiagonal(a, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript Program to print the Diagonals of a Matrix

    let MAX = 100;

    // Function to print the Principal Diagonal
    function printPrincipalDiagonal(mat, n)
    {
        document.write("Principal Diagonal: ");

        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {

                // Condition for principal diagonal
                if (i == j) {
                    document.write(mat[i][j] + ", ");
                }
            }
        }
        document.write("</br>");
    }

    // Function to print the Secondary Diagonal
    function printSecondaryDiagonal(mat, n)
    {
        document.write("Secondary Diagonal: ");

        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {

                // Condition for secondary diagonal
                if ((i + j) == (n - 1)) {
                    document.write(mat[i][j] + ", ");
                }
            }
        }
        document.write("</br>");
    }

    let n = 4;
    let a = [ [ 1, 2, 3, 4 ],
              [ 5, 6, 7, 8 ],
              [ 1, 2, 3, 4 ],
              [ 5, 6, 7, 8 ] ];

    printPrincipalDiagonal(a, n);
    printSecondaryDiagonal(a, n);

</script>
```

**Output:** 

```
Principal Diagonal: 1, 6, 3, 8, 
Secondary Diagonal: 4, 7, 2, 5,
```

**复杂度分析:**

*   **时间复杂度:** O(n <sup>2</sup> )。
    由于涉及嵌套循环，因此时间复杂度是平方的。
*   **辅助空间:** O(1)。
    因为没有多余的空间被占用。

**<u>方法 2:</u>**
在该方法中，使用单个 for 循环可以实现打印对角线元素的相同条件。
**进近:**

1.  **对于主对角线元素:**运行一个循环，直到 **n** ，其中 **n** 是**列数**，打印**数组【I】【I】**，其中 **i** 是索引变量。
2.  **对于次对角线元素:**运行一个循环直到 **n** ，其中 **n** 是列数，打印**数组【I】【k】**，其中 **i** 是索引变量， **k =数组 _ length–1**。降低 **k** 直到 **i < n** 。

下面是上述方法的实现。

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
        // Printing principal diagonal
        cout << mat[i][i] << ", ";
    }
    cout << endl;
}

// Function to print the Secondary Diagonal
void printSecondaryDiagonal(int mat[][MAX], int n)
{
    cout << "Secondary Diagonal: ";
    int k = n - 1;
    for (int i = 0; i < n; i++) {
        // Printing secondary diagonal
        cout << mat[i][k--] << ", ";
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

// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the
// Diagonals of a Matrix
class Main{

static int MAX = 100;

// Function to print the Principal Diagonal
public static void printPrincipalDiagonal(int mat[][],
                                          int n)
{
  System.out.print("Principal Diagonal: ");

  for (int i = 0; i < n; i++)
  {
    // Printing principal diagonal
    System.out.print(mat[i][i] + ", ");
  }
  System.out.println();
}

// Function to print the Secondary Diagonal
public static void printSecondaryDiagonal(int mat[][],
                                          int n)
{
  System.out.print("Secondary Diagonal: ");
  int k = n - 1;

  for (int i = 0; i < n; i++)
  {
    // Printing secondary diagonal
    System.out.print(mat[i][k--] + ", ");
  }
  System.out.println();
}

public static void main(String[] args)
{
  int n = 4;
  int a[][] = {{1, 2, 3, 4},
               {5, 6, 7, 8},
               {1, 2, 3, 4},
               {5, 6, 7, 8}};
  printPrincipalDiagonal(a, n);
  printSecondaryDiagonal(a, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to print the
# Diagonals of a Matrix
MAX = 100

# Function to print the Principal Diagonal
def printPrincipalDiagonal(mat, n):

    print("Principal Diagonal: ", end = "")

    for i in range(n):

        # Printing principal diagonal
        print(mat[i][i], end = ", ")

    print()

# Function to print the Secondary Diagonal
def printSecondaryDiagonal(mat, n):

    print("Secondary Diagonal: ", end = "")
    k = n - 1

    for i in range(n):

        # Printing secondary diagonal
        print(mat[i][k], end = ", ")
        k -= 1

    print()

# Driver Code
n = 4
a = [ [ 1, 2, 3, 4 ],
      [ 5, 6, 7, 8 ],
      [ 1, 2, 3, 4 ],
      [ 5, 6, 7, 8 ] ]

printPrincipalDiagonal(a, n)
printSecondaryDiagonal(a, n)

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to print the
// Principal Diagonal
static void printPrincipalDiagonal(int [,]mat,
                                   int n)
{
  Console.Write("Principal Diagonal: ");

  for (int i = 0; i < n; i++)
  {
    // Printing principal diagonal
    Console.Write(mat[i, i] + ", ");
  }
  Console.Write("\n");
}

// Function to print the
// Secondary Diagonal
static void printSecondaryDiagonal(int [,]mat,
                                   int n)
{
  Console.Write("Secondary Diagonal: ");
  int k = n - 1;

  for (int i = 0; i < n; i++)
  {
    // Printing secondary diagonal
    Console.Write(mat[i, k--] + ", ");
  }

  Console.Write("\n");
}

// Driver code
static void Main()
{
  int n = 4;
  int [,]a = {{1, 2, 3, 4},
              {5, 6, 7, 8},
              {1, 2, 3, 4},
              {5, 6, 7, 8}};
  printPrincipalDiagonal(a, n);
  printSecondaryDiagonal(a, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // Javascript Program to print the
    // Diagonals of a Matrix

    let MAX = 100;

    // Function to print the Principal Diagonal
    function printPrincipalDiagonal(mat, n)
    {
      document.write("Principal Diagonal: ");

      for (let i = 0; i < n; i++)
      {
        // Printing principal diagonal
        document.write(mat[i][i] + ", ");
      }
      document.write("</br>");
    }

    // Function to print the Secondary Diagonal
    function printSecondaryDiagonal(mat, n)
    {
      document.write("Secondary Diagonal: ");
      let k = n - 1;

      for (let i = 0; i < n; i++)
      {
        // Printing secondary diagonal
        document.write(mat[i][k--] + ", ");
      }
      document.write("</br>");
    }

    let n = 4;
    let a = [[1, 2, 3, 4],
             [5, 6, 7, 8],
             [1, 2, 3, 4],
             [5, 6, 7, 8]];
    printPrincipalDiagonal(a, n);
    printSecondaryDiagonal(a, n);

</script>
```

**Output:** 

```
Principal Diagonal: 1, 6, 3, 8, 
Secondary Diagonal: 4, 7, 2, 5,
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    因为只有一个循环，所以时间复杂度是线性的。
*   **辅助空间:** O(1)。
    因为没有多余的空间被占用。