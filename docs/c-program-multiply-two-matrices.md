# 将两个矩阵相乘的程序

> 原文： [https://www.geeksforgeeks.org/c-program-multiply-two-matrices/](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)

给定两个矩阵，将它们相乘的任务。 矩阵可以是正方形或矩形。

**示例**：

```
Input : mat1[][] = {{1, 2}, 
                   {3, 4}}
        mat2[][] = {{1, 1}, 
                    {1, 1}}
Output : {{3, 3}, 
          {7, 7}}
Input : mat1[][] = {{2, 4}, 
                    {3, 4}}
        mat2[][] = {{1, 2}, 
                    {1, 3}}       
Output : {{6, 16}, 
          {7, 18}}

```

![](img/f817ce00b9c904bc4fa28109e9094336.png)



**方阵的乘积**：

下面的程序将两个大小为`4 * 4`的方阵相乘，我们可以为不同的维数更改`N`。

## C++ 

```cpp

// C++ program to multiply  
// two square matrices. 
#include <iostream> 

using namespace std; 

#define N 4 

// This function multiplies  
// mat1[][] and mat2[][], and  
// stores the result in res[][] 
void multiply(int mat1[][N],  
              int mat2[][N],  
              int res[][N]) 
{ 
    int i, j, k; 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < N; j++) 
        { 
            res[i][j] = 0; 
            for (k = 0; k < N; k++) 
                res[i][j] += mat1[i][k] *  
                             mat2[k][j]; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int i, j; 
    int res[N][N]; // To store result 
    int mat1[N][N] = {{1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}, 
                      {4, 4, 4, 4}}; 

    int mat2[N][N] = {{1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}, 
                      {4, 4, 4, 4}}; 

    multiply(mat1, mat2, res); 

    cout << "Result matrix is \n"; 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < N; j++) 
        cout << res[i][j] << " "; 
        cout << "\n"; 
    } 

    return 0; 
} 

// This code is contributed 
// by Soumik Mondal 

```

## C

```c

// C program to multiply two square matrices. 
#include <stdio.h> 
#define N 4 

// This function multiplies mat1[][] and mat2[][], 
// and stores the result in res[][] 
void multiply(int mat1[][N], int mat2[][N], int res[][N]) 
{ 
    int i, j, k; 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < N; j++) 
        { 
            res[i][j] = 0; 
            for (k = 0; k < N; k++) 
                res[i][j] += mat1[i][k]*mat2[k][j]; 
        } 
    } 
} 

int main() 
{ 
    int mat1[N][N] = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}, 
                    {4, 4, 4, 4}}; 

    int mat2[N][N] = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}, 
                    {4, 4, 4, 4}}; 

    int res[N][N]; // To store result 
    int i, j; 
    multiply(mat1, mat2, res); 

    printf("Result matrix is \n"); 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < N; j++) 
           printf("%d ", res[i][j]); 
        printf("\n"); 
    } 

    return 0; 
} 

```

## Java

```java

// Java program to multiply two square 
// matrices. 
import java.io.*; 

class GFG { 

    static int N = 4; 

    // This function multiplies mat1[][] 
    // and mat2[][], and stores the result 
    // in res[][] 
    static void multiply(int mat1[][],  
                  int mat2[][], int res[][]) 
    { 
        int i, j, k; 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < N; j++) 
            { 
                res[i][j] = 0; 
                for (k = 0; k < N; k++) 
                    res[i][j] += mat1[i][k]  
                                * mat2[k][j]; 
            } 
        } 
    } 

    // Driver code 
    public static void main (String[] args)  
    { 
        int mat1[][] = { {1, 1, 1, 1}, 
                         {2, 2, 2, 2}, 
                         {3, 3, 3, 3}, 
                         {4, 4, 4, 4}}; 

        int mat2[][] = { {1, 1, 1, 1}, 
                         {2, 2, 2, 2}, 
                         {3, 3, 3, 3}, 
                         {4, 4, 4, 4}}; 

        // To store result 
        int res[][] = new int[N][N] ; 
        int i, j; 
        multiply(mat1, mat2, res); 

        System.out.println("Result matrix"
                                + " is "); 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < N; j++) 
                System.out.print( res[i][j] 
                                    + " "); 
            System.out.println(); 
        } 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python 3

```py

# 4x4 matrix multiplication using Python3 
# Function definition 
def matrix_multiplication(M,N): 
    # List to store matrix multiplication result 
    R = [[0, 0, 0, 0],  
        [0, 0, 0, 0],  
        [0, 0, 0, 0], 
        [0, 0, 0, 0]]  

    for i in range(0, 4):  
        for j in range(0, 4): 
            for k in range(0, 4):  
                R[i][j] += M[i][k] * N[k][j]  

    for i in range(0,4):  
        for j in range(0,4):  
            #if we use print(), by default cursor moves to next line each time,  
            #Now we can explicitly define ending character or sequence passing 
            #second parameter as end="<character or string>" 
            #syntax: print(<variable or value to print>, end="<ending with>") 
            #Here space (" ") is used to print a gape after printing  
            #each element of R 
            print(R[i][j],end=" ") 
        print("\n",end="") 

# First matrix. M is a list 
M = [[1, 1, 1, 1],  
    [2, 2, 2, 2],  
    [3, 3, 3, 3], 
    [4, 4, 4, 4]] 

# Second matrix. N is a list 
N = [[1, 1, 1, 1],  
    [2, 2, 2, 2],  
    [3, 3, 3, 3], 
    [4, 4, 4, 4]]  

# Call matrix_multiplication function 
matrix_multiplication(M,N) 

# This code is contributed by Santanu 

```

## C# 

```cs

// C# program to multiply two square 
// matrices. 
using System; 

class GFG { 

    static int N = 4; 

    // This function multiplies mat1[][] 
    // and mat2[][], and stores the result 
    // in res[][] 
    static void multiply(int[,] mat1,  
                int [,]mat2, int [,]res) 
    { 
        int i, j, k; 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < N; j++) 
            { 
                res[i,j] = 0; 
                for (k = 0; k < N; k++) 
                    res[i,j] += mat1[i,k]  
                                * mat2[k,j]; 
            } 
        } 
    } 

    // Driver code 
    public static void Main ()  
    { 
        int [,]mat1 = { {1, 1, 1, 1}, 
                        {2, 2, 2, 2}, 
                        {3, 3, 3, 3}, 
                        {4, 4, 4, 4}}; 

        int [,]mat2 = { {1, 1, 1, 1}, 
                        {2, 2, 2, 2}, 
                        {3, 3, 3, 3}, 
                        {4, 4, 4, 4}}; 

        // To store result 
        int [,]res = new int[N,N] ; 
        int i, j; 
        multiply(mat1, mat2, res); 

        Console.WriteLine("Result matrix"
                                + " is "); 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < N; j++) 
                Console.Write( res[i,j] 
                                    + " "); 
            Console.WriteLine(); 
        } 
    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// PHP program to multiply two  
// square matrices. 

// This function multiplies mat1[][] and  
// mat2[][], and stores the result in res[][] 
function multiply(&$mat1, &$mat2, &$res) 
{ 
    $N = 4; 
    for ($i = 0; $i < $N; $i++) 
    { 
        for ($j = 0; $j < $N; $j++) 
        { 
            $res[$i][$j] = 0; 
            for ($k = 0; $k < $N; $k++) 
                $res[$i][$j] += $mat1[$i][$k] *  
                                $mat2[$k][$j]; 
        } 
    } 
} 

// Driver Code 
$mat1 = array(array(1, 1, 1, 1), 
              array(2, 2, 2, 2), 
              array(3, 3, 3, 3), 
              array(4, 4, 4, 4)); 

$mat2 = array(array(1, 1, 1, 1), 
              array(2, 2, 2, 2), 
              array(3, 3, 3, 3), 
              array(4, 4, 4, 4)); 

multiply($mat1, $mat2, $res); 
$N = 4; 
echo ("Result matrix is \n"); 
for ($i = 0; $i < $N; $i++) 
{ 
    for ($j = 0; $j < $N; $j++) 
    { 
        echo ($res[$i][$j]); 
        echo(" "); 
    } 
    echo ("\n"); 
} 

// This code is contributed  
// by Shivi_Aggarwal  
?> 

```

**输出**：

```
Result matrix is
10 10 10 10
20 20 20 20
30 30 30 30
40 40 40 40 
```

**矩形矩阵的乘法**：

我们在 C 中使用指针来乘法到矩阵。 请参考以下帖子作为代码的前提条件。

[如何在 C 中将 2D 数组作为参数传递？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)

## C++

```cpp

// C++ program to multiply two 
// rectangular matrices 
#include<bits/stdc++.h> 
using namespace std; 

// Multiplies two matrices mat1[][]  
// and mat2[][] and prints result. 
// (m1) x (m2) and (n1) x (n2) are  
// dimensions of given matrices. 
void multiply(int m1, int m2, int mat1[][2],  
              int n1, int n2, int mat2[][2]) 
{ 
    int x, i, j; 
    int res[m1][n2]; 
    for (i = 0; i < m1; i++)  
    { 
        for (j = 0; j < n2; j++)  
        { 
            res[i][j] = 0; 
            for (x = 0; x < m2; x++)  
            { 
                *(*(res + i) + j) += *(*(mat1 + i) + x) * 
                                     *(*(mat2 + x) + j); 
            } 
        } 
    } 
    for (i = 0; i < m1; i++)  
    { 
        for (j = 0; j < n2; j++)  
        { 
            cout << *(*(res + i) + j) << " "; 
        } 
        cout << "\n"; 
    } 
} 

// Driver code 
int main() 
{ 
    int mat1[][2] = { { 2, 4 }, { 3, 4 } }; 
    int mat2[][2] = { { 1, 2 }, { 1, 3 } }; 
    int m1 = 2, m2 = 2, n1 = 2, n2 = 2; 
    multiply(m1, m2, mat1, n1, n2, mat2); 
    return 0; 
} 

// This code is contributed  
// by Akanksha Rai(Abby_akku) 

```

## C

```c
// C program to multiply two square matrices.
#include <stdio.h>
#define N 4
 
// This function multiplies mat1[][] and mat2[][],
// and stores the result in res[][]
void multiply(int mat1[][N], int mat2[][N], int res[][N])
{
    int i, j, k;
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++) {
            res[i][j] = 0;
            for (k = 0; k < N; k++)
                res[i][j] += mat1[i][k] * mat2[k][j];
        }
    }
}
 
int main()
{
    int mat1[N][N] = { { 1, 1, 1, 1 },
                       { 2, 2, 2, 2 },
                       { 3, 3, 3, 3 },
                       { 4, 4, 4, 4 } };
 
    int mat2[N][N] = { { 1, 1, 1, 1 },
                       { 2, 2, 2, 2 },
                       { 3, 3, 3, 3 },
                       { 4, 4, 4, 4 } };
 
    int res[N][N]; // To store result
    int i, j;
    multiply(mat1, mat2, res);
 
    printf("Result matrix is \n");
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++)
            printf("%d ", res[i][j]);
        printf("\n");
    }
 
    return 0;
}
```

## Java

```java
// Java program to multiply two square
// matrices.
import java.io.*;
 
class GFG {
 
    static int N = 4;
 
    // This function multiplies mat1[][]
    // and mat2[][], and stores the result
    // in res[][]
    static void multiply(int mat1[][],
                         int mat2[][], int res[][])
    {
        int i, j, k;
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++) {
                res[i][j] = 0;
                for (k = 0; k < N; k++)
                    res[i][j] += mat1[i][k]
                                 * mat2[k][j];
            }
        }
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int mat1[][] = { { 1, 1, 1, 1 },
                         { 2, 2, 2, 2 },
                         { 3, 3, 3, 3 },
                         { 4, 4, 4, 4 } };
 
        int mat2[][] = { { 1, 1, 1, 1 },
                         { 2, 2, 2, 2 },
                         { 3, 3, 3, 3 },
                         { 4, 4, 4, 4 } };
 
        // To store result
        int res[][] = new int[N][N];
        int i, j;
        multiply(mat1, mat2, res);
 
        System.out.println("Result matrix"
                           + " is ");
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++)
                System.out.print(res[i][j]
                                 + " ");
            System.out.println();
        }
    }
}
 
// This code is contributed by anuj_67.
```

## Python 3

```py
# 4x4 matrix multiplication using Python3
# Function definition
def matrix_multiplication(M, N):
    # List to store matrix multiplication result
    R = [[0, 0, 0, 0], 
        [0, 0, 0, 0], 
        [0, 0, 0, 0],
        [0, 0, 0, 0]] 
 
    for i in range(0, 4): 
        for j in range(0, 4):
            for k in range(0, 4): 
                R[i][j] += M[i][k] * N[k][j] 
 
    for i in range(0, 4): 
        for j in range(0, 4): 
            # if we use print(), by default cursor moves to next line each time, 
            # Now we can explicitly define ending character or sequence passing
            # second parameter as end ="<character or string>"
            # syntax: print(<variable or value to print>, end ="<ending with>")
            # Here space (" ") is used to print a gape after printing 
            # each element of R
            print(R[i][j], end =" ")
        print("\n", end ="")
 
# First matrix. M is a list
M = [[1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3],
    [4, 4, 4, 4]]
 
# Second matrix. N is a list
N = [[1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3],
    [4, 4, 4, 4]] 
     
# Call matrix_multiplication function
matrix_multiplication(M, N)
 
# This code is contributed by Santanu
```

## C#

```cs
// C# program to multiply two square
// matrices.
using System;
 
class GFG {
 
    static int N = 4;
 
    // This function multiplies mat1[][]
    // and mat2[][], and stores the result
    // in res[][]
    static void multiply(int[, ] mat1,
                         int[, ] mat2, int[, ] res)
    {
        int i, j, k;
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++) {
                res[i, j] = 0;
                for (k = 0; k < N; k++)
                    res[i, j] += mat1[i, k]
                                 * mat2[k, j];
            }
        }
    }
 
    // Driver code
    public static void Main()
    {
        int[, ] mat1 = { { 1, 1, 1, 1 },
                         { 2, 2, 2, 2 },
                         { 3, 3, 3, 3 },
                         { 4, 4, 4, 4 } };
 
        int[, ] mat2 = { { 1, 1, 1, 1 },
                         { 2, 2, 2, 2 },
                         { 3, 3, 3, 3 },
                         { 4, 4, 4, 4 } };
 
        // To store result
        int[, ] res = new int[N, N];
        int i, j;
        multiply(mat1, mat2, res);
 
        Console.WriteLine("Result matrix"
                          + " is ");
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++)
                Console.Write(res[i, j]
                              + " ");
            Console.WriteLine();
        }
    }
}
 
// This code is contributed by anuj_67.
```

## PHP

```php
<?php
// PHP program to multiply two 
// square matrices.
 
// This function multiplies mat1[][] and 
// mat2[][], and stores the result in res[][]
function multiply(&$mat1, &$mat2, &$res)
{
    $N = 4;
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {
            $res[$i][$j] = 0;
            for ($k = 0; $k < $N; $k++)
                $res[$i][$j] += $mat1[$i][$k] * 
                                $mat2[$k][$j];
        }
    }
}
 
// Driver Code
$mat1 = array(array(1, 1, 1, 1),
              array(2, 2, 2, 2),
              array(3, 3, 3, 3),
              array(4, 4, 4, 4));
 
$mat2 = array(array(1, 1, 1, 1),
              array(2, 2, 2, 2),
              array(3, 3, 3, 3),
              array(4, 4, 4, 4));
 
multiply($mat1, $mat2, $res);
$N = 4;
echo ("Result matrix is \n");
for ($i = 0; $i < $N; $i++)
{
    for ($j = 0; $j < $N; $j++)
    {
        echo ($res[$i][$j]);
        echo(" ");
    }
    echo ("\n");
}
 
// This code is contributed 
// by Shivi_Aggarwal 
?>
```

输出：

```
Result matrix is 
10 10 10 10 
20 20 20 20 
30 30 30 30 
40 40 40 40 
```

矩形矩阵的乘法：

我们在 C 中使用指针来乘以矩阵。 请参考以下帖子作为代码的前提条件。

[如何在 C 中将 2D 数组作为参数传递？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)

## C++

```cpp
// C++ program to multiply two
// rectangular matrices
#include <bits/stdc++.h>
using namespace std;
 
// Multiplies two matrices mat1[][]
// and mat2[][] and prints result.
// (m1) x (m2) and (n1) x (n2) are
// dimensions of given matrices.
void multiply(int m1, int m2, int mat1[][2], int n1, int n2,
              int mat2[][2])
{
    int x, i, j;
    int res[m1][n2];
    for (i = 0; i < m1; i++) 
    {
        for (j = 0; j < n2; j++) 
        {
            res[i][j] = 0;
            for (x = 0; x < m2; x++) 
            {
                *(*(res + i) + j) += *(*(mat1 + i) + x)
                                     * *(*(mat2 + x) + j);
            }
        }
    }
    for (i = 0; i < m1; i++) 
    {
        for (j = 0; j < n2; j++) 
        {
            cout << *(*(res + i) + j) << " ";
        }
        cout << "\n";
    }
}
 
// Driver code
int main()
{
    int mat1[][2] = { { 2, 4 }, { 3, 4 } };
    int mat2[][2] = { { 1, 2 }, { 1, 3 } };
    int m1 = 2, m2 = 2, n1 = 2, n2 = 2;
   
    // Function call
    multiply(m1, m2, mat1, n1, n2, mat2);
    return 0;
}
 
// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## C

```c
// C program to multiply two rectangular matrices
#include <stdio.h>
 
// Multiplies two matrices mat1[][] and mat2[][]
// and prints result.
// (m1) x (m2) and (n1) x (n2) are dimensions
// of given matrices.
void multiply(int m1, int m2, int mat1[][m2], int n1,
              int n2, int mat2[][n2])
{
    int x, i, j;
    int res[m1][n2];
    for (i = 0; i < m1; i++) 
    {
        for (j = 0; j < n2; j++) 
        {
            res[i][j] = 0;
            for (x = 0; x < m2; x++) 
            {
                *(*(res + i) + j) += *(*(mat1 + i) + x)
                                     * *(*(mat2 + x) + j);
            }
        }
    }
    for (i = 0; i < m1; i++) 
    {
        for (j = 0; j < n2; j++) 
        {
            printf("%d ", *(*(res + i) + j));
        }
        printf("\n");
    }
}
 
// Driver code
int main()
{
    int mat1[][2] = { { 2, 4 }, { 3, 4 } };
    int mat2[][2] = { { 1, 2 }, { 1, 3 } };
    int m1 = 2, m2 = 2, n1 = 2, n2 = 2;
   
    // Function call
    multiply(m1, m2, mat1, n1, n2, mat2);
    return 0;
}
```

## JAVA

```java
// Java program to multiply two matrices.
 
public class GFG 
{
 
    /**
     * to find out matrix multiplication
     *
     * @param matrix1 First matrix
     * @param rows1   Number of rows in matrix 1
     * @param cols1   Number of columns in matrix 1
     * @param matrix2 Second matrix
     * @param rows2   Number of rows in matrix 2
     * @param cols2   Number of columns in matrix 2
     * @return the result matrix (matrix 1 and matrix 2
     * multiplication)
     */
    public static int[][] matrixMultiplication(
        int[][] matrix1, int rows1, int cols1,
        int[][] matrix2, int rows2, int cols2)
        throws Exception
    {
 
        // Required condition for matrix multiplication
        if (cols1 != rows2) {
            throw new Exception("Invalid matrix given.");
        }
 
        // create a result matrix
        int resultMatrix[][] = new int[rows1][cols2];
 
        // Core logic for 2 matrices multiplication
        for (int i = 0; i < resultMatrix.length; i++) 
        {
            for (int j = 0; 
                 j < resultMatrix[i].length;
                 j++) 
            {
                for (int k = 0; k < cols1; k++) 
                {
                    resultMatrix[i][j]
                        += matrix1[i][k] * matrix2[k][j];
                }
            }
        }
        return resultMatrix;
    }
 
    // Driver code
    public static void main(String[] args) throws Exception
    {
 
        // Initial matrix 1 and matrix 2
        int matrix1[][] = { { 2, 4 }, { 3, 4 } };
        int matrix2[][] = { { 1, 2 }, { 1, 3 } };
 
        // Function call to get a matrix multiplication
        int resultMatrix[][] = matrixMultiplication(
            matrix1, 2, 2, matrix2, 2, 2);
 
        // Display result matrix
        System.out.println("Result Matrix is:");
        for (int i = 0; i < resultMatrix.length; i++) 
        {
            for (int j = 0; 
                 j < resultMatrix[i].length;
                 j++)
            {
                System.out.print(resultMatrix[i][j] + "\t");
            }
            System.out.println();
        }
    }
    // This code is contributed by darshatandel1998 (Darshan
    // Tandel)
}
```

## PHP

```php
<?php
// PHP program to multiply two 
// rectangular matrices 
 
// Multiplies two matrices mat1[][]  
// and mat2[][] and prints result. 
// (m1) x (m2) and (n1) x (n2) are 
// dimensions of given matrices. 
function multiply($m1, $m2, $mat1, 
                  $n1, $n2, $mat2) 
{ 
    for ($i = 0; $i < $m1; $i++) 
    { 
        for ($j = 0; $j < $n2; $j++) 
        { 
            $res[$i][$j] = 0; 
            for ($x = 0; $x < $m2; $x++) 
            { 
                $res[$i][$j] += $mat1[$i][$x] * 
                                $mat2[$x][$j]; 
            } 
        } 
    } 
    for ($i = 0; $i < $m1; $i++) 
    { 
        for ($j = 0; $j < $n2; $j++) 
        { 
            echo $res[$i][$j] . " "; 
        } 
        echo "\n"; 
    } 
} 
 
// Driver code 
$mat1 = array( array( 2, 4 ), array( 3, 4 )); 
$mat2 = array( array( 1, 2 ), array( 1, 3 )); 
$m1 = 2;
$m2 = 2;
$n1 = 2;
$n2 = 2; 
 
//Function call
multiply($m1, $m2, $mat1, $n1, $n2, $mat2); 
 
// This code is contributed by rathbhupendra
?>
```

输出：

```
6 16 
7 18 
```


时间复杂度：`O(n3)`。 可以使用 Strassen 的矩阵乘法对其进行优化。