# 打印矩阵与其镜像之和

> 原文:[https://www . geesforgeks . org/print-sum-matrix-and-it-mirror-image/](https://www.geeksforgeeks.org/print-sum-of-matrix-and-its-mirror-image/)

给你一个有序矩阵 **N*N** 。任务是通过将给定矩阵的镜像与矩阵本身相加来找到结果矩阵。
**示例** :

```
Input : mat[][] = {{1, 2, 3},
                              {4, 5, 6},
                              {7, 8, 9}}
Output : 4 4 4
               10 10 10
               16 16 16
Explanation:  
Resultant Matrix = {{1, 2, 3},      {{3, 2, 1}, 
                                 {4, 5, 6},   +   {6, 5, 4},
                                 {7, 8, 9}}       {9, 8, 7}}

Input : mat[][] = {{1, 2},
                               {3, 4}}
Output : 3 3
               7 7
```

当找到矩阵的镜像时，每个元素的行将保持不变，但其列的值将重新排列。对于任何元素 A <sub>ij</sub> ，其在镜像中的新位置将是 A <sub>i(n-j)</sub> 。获得矩阵的镜像后，将其添加到原始矩阵并打印结果。
**积分照顾:**

1.  矩阵的索引将从 0，0 开始，在 n-1，n-1 结束，因此任何元素 A <sub>ij</sub> 的位置将是 A <sub>i(n-1-j)。</sub>
2.  打印结果时，请注意正确的输出格式

以下是上述方法的实现:

## C++

```
// C++ program to find sum of matrix and
// its mirror image
#include <bits/stdc++.h>

#define N 4
using namespace std;

// Function to print the resultant matrix
void printSum(int mat[][N])
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << setw(3) << mat[i][N - 1 - j] + mat[i][j] << " ";
        }

        cout << "\n";
    }
}

// Driver Code
int main()
{
    int mat[N][N] = { { 2, 4, 6, 8 },
                      { 1, 3, 5, 7 },
                      { 8, 6, 4, 2 },
                      { 7, 5, 3, 1 } };

    printSum(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// matrix and its mirror image
import java.io.*;

class GFG
{
static int N = 4;

// Function to print the
// resultant matrix
static void printSum(int mat[][])
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            System.out.print((mat[i][N - 1 - j] +
                              mat[i][j]) + " ");
        }

        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    int mat[][] = { { 2, 4, 6, 8 },
                    { 1, 3, 5, 7 },
                    { 8, 6, 4, 2 },
                    { 7, 5, 3, 1 } };

    printSum(mat);
}
}

// This code is contributed by anuj_67
```

## 蟒蛇 3

```
# Python 3 program to find sum of matrix
# and its mirror image

N = 4

# Function to print the resultant matrix
def printSum(mat):
    for i in range(N):
        for j in range(N):
            print('{:>3}'.format(mat[i][N - 1 - j] +
                                 mat[i][j]), end =" ")

        print("\n", end = "")

# Driver Code
if __name__ == '__main__':
    mat = [[2, 4, 6, 8],
           [1, 3, 5, 7],
           [8, 6, 4, 2],
           [7, 5, 3, 1]]

    printSum(mat)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum of
// matrix and its mirror image
using System;

class GFG
{
static int N = 4;

// Function to print the
// resultant matrix
static void printSum(int [,]mat)
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            Console.Write((mat[i, N - 1 - j] +
                           mat[i, j]) + " ");
        }

        Console.WriteLine();
    }
}

// Driver Code
public static void Main ()
{
    int [,]mat = { { 2, 4, 6, 8 },
                   { 1, 3, 5, 7 },
                   { 8, 6, 4, 2 },
                   { 7, 5, 3, 1 } };

    printSum(mat);
}
}

// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// matrix and its mirror image

// Function to print the
// resultant matrix
function printSum($mat)
{
    for ($i = 0; $i < 4; $i++)
    {
        for ($j = 0; $j < 4; $j++)
        {
            echo ($mat[$i][4 - 1 - $j] +
                  $mat[$i][$j]) . " " ;
        }

        echo "\n";
    }
}

// Driver Code
$mat = array(array(2, 4, 6, 8 ),
             array(1, 3, 5, 7),
             array(8, 6, 4, 2),
             array(7, 5, 3, 1));

printSum($mat);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of matrix and
// its mirror image

var N = 4

// Function to print the resultant matrix
function printSum(mat)
{
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < N; j++) {
            document.write( (mat[i][N - 1 - j] + mat[i][j]) + " ");
        }

        document.write("<br>");
    }
}

// Driver Code
var mat = [ [ 2, 4, 6, 8 ],
                  [ 1, 3, 5, 7 ],
                  [ 8, 6, 4, 2 ],
                  [ 7, 5, 3, 1 ] ];
printSum(mat);

</script>
```

**Output:** 

```
10  10  10  10 
  8   8   8   8 
 10  10  10  10 
  8   8   8   8
```