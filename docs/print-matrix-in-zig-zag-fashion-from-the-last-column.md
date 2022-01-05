# 从最后一列开始以之字形打印矩阵

> 原文:[https://www . geesforgeks . org/print-matrix-in-zig-zag-fashion-from-the-last-column/](https://www.geeksforgeeks.org/print-matrix-in-zig-zag-fashion-from-the-last-column/)

给定一个由 n 行 n 列组成的二维矩阵。如下图所示，从第 n-1 列开始以 ZIG-ZIG 方式打印该矩阵。

![Zigzag matrix traversal](img/724d2ec764f4c24c49d411b5509a6752.png)

**示例:**

```
Input: mat[][] = 
1 2 3 
4 5 6
7 8 9
Output: 3 2 6 9 5 1 4 8 7

Input: mat[][] = 
1 2 3 4 
5 6 7 8 
9 10 11 12 
13 14 15 16
Output: 4 3 8 12 7 2 1 6 11 16 15 10 5 9 14 13

```

<font size="3">**算法:**</font>

1.  从属于第 0 行和第 n-1 列的右上角单元格开始遍历。
2.  第一次移动总是朝着**左(西)**方向。
3.  我们做一个水平/垂直移动，以防移动是奇数。
4.  如果最后一次移动是在**西北**方向，则向左移动**如果没有墙，则向左移动**，如果**左侧**有墙，则向下移动**。******
5.  ******如果最后一次移动是在**东南**方向，移动**向下**如果没有墙**向下**，移动**向左**如果有墙**向下**。******
6.  ****我们做一个对角移动，以防移动是偶数。****
7.  ****我们选择向**东南**和**西北**方向交替移动，从**东南**开始移动。****
8.  ****在**单对角移动**中，我们保持沿同一方向穿过多个细胞，直到到达矩阵的任何一个壁。伪代码:

    ```
    if ((move_cnt >> 1) & 1) {
         // move south east
    }
    else {
         // move north west
    }

    ```**** 

> ******使用的变量******
> 
> *   ******mat** :给定 NxN 矩阵****
> *   ******cur_x** :当前行号****
> *   ******cur_y** :当前列号****
> *   ******前一步**:用于跟踪前一步****
> *   ******移动 _ 计数**:用于记录移动的次数****
> *   ******cell_cnt** :用于记录遍历的单元格数量****

****下面的代码是上述算法的实现。**** 

## ****C++****

```
**// C++ program for traversing a matrix from column n-1
#include <bits/stdc++.h>
using namespace std;

// Function used for traversing over the given matrix
void traverseMatrix(vector<vector<int> > mat, int n)
{

    // Initial cell coordinates
    int cur_x = 0, cur_y = n - 1;

    // Variable used for keeping track of last move
    string prev_move = "";

    // Variable used for keeping count
    // of cells traversed till next move
    int move_cnt = 1;
    int cell_cnt = 1;
    printf("%d ", mat[cur_x][cur_y]);

    while (cell_cnt < n * n) {

        // odd numbered move [SINGLE VERTICAL/HORIZONTAL]
        if (move_cnt & 1) {

            // last move was made in north east direction
            if (prev_move == "NORTH_WEST" or prev_move == "") {
                // move left
                if (cur_y != 0) {
                    --cur_y;
                    prev_move = "LEFT";
                }
                // move down
                else {
                    ++cur_x;
                    prev_move = "DOWN";
                }
            }

            // last move was made in south east direction
            else {
                // move down
                if (cur_x != n - 1) {
                    ++cur_x;
                    prev_move = "DOWN";
                }
                // move left
                else {
                    --cur_y;
                    prev_move = "LEFT";
                }
            }
            printf("%d ", mat[cur_x][cur_y]);
            ++cell_cnt;
        }

        // even numbered move/s [DIAGONAL/S]
        else {
            if ((move_cnt >> 1) & 1) {

                // move south east
                while (cur_x < n - 1 and cur_y < n - 1) {
                    ++cur_x;
                    ++cur_y;
                    prev_move = "SOUTH_EAST";
                    printf("%d ", mat[cur_x][cur_y]);
                    ++cell_cnt;
                }
            }
            else {
                // move north west
                while (cur_x > 0 and cur_y > 0) {
                    --cur_x;
                    --cur_y;
                    prev_move = "NORTH_WEST";
                    printf("%d ", mat[cur_x][cur_y]);
                    ++cell_cnt;
                }
            }
        }
        ++move_cnt;
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
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for traversing a matrix from column n-1

class GFG {

    // Function used for traversing over the given matrix
    static void traverseMatrix(int[][] mat, int n)
    {

        // Initial cell coordinates
        int cur_x = 0, cur_y = n - 1;

        // Variable used for keeping track of last move
        String prev_move = "";

        // Variable used for keeping count
        // of cells traversed till next move
        int move_cnt = 1;
        int cell_cnt = 1;
        System.out.print(Integer.toString(
                             mat[cur_x][cur_y])
                         + " ");

        while (cell_cnt < n * n) {

            // odd numbered move
            // [SINGLE VERTICAL/HORIZONTAL]
            if (move_cnt % 2 == 1) {
                // last move was made in north east direction
                if (prev_move == "NORTH_WEST" || prev_move == "") {
                    // move left
                    if (cur_y != 0) {
                        --cur_y;
                        prev_move = "LEFT";
                    }
                    // move down
                    else {
                        ++cur_x;
                        prev_move = "DOWN";
                    }
                }

                // last move was made in south east direction
                else {

                    // move down
                    if (cur_x != n - 1) {
                        ++cur_x;
                        prev_move = "DOWN";
                    }

                    // move left
                    else {
                        --cur_y;
                        prev_move = "LEFT";
                    }
                }
                System.out.print(Integer.toString(
                                     mat[cur_x][cur_y])
                                 + " ");
                ++cell_cnt;
            }

            // even numbered move/s [DIAGONAL/S]
            else {
                if ((move_cnt >> 1) % 2 == 1) {

                    // move south east
                    while (cur_x < n - 1 && cur_y < n - 1) {
                        ++cur_x;
                        ++cur_y;
                        prev_move = "SOUTH_EAST";
                        System.out.print(
                            Integer.toString(
                                mat[cur_x][cur_y])
                            + " ");
                        ++cell_cnt;
                    }
                }
                else {

                    // move north west
                    while (cur_x > 0 && cur_y > 0) {
                        --cur_x;
                        --cur_y;
                        prev_move = "NORTH_WEST";
                        System.out.print(
                            Integer.toString(
                                mat[cur_x][cur_y])
                            + " ");
                        ++cell_cnt;
                    }
                }
            }
            ++move_cnt;
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
}**
```

## ****计算机编程语言****

```
**# Python program for traversing a matrix from column n-1
import sys;

# Function used for traversing over the given matrix
def traverseMatrix(mat, n):

    # Initial cell coordinates
    cur_x = 0; cur_y = n - 1

    # Variable used for keeping track of last move
    prev_move = ""

    # Variable used for keeping count 
    # of cells traversed till next move
    move_cnt = 1
    cell_cnt = 1
    print(mat[cur_x][cur_y], end = ' ')

    while cell_cnt < n * n:

        # odd numbered move [SINGLE VERTICAL / HORIZONTAL]
        if move_cnt & 1: 

            # last move was made in north east direction
            if prev_move == "NORTH_WEST" or prev_move == "" :

                # move left
                if cur_y != 0:
                    cur_y -= 1 
                    prev_move = "LEFT"

                # move down
                else :
                    cur_x += 1
                    prev_move = "DOWN"

            # last move was made in south east direction
            else :

                # move down
                if(cur_x != n-1):
                    cur_x += 1
                    prev_move = "DOWN"

                # move left
                else :
                    cur_y -= 1
                    prev_move = "LEFT"

            print(mat[cur_x][cur_y], end = ' ')
            cell_cnt += 1

        # even numbered move / s [DIAGONAL / S]
        else :
            if (move_cnt >> 1) & 1:

                # move south east
                while cur_x < n - 1 and cur_y < n - 1:
                    cur_x += 1; cur_y += 1 
                    prev_move = "SOUTH_EAST"
                    print(mat[cur_x][cur_y], end = ' ')
                    cell_cnt += 1

            else :

                # move north west
                while cur_x > 0 and cur_y > 0:
                    cur_x -= 1 ; cur_y -= 1
                    prev_move = "NORTH_WEST";
                    print(mat[cur_x][cur_y], end = ' ')
                    cell_cnt += 1

        move_cnt += 1 

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

    traverseMatrix(mat, n)**
```

## ****C#****

```
**// CSHARP program for traversing a matrix from column n-1

using System;
using System.Linq;

class GFG {

    // Function used for traversing over the given matrix
    static void traverseMatrix(int[, ] mat, int n)
    {

        // Initial cell coordinates
        int cur_x = 0, cur_y = n - 1;

        // Variable used for keeping track of last move
        string prev_move = "";

        // Variable used for keeping count
        // of cells traversed till next move
        int move_cnt = 1;
        int cell_cnt = 1;
        Console.Write(mat[cur_x, cur_y].ToString() + " ");

        while (cell_cnt < n * n) {

            // odd numbered move [SINGLE VERTICAL/HORIZONTAL]
            if (move_cnt % 2 == 1) {

                // last move was made in north east direction
                if (prev_move == "NORTH_WEST" || prev_move == "") {

                    // move left
                    if (cur_y != 0) {
                        --cur_y;
                        prev_move = "LEFT";
                    }

                    // move down
                    else {
                        ++cur_x;
                        prev_move = "DOWN";
                    }
                }

                // last move was made in south east direction
                else {
                    // move down
                    if (cur_x != n - 1) {
                        ++cur_x;
                        prev_move = "DOWN";
                    }
                    // move left
                    else {
                        --cur_y;
                        prev_move = "LEFT";
                    }
                }
                Console.Write(
                    mat[cur_x, cur_y].ToString() + " ");
                ++cell_cnt;
            }

            // even numbered move/s [DIAGONAL/S]
            else {
                if ((move_cnt >> 1) % 2 == 1) {

                    // Console.WriteLine("[...]");
                    // move south east
                    while (cur_x < n - 1 && cur_y < n - 1) {
                        ++cur_x;
                        ++cur_y;
                        prev_move = "SOUTH_EAST";
                        Console.Write(
                            mat[cur_x, cur_y].ToString()
                            + " ");
                        ++cell_cnt;
                    }
                }
                else {

                    // move north west
                    while (cur_x > 0 && cur_y > 0) {
                        --cur_x;
                        --cur_y;
                        prev_move = "NORTH_WEST";
                        Console.Write(
                            mat[cur_x, cur_y].ToString()
                            + " ");
                        ++cell_cnt;
                    }
                }
            }
            ++move_cnt;
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
}**
```

## ****服务器端编程语言（Professional Hypertext Preprocessor 的缩写）****

```
**<?php
// PHP program for traversing a matrix from column n-1

// Function used for traversing over the given matrix
function traverseMatrix($mat, $n){

    # Initial cell coordinates
    $cur_x = 0; $cur_y = $n - 1;

    # Variable used for keeping track of last move
    $prev_move = "";

    # Variable used for keeping count 
    # of cells traversed till next move
    $move_cnt = 1;
    $cell_cnt = 1;
    print($mat[$cur_x][$cur_y]." ");

    while ($cell_cnt < $n * $n) {

        # odd numbered move [SINGLE VERTICAL/HORIZONTAL]
        if ($move_cnt & 1) {

            # last move was made in north east direction
            if ($prev_move == "NORTH_WEST" or 
                                        $prev_move == "") {
                # move left
                if ($cur_y != 0){
                    $cur_y -= 1;
                    $prev_move = "LEFT";
                }

                # move down
                else {
                    $cur_x += 1;
                    $prev_move = "DOWN";
                }
            }

            # last move was made in south east direction
            else {

                # move down
                if($cur_x != $n - 1){
                    $cur_x += 1;
                    $prev_move = "DOWN";
                }

                # move left
                else {
                    $cur_y -= 1;
                    $prev_move = "LEFT";
                }
            }

            print($mat[$cur_x][$cur_y]." ");
            $cell_cnt += 1;
        }

        # even numbered move/s [DIAGONAL/S]
        else {
            if (($move_cnt >> 1) & 1) {

                # move south east
                while ($cur_x < $n - 1 and $cur_y < $n - 1) {
                    $cur_x += 1; $cur_y += 1;
                    $prev_move = "SOUTH_EAST";
                    print($mat[$cur_x][$cur_y]." ");
                    $cell_cnt += 1;
                }
            }

            else {

                # move north west
                while($cur_x > 0 and $cur_y > 0) {
                    $cur_x -=1 ; $cur_y -= 1;
                    $prev_move = "NORTH_WEST";
                    print($mat[$cur_x][$cur_y]." ");
                    $cell_cnt += 1;
                }
            }
        }

        $move_cnt += 1;
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
?>**
```

******Output:**

```
5 4 10 15 9 3 2 8 14 20 25 19 13 7 1 6 12 18 24 23 17 11 16 22 21

```**** 

******时间复杂度** : O(N^2)
**空间复杂度** : O(1)****