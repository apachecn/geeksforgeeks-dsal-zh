# 从最后一列

开始，以蛇形图案打印矩阵

> 原文:[https://www . geeksforgeeks . org/print-matrix-in-snake-pattern-from-the-last-column/](https://www.geeksforgeeks.org/print-matrix-in-snake-pattern-from-the-last-column/)

给定一个由 n 行 n 列组成的二维矩阵。如下图所示，从第 n-1 列开始以蛇形方式打印该矩阵。

![matrix_traversal_snake](img/4697e0977dc6d41a71450970cab92265.png)

**示例:**

```
Input : mat[][] =  
1 2 3 
4 5 6
7 8 9
Output: 3 2 1 4 5 6 9 8 7

Input: mat[][] = 
1 2 3 4 
5 6 7 8 
9 10 11 12 
13 14 15 16
Output: 4 3 2 1 5 6 7 8 12 11 10 9 13 14 15 16

```

<font size="3">**算法:**</font>

1.  从属于第 0 行和第 n-1 列的右上角单元格开始遍历。
2.  第一次移动总是向**左(西)**方向水平移动。
3.  或者，在矩阵遍历期间进行水平和垂直移动。
4.  在一次水平移动中，我们遍历多个单元格，直到到达矩阵的任何一个壁。
5.  在水平移动中，如果行是奇数，我们向**右(东)**方向移动，否则我们向**左(西)**方向移动
6.  在单次垂直移动中，我们沿**向下**方向遍历单个单元格。

以下是上述算法的实现:

## C++

```
// C++ program for traversing a matrix from column n-1
#include <bits/stdc++.h>
using namespace std;

// Function used for traversing over the given matrix
void traverseMatrix(vector<vector<int> > mat, int n)
{

    for (int i = 0; i < n; i++) {
        if (i%2 == 1)
            for (int j = 0; j < n; j++)
                printf("%d ", mat[i][j]);

        else
            for (int j = n - 1; j >= 0; j--)
                printf("%d ", mat[i][j]);
    }
}

// Driver function
int main()
{

    // number of rows and columns
    int n = 5;

    // 5x5 matrix
    vector<vector<int> > mat{
        { 1, 2, 3, 4, 5 },
        { 6, 7, 8, 9, 10 },
        { 11, 12, 13, 14, 15 },
        { 16, 17, 18, 19, 20 },
        { 21, 22, 23, 24, 25 }
    };

    traverseMatrix(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for traversing a matrix from column n-1

class GFG {

    // Function used for traversing over the given matrix
    static void traverseMatrix(int[][] mat, int n)
    {

        for (int i = 0; i < n; i++) {
            if (i % 2 == 1) {
                for (int j = 0; j < n; j++) {
                    System.out.print(
                        Integer.toString(mat[i][j]) + " ");
                }
            }
            else {
                for (int j = n - 1; j >= 0; j--) {
                    System.out.print(
                        Integer.toString(mat[i][j]) + " ");
                }
            }
        }
    }

    // Driver function
    public static void main(String[] args)
    {

        // number of rows and columns
        int n = 5;

        // 5x5 matrix
        int[][] mat = {
            { 1, 2, 3, 4, 5 },
            { 6, 7, 8, 9, 10 },
            { 11, 12, 13, 14, 15 },
            { 16, 17, 18, 19, 20 },
            { 21, 22, 23, 24, 25 }
        };

        traverseMatrix(mat, n);

        System.exit(0);
    }
}
```

## 蟒蛇 3

```
# Python3 program for traversing a matrix from column n-1
import sys;

# Function used for traversing over the given matrix
def traverseMatrix(mat, n):

    for i in range(n): 
        if i & 1:
            for j in range(n):
                print(str(mat[i][j])+ "", end = " ")
        else:
            for j in range(n-1, -1, -1):
                print(str(mat[i][j])+ "", end = " ")

# Driver function
if __name__ == '__main__':

    # number of rows and columns
    n = 5

    # 5x5 matrix
    mat =[
         [1,  2,  3,  4,  5],
         [6,  7,  8,  9,  10],
         [11, 12, 13, 14, 15],
         [16, 17, 18, 19, 20],
         [21, 22, 23, 24, 25]
    ]

    traverseMatrix(mat, n)
```

## C#

```
// CSHARP program for traversing a matrix from column n-1

using System;
using System.Linq;

class GFG {

    // Function used for traversing over the given matrix
    static void traverseMatrix(int[, ] mat, int n)
    {

        for (int i = 0; i < n; i++) {
            if (i % 2 == 1) {
                for (int j = 0; j < n; j++) {
                    Console.Write(mat[i, j].ToString() + " ");
                }
            }
            else {
                for (int j = n - 1; j >= 0; j--) {
                    Console.Write(mat[i, j].ToString() + " ");
                }
            }
        }
    }

    // Driver function
    public static void Main()
    {

        // number of rows and columns
        int n = 5;

        // 5x5 matrix
        int[, ] mat = {
            { 1, 2, 3, 4, 5 },
            { 6, 7, 8, 9, 10 },
            { 11, 12, 13, 14, 15 },
            { 16, 17, 18, 19, 20 },
            { 21, 22, 23, 24, 25 }
        };

        traverseMatrix(mat, n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for traversing a matrix from column n-1

# Function used for traversing over the given matrix
function traverseMatrix($mat, $n){

    for($i = 0; $i < $n; $i++) {
        if($i & 1) {
            for($j = 0; $j < $n; $j++) {
                print($mat[$i][$j]." ");
            }
        }
        else {
            for($j = $n - 1; $j >= 0; $j--) {
                print($mat[$i][$j]." ");
            }    
        }
    }
} 

// Driver function

# number of rows and columns
$n = 5;

#  5x5 matrix
$mat = array(
     array(1,  2,  3,  4,  5),
     array(6,  7,  8,  9,  10),
     array(11, 12, 13, 14, 15),
     array(16, 17, 18, 19, 20),
     array(21, 22, 23, 24, 25)
);

traverseMatrix($mat, $n);

?>
```

**Output:**

```
5 4 3 2 1 6 7 8 9 10 15 14 13 12 11 16 17 18 19 20 25 24 23 22 21

```

**时间复杂度** : O(N^2)
**空间复杂度** : O(1)