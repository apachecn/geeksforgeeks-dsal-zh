# 两个矩阵相乘的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-程序乘二矩阵/](https://www.geeksforgeeks.org/java-program-to-multiply-two-matrices/)

给定两个矩阵，将它们相乘的任务。矩阵可以是正方形或矩形。

**示例:**

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

**方阵乘法:**
下面的程序将两个大小为 4*4 的方阵相乘，我们可以针对不同的维度改变 N。

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

**Output**

```
Result matrix is 
10 10 10 10 
20 20 20 20 
30 30 30 30 
40 40 40 40
```

**时间复杂度:** O(n <sup>3</sup> )。它可以使用斯特拉森矩阵乘法进行优化

**辅助空间:** O(n <sup>2</sup> )

**矩形矩阵的乘法:**
我们使用 C 语言中的指针与矩阵相乘。请参考以下帖子作为代码的先决条件。
[如何在 C 中传递一个 2D 阵作为参数？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two matrices.

public class GFG 
{

    /**
     * to find out matrix multiplication
     *
     * @param matrix1 First matrix
     * @param rows1   Number of rows in matrix 1
     * @param cols1   Number of columns in matrix 1
     * @param matrix2 Second matrix
     * @param rows2   Number of rows in matrix 2
     * @param cols2   Number of columns in matrix 2
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
                System.out.print(resultMatrix[i][j] + "    ");
            }
            System.out.println();
        }
    }
    // This code is contributed by darshatandel1998 (Darshan
    // Tandel)
}
```

**Output**

```
6 16 
7 18
```

**时间复杂度:** O(n <sup>3</sup> )。可以使用[斯特拉森的矩阵乘法](https://www.geeksforgeeks.org/strassens-matrix-multiplication/)进行优化

**辅助空间:** O(m1 * n2)

更多详情请参考[两矩阵相乘程序](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)整篇文章！