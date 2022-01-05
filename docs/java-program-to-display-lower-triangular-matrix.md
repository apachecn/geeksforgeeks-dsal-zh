# 显示下三角矩阵的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序到显示-下三角矩阵/](https://www.geeksforgeeks.org/java-program-to-display-lower-triangular-matrix/)

下三角矩阵是一个正方形矩阵，其中主对角线以上的所有元素都是 0。如果矩阵不是正方形矩阵，就永远不能称为下三角矩阵。

**示例**

```
Input 1: mat[][] = { {2, 1, 4},
                     {1, 2, 3},  
                     {3, 6, 2}}

Output :  mat[][]= {{2, 0, 0},
                    {1, 2, 0},  
                    {3, 6, 2}}

Explaination :    All the element below the principal diagonal needs to be 0.

Input 2 : mat[][]=    {{4, 6},
                         {2, 8}}

Output :   mat[][]=     {{4, 0},
                         {2, 8}}

Input 3 :  mat[][] = { {2, 1, 4, 6},
                       {1, 2, 3, 7},  
                       {3, 6, 2, 8} }  

Output :   Matrix should be a Square Matrix
```

**进场:**

*   如果矩阵有相等的行和列，继续程序，否则退出程序。
*   对整个矩阵进行循环，对于列数大于行号的行，**使该位置的元素等于 0。**

以下是上述方法的**实现方式**:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for displaying lower triangular matrix
import java.io.*;

class GFG {
    static void lowerTriangularMatrix(int matrix[][])
    {
        int row = matrix.length;
        int col = matrix[0].length;

        // if number of rows and columns are not equal,
        // then return back
        if (row != col) {
            System.out.println(
                "Matrix should be a Square Matrix");
            return;
        }
        else {
            // looping over the whole matrix
            for (int i = 0; i < row; i++) {
                for (int j = 0; j < col; j++) {

                    // for the rows,whose column number is
                    // greater then row number,mark the
                    // element as 0
                    if (i < j) {
                        matrix[i][j] = 0;
                    }
                }
            }

            System.out.println(
                "Lower Triangular Matrix is given by :-");
            // printing the lower triangular matrix
            for (int i = 0; i < row; i++) {
                for (int j = 0; j < col; j++) {
                    System.out.print(matrix[i][j] + " ");
                }
                System.out.println();
            }
        }
    }
    public static void main(String[] args)
    {
        // driver code
        int mat[][]
            = { { 2, 1, 4 }, { 1, 2, 3 }, { 3, 6, 2 } };
        // calling the function
        lowerTriangularMatrix(mat);
    }
}
```

**输出:**

```
Lower Triangular Matrix is given by :-
2 0 0 
1 2 0 
3 6 2 
```

*   **空间复杂度:**矩阵可原地更改**。即不需要额外的矩阵空间。0(N^2)**
*   ****时间复杂度:** 0(N^2)**