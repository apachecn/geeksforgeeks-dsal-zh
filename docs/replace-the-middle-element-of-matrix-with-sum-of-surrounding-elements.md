# 将矩阵的中间元素替换为周围元素的和

> 原文:[https://www . geeksforgeeks . org/将矩阵的中间元素替换为周围元素的总和/](https://www.geeksforgeeks.org/replace-the-middle-element-of-matrix-with-sum-of-surrounding-elements/)

给定奇数维的正方形矩阵 **mat[][]** ，任务是将矩阵最中间元素的值更改为其周围元素的总和。
**例:**

```
Input: 
mat[][] = { {2, 1, 7}, 
            {3, 7, 2}, 
            {5, 4, 9} }
Output:
2 1 7
3 10 2
5 4 9

Input: 
mat[][] = {{1, 3, 5, 6, 7},
           {3, 5, 3, 2, 1},
           {1, 2, 3, 4, 5},
           {7, 9, 2, 1, 6},
           {9, 1, 5, 3, 2} }
Output: 
1 3 5 6 7
3 5 3 2 1
1 2 11 4 5
7 9 2 1 6
9 1 5 3 2
```

**方法:**奇数阶矩阵的中间元素将位于**垫【n/2】【n/2】**的位置。
因此直接更新元素为:

```
mat[n / 2][n / 2] = mat[n / 2 - 1][n / 2]
                  + mat[n / 2][n / 2 - 1]
                  + mat[n / 2 + 1][n / 2]
                  + mat[n / 2][n / 2 + 1]
```

以下是上述方法的实现:

## C++

```
// C++ program to replace the value of the middle element
// of the matrix with the sum of surrounding elements

#include <iostream>
using namespace std;
const int MAX = 100;

// Function to print the matrix
void print(int mat[][MAX], int n)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to change the value of the middle element
// of the matrix to the sum of surrounding elements
void changemiddle(int mat[][MAX], int n)
{
    // Change the middle element
    mat[n / 2][n / 2]
        = mat[n / 2 - 1][n / 2]
          + mat[n / 2][n / 2 - 1]
          + mat[n / 2 + 1][n / 2]
          + mat[n / 2][n / 2 + 1];

    // Function call to print the matrix
    print(mat, n);
}

// Driver code
int main()
{
    int mat[][MAX] = { { 2, 1, 7 },
                       { 3, 7, 2 },
                       { 5, 4, 9 } };

    changemiddle(mat, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace the value of the middle element
// of the matrix with the sum of surrounding elements\

public class GFG{

    // Function to print the matrix
    static void print(int mat[][], int n)
    {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(mat[i][j] + " ");
            }
             System.out.println();
        }
    }

    // Function to change the value of the middle element
    // of the matrix to the sum of surrounding elements
    static void changemiddle(int mat[][], int n)
    {
        // Change the middle element
        mat[n / 2][n / 2]
            = mat[n / 2 - 1][n / 2]
              + mat[n / 2][n / 2 - 1]
              + mat[n / 2 + 1][n / 2]
              + mat[n / 2][n / 2 + 1];

        // Function call to print the matrix
        print(mat, n);
    }

    // Driver code
    public static void main(String []args)
    {
        int mat[][] = { { 2, 1, 7 },
                           { 3, 7, 2 },
                           { 5, 4, 9 } };

        changemiddle(mat, 3);
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 program to replace the value
# of the middle element of the matrix
# with the sum of surrounding elements

MAX = 100

# Function to print the matrix
def printMatrix(mat, n):

    for i in range(n):
        for j in range(n):
            print(mat[i][j], end = " ")

        print()

# Function to change the value of
# the middle element of the matrix
# to the sum of surrounding elements
def changemiddle(mat, n):

    # Change the middle element
    mat[n // 2][n // 2] = (mat[n // 2 - 1][n // 2] +
                           mat[n // 2][n // 2 - 1] +
                           mat[n // 2 + 1][n // 2] +
                           mat[n // 2][n // 2 + 1])

    # Function call to print the matrix
    printMatrix(mat, n)

# Driver Code
if __name__ == "__main__":

    mat = [ [ 2, 1, 7 ],
            [ 3, 7, 2 ],
            [ 5, 4, 9 ]]

    changemiddle(mat, 3)

# This code is contributed
# by rituraj_jain
```

## C#

```
// C# program to replace the value of the middle element
// of the matrix with the sum of surrounding elements

using System;
public class GFG{

    // Function to print the matrix
    static void print(int[,] mat, int n)
    {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                Console.Write(mat[i,j] + " ");
            }
             Console.Write("\n");
        }
    }

    // Function to change the value of the middle element
    // of the matrix to the sum of surrounding elements
    static void changemiddle(int[,] mat, int n)
    {
        // Change the middle element
        mat[n / 2,n / 2]
            = mat[n / 2 - 1,n / 2]
              + mat[n / 2,n / 2 - 1]
              + mat[n / 2 + 1,n / 2]
              + mat[n / 2,n / 2 + 1];

        // Function call to print the matrix
        print(mat, n);
    }

    // Driver code
    public static void Main()
    {
        int[,] mat = { { 2, 1, 7 },
                           { 3, 7, 2 },
                           { 5, 4, 9 } };

        changemiddle(mat, 3);
    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace the value of
// the middle element of the matrix
// with the sum of surrounding elements

// Function to print the matrix
function printmat(&$mat, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            echo ($mat[$i][$j]);
            echo (" ");
        }
        echo ("\n");
    }
}

// Function to change the value of the
// middle element of the matrix to the
// sum of surrounding elements
function changemiddle(&$mat, $n)
{
    // Change the middle element
    $mat[$n / 2][$n / 2] = $mat[$n / 2 - 1][$n / 2] +
                           $mat[$n / 2][$n / 2 - 1] +
                           $mat[$n / 2 + 1][$n / 2] +
                           $mat[$n / 2][$n / 2 + 1];

    // Function call to print the matrix
    printmat($mat, $n);
}

// Driver code
$mat = array(array(2, 1, 7),
             array(3, 7, 2),
             array(5, 4, 9));

changemiddle($mat, 3);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript program to replace the
// value of the middle element
// of the matrix with the sum of
// surrounding elements

    // Function to print the matrix
    function print(mat,n)
    {
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                document.write(mat[i][j] + " ");
            }
             document.write("<br>");
        }
    }

    // Function to change the value of the middle element
    // of the matrix to the sum of surrounding elements
    function changemiddle(mat,n)
    {
        // Change the middle element
        mat[Math.floor(n / 2)][Math.floor(n / 2)]
            = mat[Math.floor(n / 2) - 1][Math.floor(n / 2)]
              + mat[Math.floor(n / 2)][Math.floor(n / 2) - 1]
              + mat[Math.floor(n / 2) + 1][Math.floor(n / 2)]
              + mat[Math.floor(n / 2)][Math.floor(n / 2) + 1];

        // Function call to print the matrix
        print(mat, n);
    }

    // Driver code
    let mat = [ [ 2, 1, 7 ],
            [ 3, 7, 2 ],
            [ 5, 4, 9 ]] ;

    changemiddle(mat, 3)

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2 1 7 
3 10 2 
5 4 9
```

**时间复杂度:** O(n * m)，这里 n 为行数，m 为列数。