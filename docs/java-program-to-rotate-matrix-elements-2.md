# 旋转矩阵元素的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序转矩阵-元素-2/](https://www.geeksforgeeks.org/java-program-to-rotate-matrix-elements-2/)

给定一个矩阵，顺时针旋转其中的元素。

**示例:**

```
Input
1    2    3
4    5    6
7    8    9

Output:
4    1    2
7    5    3
8    9    6

For 4*4 matrix
Input:
1    2    3    4    
5    6    7    8
9    10   11   12
13   14   15   16

Output:
5    1    2    3
9    10   6    4
13   11   7    8
14   15   16   12
```

这个想法是使用类似于[程序的循环来打印螺旋形式的矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)。一个接一个地旋转元素的所有环，从最外面开始。要旋转环，我们需要执行以下操作。
1)移动顶行的元素。
2)移动最后一列的元素。
3)移动最下面一行的元素。
4)移动第一列的元素。
有内圈时，对内圈重复上述步骤。

以下是上述想法的实现。感谢 Gaurav Ahirwar 提出以下解决方案。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rotate a matrix
import java.lang.*;
import java.util.*;

class GFG
{
    static int R = 4;
    static int C = 4;

    // A function to rotate a matrix 
    // mat[][] of size R x C.
    // Initially, m = R and n = C
    static void rotatematrix(int m,
                    int n, int mat[][])
    {
        int row = 0, col = 0;
        int prev, curr;

        /*
        row - Staring row index
        m - ending row index
        col - starting column index
        n - ending column index
        i - iterator
        */
        while (row < m && col < n)
        {

            if (row + 1 == m || col + 1 == n)
                break;

            // Store the first element of next
            // row, this element will replace 
            // first element of current row
            prev = mat[row + 1][col];

            // Move elements of first row 
            // from the remaining rows 
            for (int i = col; i < n; i++)
            {
                curr = mat[row][i];
                mat[row][i] = prev;
                prev = curr;
            }
            row++;

            // Move elements of last column
            // from the remaining columns 
            for (int i = row; i < m; i++)
            {
                curr = mat[i][n-1];
                mat[i][n-1] = prev;
                prev = curr;
            }
            n--;

            // Move elements of last row 
            // from the remaining rows 
            if (row < m)
            {
                for (int i = n-1; i >= col; i--)
                {
                    curr = mat[m-1][i];
                    mat[m-1][i] = prev;
                    prev = curr;
                }
            }
            m--;

            // Move elements of first column
            // from the remaining rows 
            if (col < n)
            {
                for (int i = m-1; i >= row; i--)
                {
                    curr = mat[i][col];
                    mat[i][col] = prev;
                    prev = curr;
                }
            }
            col++;
        }

            // Print rotated matrix
            for (int i = 0; i < R; i++)
            {
                for (int j = 0; j < C; j++)
                System.out.print( mat[i][j] + " ");
                System.out.print("
");
            }
    }

/* Driver program to test above functions */
    public static void main(String[] args) 
    {
    // Test Case 1
    int a[][] = { {1, 2, 3, 4},
                  {5, 6, 7, 8},
                {9, 10, 11, 12},
                {13, 14, 15, 16} };

    // Tese Case 2
    /* int a[][] = new int {{1, 2, 3},
                            {4, 5, 6},
                            {7, 8, 9}
                        };*/
    rotatematrix(R, C, a);

    }
}

// This code is contributed by Sahil_Bansall
```

**输出:**

```
5 1 2 3
9 10 6 4
13 11 7 8
14 15 16 12
```

更多详情请参考[旋转矩阵元素](https://www.geeksforgeeks.org/rotate-matrix-elements/)整篇文章！