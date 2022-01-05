# 相邻元素网格中的最小乘积

> 原文:[https://www . geeksforgeeks . org/相邻元素网格中的最小产品数/](https://www.geeksforgeeks.org/minimum-product-in-a-grid-of-adjacent-elements/)

给定一个 N×M 网格。任务是找出矩阵中相同方向(上、下、左、右或对角)的四个相邻数的最小乘积。

**示例:**

```
Input : mat[][] = {1, 2, 3, 4,
                   5, 6, 7, 8,
                   9, 10, 11, 12}  
Output : 700 
2*5*7*10 gives output as 700 which is the smallest 
product possible 

Input :{7, 6, 7, 9
        1, 2, 3, 4
        1, 2, 3, 6,
        5, 6, 7, 1}   
Output: 36   
```

**方法:**除了第一行、最后一行、第一列和最后一列之外，在矩阵中遍历。计算四个相邻数字的乘积，分别是***mat【I-1】【j】、mat【I+1】【j】、mat【I】【j+1】和 mat【I】【j-1】*****。**在每次计算中，如果这样形成的乘积小于先前找到的最小值，则用计算的乘积替换最小变量。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum product
// of adjacent elements
#include <bits/stdc++.h>
using namespace std;
const int N = 3;
const int M = 4;

// Function to return the minimum
// product of adjacent elements
int minimumProduct(int mat[N][M])
{

    // initial minimum
    int minimum = INT_MAX;

    // Traverse in the matrix
    // except the first, last row
    // first and last column
    for (int i = 1; i < N - 1; i++) {
        for (int j = 1; j < M - 1; j++) {
            // product the adjacent elements
            int p = mat[i - 1][j] * mat[i + 1][j]
                    * mat[i][j + 1] * mat[i][j - 1];

            // if the product is less than
            // the previously computed minimum
            if (p < minimum)
                minimum = p;
        }
    }

    return minimum;
}

// Driver Code
int main()
{
    int mat[][4] = { { 1, 2, 3, 4 },
                     { 4, 5, 6, 7 },
                     { 7, 8, 9, 12 } };

    cout << minimumProduct(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the minimum product
// of adjacent elements
import java.io.*;

class GFG
{
static int N = 3;
static int M = 4;

// Function to return the
// minimum product of
// adjacent elements
static int minimumProduct(int mat[][])
{

    // initial minimum
    int minimum = Integer.MAX_VALUE;

    // Traverse in the matrix
    // except the first, last row
    // first and last column
    for (int i = 1; i < N - 1; i++)
    {
        for (int j = 1; j < M - 1; j++)
        {
            // product the
            // adjacent elements
            int p = mat[i - 1][j] *
                    mat[i + 1][j] *
                    mat[i][j + 1] *
                    mat[i][j - 1];

            // if the product is less
            // than the previously
            // computed minimum
            if (p < minimum)
                minimum = p;
        }
    }

    return minimum;
}

// Driver Code
public static void main (String[] args)
{
    int mat[][] = {{1, 2, 3, 4},
                   {4, 5, 6, 7},
                   {7, 8, 9, 12}};

    System.out.println(minimumProduct(mat));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find the minimum
# product of adjacent elements
import sys

N = 3
M = 4

# Function to return the minimum
# product of adjacent elements
def minimumProduct(mat):

    # initial minimum
    minimum = sys.maxsize

    # Traverse in the matrix except
    # the first, last row first
    # and last column
    for i in range(1, N - 1, 1):
        for j in range(1, M - 1, 1):

            # product the adjacent elements
            p = (mat[i - 1][j] * mat[i + 1][j] *
                 mat[i][j + 1] * mat[i][j - 1])

            # if the product is less than
            # the previously computed minimum
            if (p < minimum):
                minimum = p

    return minimum

# Driver Code
if __name__ == '__main__':
    mat = [[1, 2, 3, 4],   
           [4, 5, 6, 7],
           [7, 8, 9, 12]]

    print(minimumProduct(mat))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find
// the minimum product
// of adjacent elements
using System;

class GFG
{
static int N = 3;
static int M = 4;

// Function to return the
// minimum product of
// adjacent elements
static int minimumProduct(int [,]mat)
{

    // initial minimum
    int minimum = int.MaxValue;

    // Traverse in the matrix
    // except the first, last row
    // first and last column
    for (int i = 1;
             i < N - 1; i++)
    {
        for (int j = 1;
                 j < M - 1; j++)
        {
            // product the
            // adjacent elements
            int p = mat[i - 1, j] *
                    mat[i + 1, j] *
                    mat[i, j + 1] *
                    mat[i, j - 1];

            // if the product is less
            // than the previously
            // computed minimum
            if (p < minimum)
                minimum = p;
        }
    }

    return minimum;
}

// Driver Code
public static void Main ()
{
    int [,]mat = {{1, 2, 3, 4},
                  {4, 5, 6, 7},
                  {7, 8, 9, 12}};

    Console.WriteLine(minimumProduct(mat));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// product of adjacent elements
$N = 3;
$M = 4;

// Function to return the minimum
// product of adjacent elements
function minimumProduct($mat)
{
    global $N;
    global $M;

    // initial minimum
    $minimum = PHP_INT_MAX;

    // Traverse in the matrix
    // except the first, last row
    // first and last column
    for ($i = 1; $i < $N - 1; $i++)
    {
        for ($j = 1; $j < $M - 1; $j++)
        {
            // product the adjacent elements
            $p = $mat[$i - 1][$j] * $mat[$i + 1][$j] *
                 $mat[$i][$j + 1] * $mat[$i][$j - 1];

            // if the product is less than the
            // previously computed minimum
            if ($p < $minimum)
                $minimum = $p;
        }
    }

    return $minimum;
}

// Driver Code
$mat = array(array(1, 2, 3, 4),
             array(4, 5, 6, 7),
             array(7, 8, 9, 12));

echo minimumProduct($mat);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>
    // Javascript program to find
    // the minimum product
    // of adjacent elements

    let N = 3;
    let M = 4;

    // Function to return the
    // minimum product of
    // adjacent elements
    function minimumProduct(mat)
    {

        // initial minimum
        let minimum = Number.MAX_VALUE;

        // Traverse in the matrix
        // except the first, last row
        // first and last column
        for (let i = 1; i < N - 1; i++)
        {
            for (let j = 1; j < M - 1; j++)
            {
                // product the
                // adjacent elements
                let p = mat[i - 1][j] *
                        mat[i + 1][j] *
                        mat[i][j + 1] *
                        mat[i][j - 1];

                // if the product is less
                // than the previously
                // computed minimum
                if (p < minimum)
                    minimum = p;
            }
        }

        return minimum;
    }

    let mat = [[1, 2, 3, 4],
               [4, 5, 6, 7],
               [7, 8, 9, 12]];

    document.write(minimumProduct(mat));

</script>
```

**Output:** 

```
384
```

**时间复杂度:** O(N*M)