# Java 程序添加两个矩阵

> 原文:[https://www . geesforgeks . org/Java-程序加二矩阵/](https://www.geeksforgeeks.org/java-program-to-add-two-matrices/)

给定两个相同大小的矩阵 **A** 和 **B** ，在 Java 中添加它们的任务。
**例:**

```
Input: A[][] = {{1, 2}, 
                {3, 4}}
       B[][] = {{1, 1}, 
                {1, 1}}
Output: {{2, 3}, 
         {4, 5}}

Input: A[][] = {{2, 4}, 
                {3, 4}}
       B[][] = {{1, 2}, 
                {1, 3}}       
Output: {{3, 6}, 
         {4, 7}}
```

**进场:**

*   取要相加的两个矩阵
*   创建一个新矩阵来存储两个矩阵的和
*   遍历这两个矩阵的每个元素，然后将它们相加。将此总和存储在新矩阵中相应的索引处。
*   打印最终的新矩阵

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for addition of two matrices

import java.io.*;

class GFG {

    // Function to print Matrix
    static void printMatrix(int M[][],
                            int rowSize,
                            int colSize)
    {
        for (int i = 0; i < rowSize; i++) {
            for (int j = 0; j < colSize; j++)
                System.out.print(M[i][j] + " ");

            System.out.println();
        }
    }

    // Function to add the two matrices
    // and store in matrix C
    static int[][] add(int A[][], int B[][],
                       int size)
    {
        int i, j;
        int C[][] = new int[size][size];

        for (i = 0; i < size; i++)
            for (j = 0; j < size; j++)
                C[i][j] = A[i][j] + B[i][j];

        return C;
    }

    // Driver code
    public static void main(String[] args)
    {
        int size = 4;

        int A[][] = { { 1, 1, 1, 1 },
                      { 2, 2, 2, 2 },
                      { 3, 3, 3, 3 },
                      { 4, 4, 4, 4 } };
        // Print the matrices A
        System.out.println("\nMatrix A:");
        printMatrix(A, size, size);

        int B[][] = { { 1, 1, 1, 1 },
                      { 2, 2, 2, 2 },
                      { 3, 3, 3, 3 },
                      { 4, 4, 4, 4 } };
        // Print the matrices B
        System.out.println("\nMatrix B:");
        printMatrix(B, size, size);

        // Add the two matrices
        int C[][] = add(A, B, size);

        // Print the result
        System.out.println("\nResultant Matrix:");
        printMatrix(C, size, size);
    }
}
```

**Output:** 

```
Matrix A:
1 1 1 1 
2 2 2 2 
3 3 3 3 
4 4 4 4 

Matrix B:
1 1 1 1 
2 2 2 2 
3 3 3 3 
4 4 4 4 

Resultant Matrix:
2 2 2 2 
4 4 4 4 
6 6 6 6 
8 8 8 8
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为矩阵的行号或列号*

***辅助空间:** O(N <sup>2</sup> )*