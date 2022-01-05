# 在 M 个范围内应用增量操作后打印矩阵

> 原文:[https://www . geesforgeks . org/print-matrix-applied-increment-operations-in-m-ranges/](https://www.geeksforgeeks.org/print-matrix-after-applying-increment-operations-in-m-ranges/)

给定尺寸为 **N * N** 的二维矩阵 **mat[][]** ，矩阵的所有元素最初都是 **0** 。需要对矩阵进行多个查询(M 个范围)，其中每个查询由四个整数组成 **X1** 、 **Y1** 、 **X2** 和 **Y2** ，任务是将 **1** 添加到**mat【X1】【Y1】**和**mat【X2】【Y2】**之间的所有单元格中(包括二者)，并最终打印更新后矩阵的内容。
**例:**

> **输入:** N = 2，q[][] = { { 0，0，1，1 }，{ 0，0，0，1 } }
> **输出:**
> 2 2
> 1 1
> 第一次查询后:mat[][] = { {1，1 }，{1，1} }
> 第二次查询后:mat[][] = { {2，2}，{1，1} }
> **输入:** N = 5，q[][]= } 3，4 } }
> **输出:**
> 1 1 1 1 1
> 1 1 2 1 2 2
> 2 2 2 2 2 2
> 2 2 2
> 0 0 0 0

**方式:**对于每个查询 **(X1，Y1)** 表示子矩阵的左上角单元格， **(X2，Y2)** 表示子矩阵的右下角单元格。对于每个左上角单元格，在左上角元素中添加 **1** ，并从右下角单元格旁边的元素(如果有)中减去 **1** 。
然后保持原始(现已修改)矩阵中所有元素的累计总和，每次相加时，当前总和就是当前位置的元素(已更新)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to update and print the
// matrix after performing queries
void updateMatrix(int n, int q[3][4])
{
    int i, j;
    int mat[n][n];
    for(int i = 0; i < n; i++)
    for(int j = 0; j < n; j++)
    mat[i][j] = 0;
    for (i = 0; i < 3; i++)
    {
        int X1 = q[i][0];
        int Y1 = q[i][1];
        int X2 = q[i][2];
        int Y2 = q[i][3];

        // Add 1 to the first element of
        // the sub-matrix
        mat[X1][Y1]++;

        // If there is an element after the
        // last element of the sub-matrix
        // then decrement it by 1
        if (Y2 + 1 < n)
            mat[X2][Y2 + 1]--;
        else if (X2 + 1 < n)
            mat[X2 + 1][0]--;
    }

    // Calculate the running sum
    int sum = 0;
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            sum += mat[i][j];

            // Print the updated element
            cout << sum << " ";
        }

        // Next line
        cout << endl;
    }
}

// Driver code
int main()
{

    // Size of the matrix
    int n = 5;

    // Queries
    int q[3][4] = {{ 0, 0, 1, 2 },
                   { 1, 2, 3, 4 },
                   { 1, 4, 3, 4 }};

    updateMatrix(n, q);
    return 0;
}

// This code is contributed by chandan_jnu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to update and print the matrix
    // after performing queries
    static void updateMatrix(int n, int q[][], int mat[][])
    {
        int i, j;
        for (i = 0; i < q.length; i++) {
            int X1 = q[i][0];
            int Y1 = q[i][1];
            int X2 = q[i][2];
            int Y2 = q[i][3];

            // Add 1 to the first element of the sub-matrix
            mat[X1][Y1]++;

            // If there is an element after the last element
            // of the sub-matrix then decrement it by 1
            if (Y2 + 1 < n)
                mat[X2][Y2 + 1]--;
            else if (X2 + 1 < n)
                mat[X2 + 1][0]--;
        }

        // Calculate the running sum
        int sum = 0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                sum += mat[i][j];

                // Print the updated element
                System.out.print(sum + " ");
            }

            // Next line
            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Size of the matrix
        int n = 5;
        int mat[][] = new int[n][n];

        // Queries
        int q[][] = { { 0, 0, 1, 2 },
                      { 1, 2, 3, 4 },
                      { 1, 4, 3, 4 } };

        updateMatrix(n, q, mat);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to update and print the matrix
# after performing queries
def updateMatrix(n, q, mat):

    for i in range(0, len(q)):
            X1 = q[i][0];
            Y1 = q[i][1];
            X2 = q[i][2];
            Y2 = q[i][3];

            # Add 1 to the first element of
            # the sub-matrix
            mat[X1][Y1] = mat[X1][Y1] + 1;

            # If there is an element after the
            # last element of the sub-matrix
            # then decrement it by 1
            if (Y2 + 1 < n):
                mat[X2][Y2 + 1] = mat[X2][Y2 + 1] - 1;
            elif (X2 + 1 < n):
                mat[X2 + 1][0] = mat[X2 + 1][0] - 1;

    # Calculate the running sum
    sum = 0;
    for i in range(0, n):
        for j in range(0, n):
            sum =sum + mat[i][j];

            # Print the updated element
            print(sum, end = ' ');

        # Next line
        print(" ");

# Driver code

# Size of the matrix
n = 5;
mat = [[0 for i in range(n)]
          for i in range(n)];

# Queries
q = [[ 0, 0, 1, 2 ],
     [ 1, 2, 3, 4 ],
     [ 1, 4, 3, 4 ]];

updateMatrix(n, q, mat);

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# implementation of the above approach

using System;

public class GFG {

    // Function to update and print the matrix
    // after performing queries
    static void updateMatrix(int n, int [,]q, int [,]mat)
    {
        int i, j;
        for (i = 0; i < q.GetLength(0); i++) {
            int X1 = q[i,0];
            int Y1 = q[i,1];
            int X2 = q[i,2];
            int Y2 = q[i,3];

            // Add 1 to the first element of the sub-matrix
            mat[X1,Y1]++;

            // If there is an element after the last element
            // of the sub-matrix then decrement it by 1
            if (Y2 + 1 < n)
                mat[X2,Y2 + 1]--;
            else if (X2 + 1 < n)
                mat[X2 + 1,0]--;
        }

        // Calculate the running sum
        int sum = 0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                sum += mat[i,j];

                // Print the updated element
                Console.Write(sum + " ");
            }

            // Next line
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {

        // Size of the matrix
        int n = 5;
        int [,]mat = new int[n,n];

        // Queries
        int [,]q = { { 0, 0, 1, 2 },
                    { 1, 2, 3, 4 },
                    { 1, 4, 3, 4 } };

        updateMatrix(n, q, mat);
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to update and print the
// matrix after performing queries
function updateMatrix($n, $q, $mat)
{
    for ($i = 0; $i < sizeof($q); $i++)
    {
        $X1 = $q[$i][0];
        $Y1 = $q[$i][1];
        $X2 = $q[$i][2];
        $Y2 = $q[$i][3];

        // Add 1 to the first element of
        // the sub-matrix
        $mat[$X1][$Y1]++;

        // If there is an element after the last
        // element of the sub-matrix then decrement
        // it by 1
        if ($Y2 + 1 < $n)
            $mat[$X2][$Y2 + 1]--;
        else if ($X2 + 1 < $n)
            $mat[$X2 + 1][0]--;
    }

    // Calculate the running sum
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            $sum += $mat[$i][$j];

            // Print the updated element
            echo($sum . " ");
        }

        // Next line
        echo("\n");
    }
}

// Driver code

// Size of the matrix
$n = 5;
$mat = array_fill(0, $n,
       array_fill(0, $n, 0));

// Queries
$q = array(array( 0, 0, 1, 2 ),
           array( 1, 2, 3, 4 ),
           array( 1, 4, 3, 4 ));

updateMatrix($n, $q, $mat);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to update and print the matrix
    // after performing queries
    function updateMatrix(n, q, mat)
    {
        let i, j;
        for (i = 0; i < q.length; i++) {
            let X1 = q[i][0];
            let Y1 = q[i][1];
            let X2 = q[i][2];
            let Y2 = q[i][3];

            // Add 1 to the first element of the sub-matrix
            mat[X1][Y1]++;

            // If there is an element after the last element
            // of the sub-matrix then decrement it by 1
            if (Y2 + 1 < n)
                mat[X2][Y2 + 1]--;
            else if (X2 + 1 < n)
                mat[X2 + 1][0]--;
        }

        // Calculate the running sum
        let sum = 0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                sum += mat[i][j];

                // Print the updated element
                document.write(sum + " ");
            }

            // Next line
            document.write("</br>");
        }
    }

    // Size of the matrix
    let n = 5;
    let mat = new Array(n);
    for(let i = 0; i < n; i++)
    {
        mat[i] = new Array(n);
        for(let j = 0; j < n; j++)
        {
            mat[i][j] = 0;
        }
    }

    // Queries
    let q = [ [ 0, 0, 1, 2 ],
              [ 1, 2, 3, 4 ],
              [ 1, 4, 3, 4 ] ];

    updateMatrix(n, q, mat);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
1 1 1 1 1 
1 1 2 1 2 
2 2 2 2 2 
2 2 2 2 2 
0 0 0 0 0
```