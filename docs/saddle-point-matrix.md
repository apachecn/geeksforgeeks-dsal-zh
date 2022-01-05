# 矩阵中的鞍点

> 原文:[https://www.geeksforgeeks.org/saddle-point-matrix/](https://www.geeksforgeeks.org/saddle-point-matrix/)

给定一个 n×n 大小的矩阵，任务是找到矩阵的鞍点。鞍点是矩阵的一个元素，它是行中的最小元素，列中的最大元素。
**例:**

```
Input: Mat[3][3] = { {1, 2, 3},
                  {4, 5, 6},
                  {7, 8, 9}}
Output: 7
7 is minimum in its row and maximum in its column.

Input: Mat[3][3] = {{1, 2, 3},
                    {4, 5, 6},
                    {10, 18, 4}}
Output: No saddle point
```

一个**简单的解决方法**是逐个遍历所有矩阵元素，检查元素是否为鞍点。
一个**高效的解决方案**基于以下步骤。
逐个遍历所有行，并对每一行 I 执行以下操作

1.  找到当前行的最小元素，并存储最小元素的列索引。
2.  检查最小行元素在其列中是否也是最大值。我们在这里使用存储的列索引。
3.  如果是，那么鞍点 else 继续到矩阵的末尾。

下面是上述步骤的实现。

## C++

```
// C++ program to illustrate Saddle point
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Function to find saddle point
bool findSaddlePoint(int mat[MAX][MAX], int n)
{
    // Process all rows one by one
    for (int i = 0; i < n; i++)
    {
        // Find the minimum element of row i.
        // Also find column index of the minimum element
        int min_row = mat[i][0], col_ind = 0;
        for (int j = 1; j < n; j++)
        {
            if (min_row > mat[i][j])
            {
                min_row = mat[i][j];
                col_ind = j;
            }
        }

        // Check if the minimum element of row is also
        // the maximum element of column or not
        int k;
        for (k = 0; k < n; k++)

            // Note that col_ind is fixed
            if (min_row < mat[k][col_ind])
                break;

        // If saddle point is present in this row then
        // print it
        if (k == n)
        {
           cout << "Value of Saddle Point " << min_row;
           return true;
        }
    }

    // If Saddle Point not found
    return false;
}

// Driver code
int main()
{
    int mat[MAX][MAX] = {{1, 2, 3},
                        {4, 5, 6},
                        {7, 8, 9}};
    int n = 3;
    if (findSaddlePoint(mat, n) == false)
       cout << "No Saddle Point ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate Saddle point

class Test
{
    // Method to find saddle point
    static boolean findSaddlePoint(int mat[][    ], int n)
    {
        // Process all rows one by one
        for (int i = 0; i < n; i++)
        {
            // Find the minimum element of row i.
            // Also find column index of the minimum element
            int min_row = mat[i][0], col_ind = 0;
            for (int j = 1; j < n; j++)
            {
                if (min_row > mat[i][j])
                {
                    min_row = mat[i][j];
                    col_ind = j;
                }
            }

            // Check if the minimum element of row is also
            // the maximum element of column or not
            int k;
            for (k = 0; k < n; k++)

                // Note that col_ind is fixed
                if (min_row < mat[k][col_ind])
                    break;

            // If saddle point is present in this row then
            // print it
            if (k == n)
            {
               System.out.println("Value of Saddle Point " + min_row);
               return true;
            }
        }

        // If Saddle Point not found
        return false;
    }

    // Driver method
    public static void main(String[] args)
    {
        int mat[][] = {{1, 2, 3},
                      {4, 5, 6},
                     {7, 8, 9}};

        int n = 3;
        if (findSaddlePoint(mat, n) == false)
            System.out.println("No Saddle Point ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to illustrate
# Saddle point

# Method to find saddle point
def findSaddlePoint(mat, n):

    # Process all rows one
    # by one
    for i in range(n):

        # Find the minimum element
        # of row i.
        # Also find column index of
        # the minimum element
        min_row = mat[i][0];
        col_ind = 0;
        for j in range(1, n):
            if (min_row > mat[i][j]):
                min_row = mat[i][j];
                col_ind = j;

        # Check if the minimum element
        # of row is also the maximum
        # element of column or not
        k = 0;
        for k in range(n):

            # Note that col_ind is fixed
            if (min_row < mat[k][col_ind]):
                break;
            k += 1;

        # If saddle point present in this
        # row then print
        if (k == n):
            print("Value of Saddle Point ",
                  min_row);
            return True;

    # If Saddle Point found
    return False;

# Driver method
if __name__ == '__main__':

    mat = [[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]];

    n = 3;
    if (findSaddlePoint(mat, n) ==
        False):
        print("No Saddle Po");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to illustrate Saddle point
using System;

class GFG {

    // Method to find saddle point
    static bool findSaddlePoint(int [,] mat,
                                int n)
    {

        // Process all rows one by one
        for (int i = 0; i < n; i++)
        {

            // Find the minimum element of
            // row i. Also find column index
            // of the minimum element
            int min_row = mat[i, 0], col_ind = 0;
            for (int j = 1; j < n; j++)
            {
                if (min_row > mat[i, j])
                {
                    min_row = mat[i, j];
                    col_ind = j;
                }
            }

            // Check if the minimum element
            // of row is also the maximum
            // element of column or not
            int k;
            for (k = 0; k < n; k++)

                // Note that col_ind is fixed
                if (min_row < mat[k, col_ind])
                    break;

            // If saddle point is present in this row then
            // print it
            if (k == n)
            {
                Console.WriteLine("Value of Saddle Point "
                                                + min_row);
                return true;
            }
        }

        // If Saddle Point not found
        return false;
    }

    // Driver code
    public static void Main()
    {
        int [,] mat = {{1, 2, 3},
                       {4, 5, 6},
                       {7, 8, 9}};

        int n = 3;
        if (findSaddlePoint(mat, n) == false)
            Console.WriteLine("No Saddle Point ");
    }
}

// This code is contributed by KRV.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate
// Saddle point

$MAX = 100;

// Function to find saddle point
function findSaddlePoint( $mat, $n)
{
    // Process all rows one by one
    for ( $i = 0; $i < $n; $i++)
    {
        // Find the minimum element
        // of row i. Also find column
        // index of the minimum element
        $min_row = $mat[$i][0];
        $col_ind = 0;
        for ( $j = 1; $j < $n; $j++)
        {
            if ($min_row > $mat[$i][$j])
            {
                $min_row = $mat[$i][$j];
                $col_ind = $j;
            }
        }

        // Check if the minimum element of
        // row is also the maximum element
        // of column or not
        $k;
        for ($k = 0; $k < $n; $k++)

            // Note that col_ind is fixed
            if ($min_row < $mat[$k][$col_ind])
                break;

        // If saddle point is present in
        // this row then print it
        if ($k == $n)
        {
        echo "Value of Saddle Point " ,
                              $min_row;
        return true;
        }
    }

    // If Saddle Point not found
    return false;
}

// Driver code
$mat = array(array(1, 2, 3),
             array(4, 5, 6),
             array (7, 8, 9));
$n = 3;
if (findSaddlePoint($mat, $n) == false)
echo "No Saddle Point ";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to illustrate Saddle point

// Method to find saddle point
function findSaddlePoint(mat, n)
{

    // Process all rows one by one
        for (let i = 0; i < n; i++)
        {

            // Find the minimum element of row i.
            // Also find column index of the minimum element
            let min_row = mat[i][0], col_ind = 0;
            for (let j = 1; j < n; j++)
            {
                if (min_row > mat[i][j])
                {
                    min_row = mat[i][j];
                    col_ind = j;
                }
            }

            // Check if the minimum element of row is also
            // the maximum element of column or not
            let k;
            for (k = 0; k < n; k++)

                // Note that col_ind is fixed
                if (min_row < mat[k][col_ind])
                    break;

            // If saddle point is present in this row then
            // print it
            if (k == n)
            {
               document.write("Value of Saddle Point " + min_row+"<br>");
               return true;
            }
        }

        // If Saddle Point not found
        return false;
}

// Driver method
let mat = [[1, 2, 3],
                      [4, 5, 6],
                     [7, 8, 9]];

        let n = 3;
        if (findSaddlePoint(mat, n) == false)
            document.write("No Saddle Point ");

// This code is contributed by rag2127
</script>
```

**输出:**

```
Value of Saddle Point 7
```

**练习:**
矩阵中可以有多个鞍点吗？
本文由**萨希尔·查布拉(杀手)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。