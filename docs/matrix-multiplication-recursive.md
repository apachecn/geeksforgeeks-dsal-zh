# 矩阵乘法 | 递归

> 原文： [https://www.geeksforgeeks.org/matrix-multiplication-recursive/](https://www.geeksforgeeks.org/matrix-multiplication-recursive/)

给定两个矩阵`A`和`B`。任务是递归地将矩阵`A`和矩阵`B`相乘。 如果矩阵`A`和矩阵`B`不兼容乘法，则生成输出`"Not Possible"`。

**示例**：

```
Input: A = 12 56
           45 78
       B = 2 6
           5 8
Output: 304 520
        480 894

Input: A = 1 2 3
           4 5 6
           7 8 9
       B = 1 2 3
           4 5 6
           7 8 9

Output: 30  36  42  
        66  81  96  
       102 126 150  

```



建议首先参考[迭代式矩阵乘法](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)。

首先检查矩阵之间的乘法是否可行。 为此，请检查第一矩阵的列数是否等于第二矩阵的行数。 如果两者相等，则继续操作，否则生成输出`"Not Possible"`。

在递归矩阵乘法中，我们通过递归调用实现了三个迭代循环。`multipleMatrix()`的最内层递归调用是迭代`k`（`col1`或`row2`）。 第二个`multipleMatrix()`的递归调用将更改列，最外面的递归调用将更改行。

以下是递归矩阵乘法代码。

## C/C++ 

```cpp

// Recursive code for Matrix Multiplication 
#include <stdio.h> 

const int MAX = 100; 

void multiplyMatrixRec(int row1, int col1, int A[][MAX], 
                       int row2, int col2, int B[][MAX], 
                       int C[][MAX]) 
{ 
    // Note that below variables are static 
    // i and j are used to know current cell of 
    // result matrix C[][]. k is used to know 
    // current column number of A[][] and row 
    // number of B[][] to be multiplied 
    static int i = 0, j = 0, k = 0; 

    // If all rows traversed. 
    if (i >= row1) 
        return; 

    // If i < row1 
    if (j < col2) 
    { 
      if (k < col1) 
      { 
         C[i][j] += A[i][k] * B[k][j]; 
         k++; 

         multiplyMatrixRec(row1, col1, A, row2, col2, 
                                               B, C); 
      } 

      k = 0; 
      j++; 
      multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 
    } 

    j = 0; 
    i++; 
    multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 
} 

// Function to multiply two matrices A[][] and B[][] 
void multiplyMatrix(int row1, int col1, int A[][MAX], 
                    int row2, int col2, int B[][MAX]) 
{ 
    if (row2 != col1) 
    { 
        printf("Not Possible\n"); 
        return; 
    } 

    int C[MAX][MAX] = {0}; 

    multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 

    // Print the result 
    for (int i = 0; i < row1; i++) 
    { 
        for (int j = 0; j < col2; j++) 
            printf("%d  ", C[i][j]); 

        printf("\n"); 
    } 
} 

// Driven Program 
int main() 
{ 
    int A[][MAX] = { {1, 2, 3}, 
                    {4, 5, 6}, 
                    {7, 8, 9}}; 

    int B[][MAX] = { {1, 2, 3}, 
                    {4, 5, 6}, 
                    {7, 8, 9} }; 

    int row1 = 3, col1 = 3, row2 = 3, col2 = 3; 
    multiplyMatrix(row1, col1, A, row2, col2, B); 

    return 0; 
} 

```

## Java

```java

// Java recursive code for Matrix Multiplication 

class GFG  
{ 
    public static int MAX = 100; 

    // Note that below variables are static 
    // i and j are used to know current cell of 
    // result matrix C[][]. k is used to know 
    // current column number of A[][] and row 
    // number of B[][] to be multiplied 
    public static int i = 0, j = 0, k = 0; 

    static void multiplyMatrixRec(int row1, int col1, int A[][], 
                       int row2, int col2, int B[][], 
                       int C[][]) 
    { 
        // If all rows traversed 
        if (i >= row1) 
            return; 

        // If i < row1 
        if (j < col2) 
        { 
            if (k < col1) 
            { 
                C[i][j] += A[i][k] * B[k][j]; 
                k++; 

                multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 
            } 

            k = 0; 
            j++; 
            multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 
        } 

        j = 0; 
        i++; 
        multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 
    } 

    // Function to multiply two matrices A[][] and B[][] 
    static void multiplyMatrix(int row1, int col1, int A[][], 
                    int row2, int col2, int B[][]) 
    { 
        if (row2 != col1) 
        { 
            System.out.println("Not Possible\n"); 
            return; 
        } 

        int[][] C = new int[MAX][MAX]; 

        multiplyMatrixRec(row1, col1, A, row2, col2, B, C); 

        // Print the result 
        for (int i = 0; i < row1; i++) 
        { 
            for (int j = 0; j < col2; j++) 
                System.out.print(C[i][j]+" "); 

            System.out.println(); 
        } 
    } 

    // driver program 
    public static void main (String[] args)  
    { 
        int row1 = 3, col1 = 3, row2 = 3, col2 = 3; 
        int A[][] = { {1, 2, 3}, 
                      {4, 5, 6}, 
                      {7, 8, 9}}; 

        int B[][] = { {1, 2, 3}, 
                      {4, 5, 6}, 
                      {7, 8, 9} }; 

        multiplyMatrix(row1, col1, A, row2, col2, B); 
    } 
} 

// Contributed by Pramod Kumar 

```

## Python3

```py

# Recursive code for Matrix Multiplication  
MAX = 100
i = 0
j = 0
k = 0

def multiplyMatrixRec(row1, col1, A,  
                      row2, col2, B, C):  

    # Note that below variables are static  
    # i and j are used to know current cell of  
    # result matrix C[][]. k is used to know  
    # current column number of A[][] and row  
    # number of B[][] to be multiplied  
    global i 
    global j 
    global k 

    # If all rows traversed.  
    if (i >= row1):  
        return

    # If i < row1  
    if (j < col2): 
        if (k < col1): 
            C[i][j] += A[i][k] * B[k][j] 
            k += 1
            multiplyMatrixRec(row1, col1, A,  
                              row2, col2,B, C) 

        k = 0
        j += 1
        multiplyMatrixRec(row1, col1, A, 
                          row2, col2, B, C) 

    j = 0
    i += 1
    multiplyMatrixRec(row1, col1, A,  
                      row2, col2, B, C) 

# Function to multiply two matrices  
# A[][] and B[][]  
def multiplyMatrix(row1, col1, A, row2, col2, B):  
    if (row2 != col1):  
        print("Not Possible")  
        return

    C = [[0 for i in range(MAX)] 
            for i in range(MAX)] 
    multiplyMatrixRec(row1, col1, A,  
                      row2, col2, B, C)  

    # Print the result  
    for i in range(row1):  
        for j in range(col2): 
            print( C[i][j], end = " ")  
        print()  

# Driver Code 
A = [[1, 2, 3], 
     [4, 5, 6], 
     [7, 8, 9]]  
B = [[1, 2, 3], 
     [4, 5, 6], 
     [7, 8, 9]]  

row1 = 3
col1 = 3
row2 = 3
col2 = 3
multiplyMatrix(row1, col1, A, row2, col2, B)  

# This code is contributed by sahilshelangia 

```

## C# 

```cs

// C# recursive code for  
// Matrix Multiplication 
using System; 

class GFG 
{ 
    public static int MAX = 100; 

    // Note that below variables 
    // are static i and j are used  
    // to know current cell of result  
    // matrix C[][]. k is used to 
    // know current column number of  
    // A[][] and row number of B[][] 
    // to be multiplied 
    public static int i = 0, j = 0, k = 0; 

    static void multiplyMatrixRec(int row1, int col1,  
                                  int [,]A, int row2,  
                                  int col2, int [,]B, 
                                  int [,]C) 
    { 
        // If all rows traversed 
        if (i >= row1) 
            return; 

        // If i < row1 
        if (j < col2) 
        { 
            if (k < col1) 
            { 
                C[i, j] += A[i, k] * B[k, j]; 
                k++; 

                multiplyMatrixRec(row1, col1, A,  
                                  row2, col2, B, C); 
            } 

            k = 0; 
            j++; 
            multiplyMatrixRec(row1, col1, A,  
                              row2, col2, B, C); 
        } 

        j = 0; 
        i++; 
        multiplyMatrixRec(row1, col1, A,  
                          row2, col2, B, C); 
    } 

    // Function to multiply two 
    // matrices A[][] and B[][] 
    static void multiplyMatrix(int row1, int col1,  
                               int [,]A, int row2,  
                               int col2, int [,]B) 
    { 
        if (row2 != col1) 
        { 
            Console.WriteLine("Not Possible\n"); 
            return; 
        } 

        int[,]C = new int[MAX, MAX]; 

        multiplyMatrixRec(row1, col1, A,  
                          row2, col2, B, C); 

        // Print the result 
        for (int i = 0; i < row1; i++) 
        { 
            for (int j = 0; j < col2; j++) 
                Console.Write(C[i, j] + " "); 

            Console.WriteLine(); 
        } 
    } 

    // Driver Code 
    static public void Main () 
    { 
        int row1 = 3, col1 = 3,  
            row2 = 3, col2 = 3; 
        int [,]A = {{1, 2, 3}, 
                    {4, 5, 6}, 
                    {7, 8, 9}}; 

        int [,]B = {{1, 2, 3}, 
                    {4, 5, 6}, 
                    {7, 8, 9}}; 

        multiplyMatrix(row1, col1, A,  
                       row2, col2, B); 
    } 
} 

// This code is contributed by m_kit 

```

**输出**：

```
30  36  42  
66  81  96  
102  126  150  

```

