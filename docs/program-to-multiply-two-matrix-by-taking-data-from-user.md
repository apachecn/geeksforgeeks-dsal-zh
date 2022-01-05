# 通过从用户处获取数据来对两个矩阵相乘的程序

> 原文:[https://www . geesforgeks . org/program-to-two-matrix-by-take-data-from-user/](https://www.geeksforgeeks.org/program-to-multiply-two-matrix-by-taking-data-from-user/)

给定两个矩阵，任务是将它们相乘。矩阵元素的大小和数量将从键盘上读取。

**示例:**

```
Input: row1 = 2, col1 = 2,
       mat1[][] = {{1, 2}, 
                   {3, 4}},
       row2 = 2, col2 = 2,
       mat2[][] = {{1, 1}, 
                   {1, 1}}
Output: {{3, 3}, 
         {7, 7}}
Input: row1 = 2, col1 = 2,
       mat1[][] = {{2, 4}, 
                   {3, 4}}
       row1 = 2, col1 = 2,
       mat2[][] = {{1, 2}, 
                   {1, 3}}       
Output: {{6, 16}, 
         {7, 18}}
```

![](img/f817ce00b9c904bc4fa28109e9094336.png)

**程序:**

## C

```
// C program to multiply two matrices.

#include <stdio.h>

const int MAX = 100;

// Function to print Matrix
void printMatrix(int M[][MAX], int rowSize, int colSize)
{
    for (int i = 0; i < rowSize; i++) {
        for (int j = 0; j < colSize; j++)
            printf("%d ", M[i][j]);

        printf("\n");
    }
}

// Function to multiply two matrices A[][] and B[][]
void multiplyMatrix(int row1, int col1, int A[][MAX],
                    int row2, int col2, int B[][MAX])
{
    int i, j, k;

    // Matrix to store the result
    int C[MAX][MAX];

    // Check if multiplication is Possible
    if (row2 != col1) {
        printf("Not Possible\n");
        return;
    }

    // Multiply the two
    for (i = 0; i < row1; i++) {
        for (j = 0; j < col2; j++) {
            C[i][j] = 0;
            for (k = 0; k < row2; k++)
                C[i][j] += A[i][k] * B[k][j];
        }
    }

    // Print the result
    printf("\nResultant Matrix: \n");
    printMatrix(C, row1, col2);
}

// Driven Program
int main()
{
    int row1, col1, row2, col2, i, j;
    int A[MAX][MAX], B[MAX][MAX];

    // Read size of Matrix A from user
    printf("Enter the number of rows of First Matrix: ");
    scanf("%d", &row1);
    printf("%d", row1);
    printf("\nEnter the number of columns of First Matrix: ");
    scanf("%d", &col1);
    printf("%d", col1);

    // Read the elements of Matrix A from user
    printf("\nEnter the elements of First Matrix: ");
    for (i = 0; i < row1; i++) {
        for (j = 0; j < col1; j++) {
            printf("\nA[%d][%d]: ", i, j);
            scanf("%d", &A[i][j]);
            printf("%d", A[i][j]);
        }
    }

    // Read size of Matrix B from user
    printf("\nEnter the number of rows of Second Matrix: ");
    scanf("%d", &row2);
    printf("%d", row2);
    printf("\nEnter the number of columns of Second Matrix: ");
    scanf("%d", &col2);
    printf("%d", col2);

    // Read the elements of Matrix B from user
    printf("\nEnter the elements of First Matrix: ");
    for (i = 0; i < row2; i++) {
        for (j = 0; j < col2; j++) {
            printf("\nB[%d][%d]: ", i, j);
            scanf("%d", &B[i][j]);
            printf("%d", B[i][j]);
        }
    }

    // Print the Matrix A
    printf("\n\nFirst Matrix: \n");
    printMatrix(A, row1, col1);

    // Print the Matrix B
    printf("\nSecond Matrix: \n");
    printMatrix(B, row2, col2);

    // Find the product of the 2 matrices
    multiplyMatrix(row1, col1, A, row2, col2, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two matrices.
import java.io.*;
import java.util.*;

class GFG{

static int MAX = 100;

// Function to print Matrix
static void printMatrix(int M[][], int rowSize,
                        int colSize)
{
    for(int i = 0; i < rowSize; i++)
    {
        for(int j = 0; j < colSize; j++)
            System.out.print(M[i][j] + " ");

        System.out.println();
    }
}

// Function to multiply two matrices A[][] and B[][]
static void multiplyMatrix(int row1, int col1,
                           int A[][], int row2,
                           int col2, int B[][])
{
    int i, j, k;

    // Matrix to store the result
    int C[][] = new int[MAX][MAX];

    // Check if multiplication is Possible
    if (row2 != col1)
    {
        System.out.println("Not Possible");
        return;
    }

    // Multiply the two
    for(i = 0; i < row1; i++)
    {
        for(j = 0; j < col2; j++)
        {
            C[i][j] = 0;
            for(k = 0; k < row2; k++)
                C[i][j] += A[i][k] * B[k][j];
        }
    }

    // Print the result
      System.out.println();
    System.out.println("Resultant Matrix: ");
    printMatrix(C, row1, col2);
}

// Driver code
public static void main(String[] args)
{
    Scanner read = new Scanner(System.in);
    int row1, col1, row2, col2, i, j;
    int A[][] = new int[MAX][MAX];
    int B[][] = new int[MAX][MAX];

    // Read size of Matrix A from user
    System.out.print("Enter the number of " +
                     "rows of First Matrix: ");
    row1 = read.nextInt();
    System.out.println(row1);
    System.out.print("Enter the number of " +
                     "columns of First Matrix: ");
    col1 = read.nextInt();
    System.out.println(col1);

    // Read the elements of Matrix A from user
    System.out.println("Enter the elements " +
                       "of First Matrix: ");
    for(i = 0; i < row1; i++)
    {
        for(j = 0; j < col1; j++)
        {
            System.out.print("A[" + i + "][" +
                                    j + "]: ");
            A[i][j] = read.nextInt();
            System.out.println(A[i][j]);
        }
    }

    // Read size of Matrix B from user
    System.out.print("Enter the number of " +
                     "rows of Second Matrix: ");
    row2 = read.nextInt();
    System.out.println(row2);
    System.out.print("Enter the number of " +
                     "columns of Second Matrix: ");
    col2 = read.nextInt();
    System.out.println(col2);

    // Read the elements of Matrix B from user
    System.out.println("Enter the elements " +
                       "of First Matrix: ");
    for(i = 0; i < row2; i++)
    {
        for(j = 0; j < col2; j++)
        {
            System.out.print("A[" + i + "][" +
                                    j + "]: ");
            B[i][j] = read.nextInt();
            System.out.println(B[i][j]);
        }
    }

    // Print the Matrix A
    System.out.println();
    System.out.println("First Matrix: ");
    printMatrix(A, row1, col1);

    // Print the Matrix B
      System.out.println();
    System.out.println("Second Matrix: ");
    printMatrix(B, row2, col2);

    // Find the product of the 2 matrices
    multiplyMatrix(row1, col1, A, row2, col2, B);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program to multiply two matrices.
MAX = 100

# Function to print Matrix
def printMatrix(M, rowSize, colSize) :

    for i in range(rowSize) :
        for j in range(colSize) :
            print(M[i][j], end = " ")

        print()

# Function to multiply two matrices
# A[][] and B[][]
def multiplyMatrix(row1, col1, A,
                   row2, col2, B) :

    # Matrix to store the result
    C = [[0 for i in range(MAX)]
            for j in range(MAX)]

    # Check if multiplication is Possible
    if (row2 != col1) :
        print("Not Possible")
        return

    # Multiply the two
    for i in range(row1) :
        for j in range(col2) :
            C[i][j] = 0
            for k in range(row2) :
                C[i][j] += A[i][k] * B[k][j];

    # Print the result
    print("Resultant Matrix: ")
    printMatrix(C, row1, col2)

# Driver Code
if __name__ == "__main__" :

    A = [[0 for i in range(MAX)]
            for j in range(MAX)]
    B = [[0 for i in range(MAX)]
            for j in range(MAX)]

    # Read size of Matrix A from user
    row1 = int(input("Enter the number of rows of First Matrix: "))
    col1 = int(input("Enter the number of columns of First Matrix: "))

    # Read the elements of Matrix A from user
    print("Enter the elements of First Matrix: ");
    for i in range(row1) :
        for j in range(col1) :
            A[i][j] = int(input("A[" + str(i) +
                                "][" + str(j) + "]: "))

    # Read size of Matrix B from user
    row2 = int(input("Enter the number of rows of Second Matrix: "))
    col2 = int(input("Enter the number of columns of Second Matrix: "))

    # Read the elements of Matrix B from user
    print("Enter the elements of Second Matrix: ");
    for i in range(row2) :
        for j in range(col2) :
            B[i][j] = int(input("B[" + str(i) +
                                "][" + str(j) + "]: "))

    # Print the Matrix A
    print("First Matrix: ")
    printMatrix(A, row1, col1)

    # Print the Matrix B
    print("Second Matrix: ")
    printMatrix(B, row2, col2)

    # Find the product of the 2 matrices
    multiplyMatrix(row1, col1, A, row2, col2, B)

# This code is contributed by Ryuga
```

**Output:** 

```
Enter the number of rows of First Matrix: 2
Enter the number of columns of First Matrix: 3
Enter the elements of First Matrix: 
A[0][0]: 1
A[0][1]: 2
A[0][2]: 3
A[1][0]: 4
A[1][1]: 5
A[1][2]: 6
Enter the number of rows of Second Matrix: 3
Enter the number of columns of Second Matrix: 2
Enter the elements of First Matrix: 
B[0][0]: 1
B[0][1]: 2
B[1][0]: 3
B[1][1]: 4
B[2][0]: 5
B[2][1]: 6

First Matrix: 
1 2 3 
4 5 6 

Second Matrix: 
1 2 
3 4 
5 6 

Resultant Matrix: 
22 28 
49 64 
```

**时间复杂度:**O(row 1 * col 2 * row 2)
T3】辅助空间: O(row1 * col2)