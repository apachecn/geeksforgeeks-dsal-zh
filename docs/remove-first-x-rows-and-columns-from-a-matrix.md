# 从矩阵中删除前 X 行和列

> 原文:[https://www . geesforgeks . org/remove-first-x-row-and-columns-from-a-matrix/](https://www.geeksforgeeks.org/remove-first-x-rows-and-columns-from-a-matrix/)

给定一个整数 **X** 和一个正方形矩阵 **mat[][]** ，任务是从给定矩阵中删除前 X 行和列，并打印更新后的矩阵。
**例:**

> **输入:**mat[]=
> 【1，2，3，4}，
> 【5，6，7，8}，
> 【8，9，4，2}，
> 【4，8，9，2} }，
> x = 2
> t8【输出:】

**方法:**为所有 **i，j∈X，N–1】**打印矩阵**arr【I】【j】**的元素，其中 **N** 是给定正方形矩阵的顺序。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

const int MAX = 50;

// Function to print the matrix after
// ignoring first x rows and columns
void remove_row_col(int arr[][MAX], int n, int x)
{

    // Ignore first x rows and columns
    for (int i = x; i < n; i++) {
        for (int j = x; j < n; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Order of the square matrix
    int n = 3;
    int arr[][MAX] = { { 1, 2, 3 },
                       { 4, 5, 6 },
                       { 7, 8, 9 } };

    int x = 1;
    remove_row_col(arr, n, x);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG
{

static int MAX = 50;

// Function to print the matrix after
// ignoring first x rows and columns
static void remove_row_col(int arr[][], int n, int x)
{

    // Ignore first x rows and columns
    for (int i = x; i < n; i++)
    {
        for (int j = x; j < n; j++)
        {
            System.out.print( arr[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    // Order of the square matrix
    int n = 3;
    int arr[][] = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } };

    int x = 1;
    remove_row_col(arr, n, x);
}
}

// This code is contributed by
// shk
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the matrix after
# ignoring first x rows and columns
def remove_row_col(arr, n, x):

    # Ignore first x rows and columns
    for i in range(x, n):
        for j in range(x, n):
            print(arr[i][j], end = " ")

        print()

# Driver Code
if __name__ == "__main__":

    # Order of the square matrix
    n = 3
    MAX = 50
    arr = [[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]]

    x = 1
    remove_row_col(arr, n, x)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to print the matrix after
    // ignoring first x rows and columns
    static void remove_row_col(int [,]arr, int n, int x)
    {

        // Ignore first x rows and columns
        for (int i = x; i < n; i++)
        {
            for (int j = x; j < n; j++)
            {
                Console.Write(arr[i, j] + " ");
            }
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main()
    {
        // Order of the square matrix
        int n = 3;
        int [,]arr = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };

        int x = 1;
        remove_row_col(arr, n, x);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MAX = 50;

// Function to print the matrix after
// ignoring first x rows and columns
function remove_row_col($arr, $n, $x)
{

    // Ignore first x rows and columns
    for ($i = $x; $i < $n; $i++)
    {
        for ($j = $x; $j < $n; $j++)
        {
            echo $arr[$i][$j] . " ";
        }
        echo "\n";
    }
}

// Driver Code

// Order of the square matrix
$n = 3;
$arr = array(array( 1, 2, 3 ),
             array( 4, 5, 6 ),
             array( 7, 8, 9 ));

$x = 1;
remove_row_col($arr, $n, $x);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let MAX = 50;

// Function to print the matrix after
// ignoring first x rows and columns
function remove_row_col(arr,n,x)
{

    // Ignore first x rows and columns
    for (let i = x; i < n; i++)
    {
        for (let j = x; j < n; j++)
        {
            document.write( arr[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code

    // Order of the square matrix
    let n = 3;
    let arr = [[ 1, 2, 3 ],
               [ 4, 5, 6 ],
               [ 7, 8, 9 ]];

    let x = 1;
    remove_row_col(arr, n, x);

// This code is contributed by sravan kumar

    </script>
```

**Output:** 

```
5 6 
8 9
```