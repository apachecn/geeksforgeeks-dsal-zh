# 旋转矩阵元素

> 原文： [https://www.geeksforgeeks.org/rotate-matrix-elements/](https://www.geeksforgeeks.org/rotate-matrix-elements/)

给定一个矩阵，顺时针旋转其中的元素。

**示例**：

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



想法是使用类似于[以螺旋形式打印矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)的程序的循环。 从最外层开始，一圈一圈地旋转所有元素环。 要旋转戒指，我们需要执行以下操作。

1.  移动第一行的元素。

2.  移动最后一列的元素。

3.  移动底部一行的元素。

4.  移动第一列的元素。

有内圈时，对内圈重复上述步骤。

以下是上述想法的实现。 感谢 Gaurav Ahirwar 提供以下解决方案的建议。

## C/C++

```
// C++ program to rotate a matrix 
  
#include <bits/stdc++.h> 
#define R 4 
#define C 4 
using namespace std; 
  
// A function to rotate a matrix mat[][] of size R x C. 
// Initially, m = R and n = C 
void rotatematrix(int m, int n, int mat[R][C]) 
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
  
        // Store the first element of next row, this 
        // element will replace first element of current 
        // row 
        prev = mat[row + 1][col]; 
  
         /* Move elements of first row from the remaining rows */
        for (int i = col; i < n; i++) 
        { 
            curr = mat[row][i]; 
            mat[row][i] = prev; 
            prev = curr; 
        } 
        row++; 
  
        /* Move elements of last column from the remaining columns */
        for (int i = row; i < m; i++) 
        { 
            curr = mat[i][n-1]; 
            mat[i][n-1] = prev; 
            prev = curr; 
        } 
        n--; 
  
         /* Move elements of last row from the remaining rows */
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
  
        /* Move elements of first column from the remaining rows */
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
    for (int i=0; i<R; i++) 
    { 
        for (int j=0; j<C; j++) 
          cout << mat[i][j] << " "; 
        cout << endl; 
    } 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    // Test Case 1 
    int a[R][C] = { {1,  2,  3,  4}, 
        {5,  6,  7,  8}, 
        {9,  10, 11, 12}, 
        {13, 14, 15, 16}  }; 
  
    // Tese Case 2 
    /* int a[R][C] = {{1, 2, 3}, 
                      {4, 5, 6}, 
                      {7, 8, 9} 
                     }; 
     */  rotatematrix(R, C, a); 
    return 0; 
}
```

## Java

```java
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
                System.out.print("\n"); 
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

## Python

```py
# Python program to rotate a matrix 
  
# Function to rotate a matrix 
def rotateMatrix(mat): 
  
    if not len(mat): 
        return
      
    """ 
        top : starting row index 
        bottom : ending row index 
        left : starting column index 
        right : ending column index 
    """
  
    top = 0
    bottom = len(mat)-1
  
    left = 0
    right = len(mat[0])-1
  
    while left < right and top < bottom: 
  
        # Store the first element of next row, 
        # this element will replace first element of 
        # current row 
        prev = mat[top+1][left] 
  
        # Move elements of top row one step right 
        for i in range(left, right+1): 
            curr = mat[top][i] 
            mat[top][i] = prev 
            prev = curr 
  
        top += 1
  
        # Move elements of rightmost column one step downwards 
        for i in range(top, bottom+1): 
            curr = mat[i][right] 
            mat[i][right] = prev 
            prev = curr 
  
        right -= 1
  
        # Move elements of bottom row one step left 
        for i in range(right, left-1, -1): 
            curr = mat[bottom][i] 
            mat[bottom][i] = prev 
            prev = curr 
  
        bottom -= 1
  
        # Move elements of leftmost column one step upwards 
        for i in range(bottom, top-1, -1): 
            curr = mat[i][left] 
            mat[i][left] = prev 
            prev = curr 
  
        left += 1
  
    return mat 
  
# Utility Function 
def printMatrix(mat): 
    for row in mat: 
        print row 
  
  
# Test case 1 
matrix =[  
            [1,  2,  3,  4 ], 
            [5,  6,  7,  8 ], 
            [9,  10, 11, 12 ], 
            [13, 14, 15, 16 ]   
        ] 
# Test case 2 
""" 
matrix =[ 
            [1, 2, 3], 
            [4, 5, 6], 
            [7, 8, 9] 
        ] 
"""
  
matrix = rotateMatrix(matrix) 
# Print modified matrix 
printMatrix(matrix)
```

## C#

```cs
// C# program to rotate a matrix 
using System; 
  
class GFG { 
      
    static int R = 4; 
    static int C = 4; 
  
    // A function to rotate a matrix  
    // mat[][] of size R x C. 
    // Initially, m = R and n = C 
    static void rotatematrix(int m, 
                        int n, int [,]mat) 
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
            prev = mat[row + 1, col]; 
      
            // Move elements of first row  
            // from the remaining rows  
            for (int i = col; i < n; i++) 
            { 
                curr = mat[row,i]; 
                mat[row, i] = prev; 
                prev = curr; 
            } 
            row++; 
      
            // Move elements of last column 
            // from the remaining columns  
            for (int i = row; i < m; i++) 
            { 
                curr = mat[i,n-1]; 
                mat[i, n-1] = prev; 
                prev = curr; 
            } 
            n--; 
      
            // Move elements of last row  
            // from the remaining rows  
            if (row < m) 
            { 
                for (int i = n-1; i >= col; i--) 
                { 
                    curr = mat[m-1,i]; 
                    mat[m-1,i] = prev; 
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
                    curr = mat[i,col]; 
                    mat[i,col] = prev; 
                    prev = curr; 
                } 
            } 
            col++; 
        } 
  
            // Print rotated matrix 
            for (int i = 0; i < R; i++) 
            { 
                for (int j = 0; j < C; j++) 
                Console.Write( mat[i,j] + " "); 
                Console.Write("\n"); 
            } 
    } 
  
    /* Driver program to test above functions */
    public static void Main()  
    { 
        // Test Case 1 
        int [,]a = { {1, 2, 3, 4}, 
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
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP program to rotate a matrix 
$R = 4; 
$C = 4; 
  
// A function to rotate a matrix  
// mat[][] of size R x C. Initially, 
// m = R and n = C 
function rotatematrix($m, $n, $mat) 
{ 
    global $R, $C; 
    $row = 0; 
    $col = 0; 
    $prev = 0; 
    $curr = 0; 
  
    /* 
    row - Staring row index 
    m - ending row index 
    col - starting column index 
    n - ending column index 
    i - iterator 
    */
    while ($row < $m && $col < $n) 
    { 
  
        if ($row + 1 == $m ||  
            $col + 1 == $n) 
            break; 
  
        // Store the first element  
        // of next row, this element  
        // will replace first element  
        // of current row 
        $prev = $mat[$row + 1][$col]; 
  
        /* Move elements of first row  
           from the remaining rows */
        for ($i = $col; $i < $n; $i++) 
        { 
            $curr = $mat[$row][$i]; 
            $mat[$row][$i] = $prev; 
            $prev = $curr; 
        } 
        $row++; 
  
        /* Move elements of last column 
           from the remaining columns */
        for ($i = $row; $i < $m; $i++) 
        { 
            $curr = $mat[$i][$n - 1]; 
            $mat[$i][$n - 1] = $prev; 
            $prev = $curr; 
        } 
        $n--; 
  
        /* Move elements of last row 
           from the remaining rows */
        if ($row < $m) 
        { 
            for ($i = $n - 1; 
                 $i >= $col; $i--) 
            { 
                $curr = $mat[$m - 1][$i]; 
                $mat[$m - 1][$i] = $prev; 
                $prev = $curr; 
            } 
        } 
        $m--; 
  
        /* Move elements of first column 
           from the remaining rows */
        if ($col < $n) 
        { 
            for ($i = $m - 1;  
                 $i >= $row; $i--) 
            { 
                $curr = $mat[$i][$col]; 
                $mat[$i][$col] = $prev; 
                $prev = $curr; 
            } 
        } 
        $col++; 
    } 
  
    // Print rotated matrix 
    for ($i = 0; $i < $R; $i++) 
    { 
        for ($j = 0; $j < $C; $j++) 
        echo $mat[$i][$j] . " "; 
        echo "\n"; 
    } 
} 
  
// Driver code 
  
// Test Case 1 
$a = array(array(1, 2, 3, 4), 
           array(5, 6, 7, 8), 
           array(9, 10, 11, 12), 
           array(13, 14, 15, 16)); 
  
// Tese Case 2 
/* int $a = array(array(1, 2, 3), 
                  array(4, 5, 6), 
                  array(7, 8, 9)); 
*/ rotatematrix($R, $C, $a); 
    return 0; 
      
// This code is contributed 
// by ChitraNayal 
?>
```

输出：

```
5 1 2 3
9 10 6 4
13 11 7 8
14 15 16 12
```
