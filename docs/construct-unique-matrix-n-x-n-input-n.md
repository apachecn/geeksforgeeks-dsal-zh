# 为输入 n 构建唯一矩阵 n×n

> 原文:[https://www . geesforgeks . org/construct-unique-matrix-n-x-n-input-n/](https://www.geeksforgeeks.org/construct-unique-matrix-n-x-n-input-n/)

给定一个奇数 n，求一个大小为 n×n 的矩阵，条件如下:

1.  每个单元格包含一个从 1 到 n(包括 1 和 n)的整数。
2.  任何整数都不会在同一行或同一列中出现两次。
3.  所有的 1 必须尽可能远离矩阵的中心。n×n 正方形的中心是奇数 n 的格((n-1)/2，(n-1)/2)。

**例:**

```
Input  : n = 1
Output : 1

Input : n = 3
Output: 3 2 1
        1 3 2
        2 1 3

Input : n = 5
Output : 5 3 2 4 1 
         1 4 3 5 2 
         2 5 4 1 3 
         3 1 5 2 4 
         4 2 1 3 5 

```

这个想法是首先决定 1 的位置。一旦 n = 5 的 1 的可能排列是，

```
_ _ _ _ 1 
1 _ _ _ _ 
_ _ _ 1 _ 
_ 1 _ _ _ 
_ _ 1 _ _ 
```

一旦我们决定了 1，填充剩余项目的任务就很简单了。我们一列一列地填写剩余的条目。对于每 1，我们遍历它的列，用 2，3，…p 填充它下面的所有条目，用 p+1 填充它上面的所有条目，..我们得到了跟踪。

```
5 3 2 4 1 
1 4 3 5 2 
2 5 4 1 3 
3 1 5 2 4 
4 2 1 3 5 
```

为了确定 1 的初始位置，我们遍历所有行，并跟踪两个列号“左”和“右”。
1)“右”从 n-1 开始，在每隔一行后继续递减。
2)“左”从 0 开始，在每隔一行后继续递增。
以下是上述想法的实现。

## C++

```
// C++ program to construct an n x n
// matrix such that every row and every
// column has distinct values.
#include <iostream>
#include <bits/stdc++.h>

using namespace std;

const int MAX = 100;
int mat[MAX][MAX];

// Fills non-one entries in column j
// Given that there is a "1" at
// position mat[i][j], this function
// fills other entries of column j.
void fillRemaining(int i, int j, int n)
{
    // Initialize value to be filled
    int x = 2;

    // Fill all values below i as 2, 3, ...p
    for (int k = i + 1; k < n; k++)
        mat[k][j] = x++;

    // Fill all values above i
    // as p + 1, p + 2, .. n
    for (int k = 0; k < i; k++)
        mat[k][j] = x++;
}

// Fills entries in mat[][]
// with the given set of rules
void constructMatrix(int n)
{
    // Alternatively fill 1s starting from
    // rightmost and leftmost columns. For
    // example for n = 3, we get { {_ _ 1},
    // {1 _ _} {_ 1 _}}
    int right = n - 1, left = 0;
    for (int i = 0; i < n; i++)
    {
        // If i is even, then fill 
        // next column from right
        if (i % 2 == 0)
        {
            mat[i][right] = 1;

            // After filling 1, fill remaining
            // entries of column "right"
            fillRemaining(i, right, n);

            // Move right one column back
            right--;
        }

        // Fill next column from left
        else
        {
            mat[i][left] = 1;

            // After filling 1, fill remaining
            // entries of column "left"
            fillRemaining(i, left, n);

            // Move left one column forward
            left++;
        }
    }
}

// Driver code
int main()
{
    int n = 5;

    // Passing n to constructMatrix function
    constructMatrix(n);

    // Printing the desired unique matrix
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
            printf("%d ",mat[i][j]);
        printf ("\n");
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct an n x n
// matrix such that every row and every
// column has distinct values.
class GFG
{

    static final int MAX = 100;
    static int[][] mat = new int[MAX][MAX];

    // Fills non-one entries in column j
    // Given that there is a "1" at
    // position mat[i][j], this function
    // fills other entries of column j.
    static void fillRemaining(int i, int j, int n)
    {
        // Initialize value to be filled
        int x = 2;

        // Fill all values below i as 2, 3, ...p
        for (int k = i + 1; k < n; k++)
            mat[k][j] = x++;

        // Fill all values above i
        // as p + 1, p + 2, .. n
        for (int k = 0; k < i; k++)
            mat[k][j] = x++;
    }

    // Fills entries in mat[][]
    // with the given set of rules
    static void constructMatrix(int n)
    {
        // Alternatively fill 1s starting from
        // rightmost and leftmost columns. For
        // example for n = 3, we get { {_ _ 1},
        // {1 _ _} {_ 1 _}}
        int right = n - 1, left = 0;
        for (int i = 0; i < n; i++)
        {
            // If i is even, then fill
            //  next column from right
            if (i % 2 == 0)
            {
                mat[i][right] = 1;

                // After filling 1, fill remaining
                // entries of column "right"
                fillRemaining(i, right, n);

                // Move right one column back
                right--;
            }

            // Fill next column from left
            else
            {
                mat[i][left] = 1;

                // After filling 1, fill remaining
                // entries of column "left"
                fillRemaining(i, left, n);

                // Move left one column forward
                left++;
            }
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;

        // Passing n to constructMatrix function
        constructMatrix(n);

        // Printing the desired unique matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0 ; j < n; j++)
            System.out.print(mat[i][j]+" ");
            System.out.println();
        }
    }
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to construct an n x n
# matrix such that every row and every
# column has distinct values.

MAX = 100;
mat = [[0 for x in range(MAX)] for y in range(MAX)];

# Fills non-one entries in column j
# Given that there is a "1" at
# position mat[i][j], this function
# fills other entries of column j.
def fillRemaining(i, j, n):

    # Initialize value to be filled
    x = 2;

    # Fill all values below i as 2, 3, ...p
    for k in range(i + 1,n):
        mat[k][j] = x;
        x+=1;

    # Fill all values above i
    # as p + 1, p + 2, .. n
    for k in range(i):
        mat[k][j] = x;
        x+=1;

# Fills entries in mat[][]
# with the given set of rules
def constructMatrix(n):

    # Alternatively fill 1s starting from
    # rightmost and leftmost columns. For
    # example for n = 3, we get { {_ _ 1},
    # {1 _ _} {_ 1 _}}
    right = n - 1;
    left = 0;
    for i in range(n):
        # If i is even, then fill
        # next column from right
        if (i % 2 == 0):
            mat[i][right] = 1;

            # After filling 1, fill remaining
            # entries of column "right"
            fillRemaining(i, right, n);

            # Move right one column back
            right-=1;

        # Fill next column from left
        else:
            mat[i][left] = 1;

            # After filling 1, fill remaining
            # entries of column "left"
            fillRemaining(i, left, n);

            # Move left one column forward
            left+=1;

# Driver code
n = 5;

# Passing n to constructMatrix function
constructMatrix(n);

# Printing the desired unique matrix
for i in range(n):
    for j in range(n):
        print(mat[i][j],end=" ");
    print("");

# This code is contributed by mits
```

## C#

```
// C# program to construct an n x n
// matrix such that every row and
// every column has distinct values.
using System;

class GFG
{

    static int MAX = 100;
    static int [,]mat = new int[MAX, MAX];

    // Fills non-one entries in column j
    // Given that there is a "1" at
    // position mat[i][j], this function
    // fills other entries of column j.
    static void fillRemaining(int i, int j, int n)
    {
        // Initialize value to be filled
        int x = 2;

        // Fill all values below i as 2, 3, ...p
        for (int k = i + 1; k < n; k++)
            mat[k, j] = x++;

        // Fill all values above i
        // as p + 1, p + 2, .. n
        for (int k = 0; k < i; k++)
            mat[k, j] = x++;
    }

    // Fills entries in mat[][]
    // with the given set of rules
    static void constructMatrix(int n)
    {
        // Alternatively fill 1s starting from
        // rightmost and leftmost columns. For
        // example for n = 3, we get { {_ _ 1},
        // {1 _ _} {_ 1 _}}
        int right = n - 1, left = 0;
        for (int i = 0; i < n; i++)
        {
            // If i is even, then fill
            // next column from right
            if (i % 2 == 0)
            {
                mat[i, right] = 1;

                // After filling 1, fill remaining
                // entries of column "right"
                fillRemaining(i, right, n);

                // Move right one column back
                right--;
            }

            // Fill next column from left
            else
            {
                mat[i, left] = 1;

                // After filling 1, fill remaining
                // entries of column "left"
                fillRemaining(i, left, n);

                // Move left one column forward
                left++;
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;

        // Passing n to constructMatrix function
        constructMatrix(n);

        // Printing the desired unique matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0 ; j < n; j++)
            Console.Write(mat[i, j]+" ");
            Console.WriteLine();
        }
    }
}

// This code is contributed by nitin mittal
```

## java 描述语言

```
<script>

// javascript program to construct an n x n
// matrix such that every row and every
// column has distinct values.

var MAX = 100;
var mat = Array(MAX).fill(0).
          map(x => Array(MAX).fill(0));

// Fills non-one entries in column j
// Given that there is a "1" at
// position mat[i][j], this function
// fills other entries of column j.
function fillRemaining(i , j , n)
{
    // Initialize value to be filled
    var x = 2;

    // Fill all values below i as 2, 3, ...p
    for (k = i + 1; k < n; k++)
        mat[k][j] = x++;

    // Fill all values above i
    // as p + 1, p + 2, .. n
    for (k = 0; k < i; k++)
        mat[k][j] = x++;
}

// Fills entries in mat
// with the given set of rules
function constructMatrix(n)
{
    // Alternatively fill 1s starting from
    // rightmost and leftmost columns. For
    // example for n = 3, we get { {_ _ 1],
    // {1 _ _} {_ 1 _}}
    var right = n - 1, left = 0;
    for (i = 0; i < n; i++)
    {
        // If i is even, then fill
        //  next column from right
        if (i % 2 == 0)
        {
            mat[i][right] = 1;

            // After filling 1, fill remaining
            // entries of column "right"
            fillRemaining(i, right, n);

            // Move right one column back
            right--;
        }

        // Fill next column from left
        else
        {
            mat[i][left] = 1;

            // After filling 1, fill remaining
            // entries of column "left"
            fillRemaining(i, left, n);

            // Move left one column forward
            left++;
        }
    }
}

// Driver Code
var n = 5;

// Passing n to constructMatrix function
constructMatrix(n);

// Printing the desired unique matrix
for (i = 0; i < n; i++)
{
    for (j = 0 ; j < n; j++)
    document.write(mat[i][j]+" ");
    document.write('<br>');
}

// This code contributed by Princi Singh

</script>
```

**输出:**

```
5 3 2 4 1 
1 4 3 5 2 
2 5 4 1 3 
3 1 5 2 4 
4 2 1 3 5 
```

本文由 **MAZHAR IMAM KHAN** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息