# 打印矩阵元素的程序逐行跳过替代元素

> 原文:[https://www . geesforgeks . org/program-to-print-elements-of-a-matrix-row-wisp-skip-alternate-elements/](https://www.geeksforgeeks.org/program-to-print-elements-of-a-matrix-row-wise-skipping-alternate-elements/)

给定一个 N*N 大小的矩阵，其中 N 总是奇数，任务是逐行打印矩阵的元素，跳过交替元素。
**例** :

```
Input: mat[3][3] = 
{{1, 4, 3},
 {2, 5, 6},
 {7, 8, 9}}
Output: 1 3 5 7 9

Input: mat[5][5] = 
{{1, 2, 3, 4, 9},
 {5, 6, 7, 8, 44},
 {19, 10, 11, 12, 33},
 {13, 14, 15, 16, 55},
 {77, 88, 99, 111, 444}}
Output: 1 3 9 6 8 19 11 33 14 16 77 99 444 
```

**进场:**

1.  开始扫描矩阵。
2.  对于每一行，检查行号是偶数还是奇数。
    *   如果该行是偶数，则在该行的偶数索引处打印元素。
    *   如果该行是奇数，打印该行奇数索引处的元素。

以下是上述方法的实现:

## C++

```
// C++ program to print elements of a Matrix
// row-wise skipping alternate elements
#include <bits/stdc++.h>
using namespace std;
#define R 100
#define C 100

// Function to print the alternate
// elements of a matrix
void printElements(int mat[][C], int n)
{
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0)
            for (int j = 0; j < n; j += 2)
                cout << mat[i][j] << " ";
        else
            for (int j = 1; j < n; j += 2)
                cout << mat[i][j] << " ";
    }
}

// Driver code
int main()
{
    int n = 3;
    int mat[R][C] = { { 1, 5, 3 },
                      { 2, 4, 7 },
                      { 9, 8, 6 } };

    printElements(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print elements of a Matrix
// row-wise skipping alternate elements
import java.util.*;
import java.lang.*;

class GFG{
// Function to print the alternate
// elements of a matrix
static void printElements(int[][] mat, int n)
{
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
            for (int j = 0; j < n; j += 2)
                System.out.print(mat[i][j] + " ");
        else
            for (int j = 1; j < n; j += 2)
                System.out.print(mat[i][j] + " ");
    }
}

// Driver code
public static void main(String args[])
{
    int n = 3;
    int[][] mat = new int[][]{ { 1, 5, 3 },{ 2, 4, 7 },{ 9, 8, 6 } };

    printElements(mat, n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python 3 program to print elements of a Matrix
# row-wise skipping alternate elements 

# Function to print the alternate
# elements of a matrix
def printElements(mat, n) :

    for i in range(n) :
        if i % 2 == 0 :
            for j in range(0, n, 2) :
                print(mat[i][j],end = " ")
        else :
            for j in range(1, n, 2) :
                print(mat[i][j],end =" ")

# Driver Code
if __name__ == "__main__" :

    n = 3
    mat = [ [ 1, 5, 3],
            [ 2, 4, 7],
            [ 9, 8, 6] ]

    printElements(mat , n)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to print elements
// of a Matrix row-wise skipping
// alternate elements
using System;

class GFG
{
// Function to print the alternate
// elements of a matrix
static void printElements(int[,] mat,
                          int n)
{
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
            for (int j = 0; j < n; j += 2)
                Console.Write(mat[i, j] + " ");
        else
            for (int j = 1; j < n; j += 2)
                Console.Write(mat[i, j] + " ");
    }
}

// Driver code
public static void Main()
{
    int n = 3;
    int[,] mat = new int[,]{ { 1, 5, 3 },
                             { 2, 4, 7 },
                             { 9, 8, 6 }};

    printElements(mat, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print elements of a Matrix
// row-wise skipping alternate elements

// Function to print the alternate
// elements of a matrix
function printElements(&$mat, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        if ($i % 2 == 0)
            for ($j = 0; $j < $n; $j += 2)
            {
                echo $mat[$i][$j] ;
                echo " ";
            }
        else
            for ($j = 1; $j < $n; $j += 2)
            {
                echo $mat[$i][$j] ;
                echo " ";
            }
    }
}

// Driver code
$n = 3;
$arr = array(array(1, 2, 4),
             array(5, 6, 8));
$mat = array(array(1, 5, 3),
             array(2, 4, 7),
             array(9, 8, 6));

printElements($mat, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript Program to print elements of a Matrix
// row-wise skipping alternate elements

    // Function to print the alternate
    // elements of a matrix
    function printElements(mat , n) {
        for (i = 0; i < n; i++) {
            if (i % 2 == 0)
                for (j = 0; j < n; j += 2)
                    document.write(mat[i][j] + " ");
            else
                for (j = 1; j < n; j += 2)
                    document.write(mat[i][j] + " ");
        }
    }

    // Driver code

        var n = 3;
        var mat =[[ 1, 5, 3 ],
        [2, 4, 7 ], [
        9, 8, 6 ] ];

        printElements(mat, n);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
1 3 4 9 6
```