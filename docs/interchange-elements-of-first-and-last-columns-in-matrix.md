# 交换矩阵中第一列和最后一列的元素

> 原文:[https://www . geesforgeks . org/interchange-矩阵中第一列和最后一列的元素/](https://www.geeksforgeeks.org/interchange-elements-of-first-and-last-columns-in-matrix/)

给定一个 4 x 4 矩阵，任务是交换第一列和最后一列的元素并显示结果矩阵。
**例:**

```
Input:
8 9 7 6
4 7 6 5
3 2 1 8
9 9 7 7
Output:
6 9 7 8
5 7 6 4
8 2 1 3
7 9 7 9

Input: 
9 7 5 1
2 3 4 1
5 6 6 5
1 2 3 1
Output: 
1 7 5 9
1 3 4 2
5 6 6 5
1 2 3 1
```

方法很简单，我们可以简单地交换矩阵的第一列和最后一列的元素，以获得所需的矩阵作为输出。
以下是上述方法的实现:

## C++

```
// C++ code to swap the element of first
// and last column and display the result
#include <iostream>
using namespace std;

#define n 4

void interchangeFirstLast(int m[][n])
{
    // swapping of element between first
    // and last columns
    for (int i = 0; i < n; i++) {
        int t = m[i][0];
        m[i][0] = m[i][n - 1];
        m[i][n - 1] = t;
    }
}

// Driver function
int main()
{
    // input in the array
    int m[n][n] = { { 8, 9, 7, 6 },
                    { 4, 7, 6, 5 },
                    { 3, 2, 1, 8 },
                    { 9, 9, 7, 7 } };

    interchangeFirstLast(m);

    // printing the interchanged matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            cout << m[i][j] << " ";
        cout << endl;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to swap the element of first
// and last column and display the result

import java.io.*;

class GFG {

static int n = 4;

static void interchangeFirstLast(int m[][])
{
    int cols = n;

    // swapping of element between first
    // and last columns
    for (int i = 0; i < n; i++) {
        int t = m[i][0];
        m[i][0] = m[i][n - 1];
        m[i][n - 1] = t;
    }
}

// Driver function

    public static void main (String[] args) {
            // input in the array
    int m[][] = { { 8, 9, 7, 6 },
                    { 4, 7, 6, 5 },
                    { 3, 2, 1, 8 },
                    { 9, 9, 7, 7 } };

    interchangeFirstLast(m);

    // printing the interchanged matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            System.out.print(m[i][j] + " ");
            System.out.println();
    }
    }
}
// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python3 code to swap the element of
# first and last column and display
# the result

def interchangeFirstLast(mat, n, m):
    rows = n

    # swapping of element between
    # first and last columns
    for i in range(n):
            t = mat[i][0];
            mat[i][0] = mat[i][n-1];
            mat[i][n-1] = t;

# Driver Program
mat = [[8, 9, 7, 6],
       [4, 7, 6, 5],
       [3, 2, 1, 8],
       [9, 9, 7, 7]]

n = 4
m = 4
interchangeFirstLast(mat, n, m)

# printing the interchanged matrix
for i in range(n):
    for j in range(m):
        print(mat[i][j], end = " ")
    print("\n")
```

## C#

```
// C# code to swap the element of first
// and last column and display the result
using System;

class GFG
{

static int n = 4;

static void interchangeFirstLast(int[, ] m)
{
    int cols = n;

    // swapping of element between first
    // and last columns
    for (int i = 0; i < n; i++)
    {
        int t = m[i, 0];
        m[i, 0] = m[i, n - 1];
        m[i, n - 1] = t;
    }
}

// Driver Code
public static void Main ()
{
// input in the array
int[,] m = { { 8, 9, 7, 6 },
                { 4, 7, 6, 5 },
                { 3, 2, 1, 8 },
                { 9, 9, 7, 7 } };

interchangeFirstLast(m);

// printing the interchanged matrix
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < n; j++)
        Console.Write(m[i, j] + " ");
        Console.WriteLine();
}
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to swap the element of first
// and last column and display the result

function interchangeFirstLast($m, $n)
{
    $cols = $n;

    // swapping of element between first
    // and last columns
    for ($i = 0; $i < $n; $i++)
    {
        $t = $m[$i][0];
        $m[$i][0] = $m[$i][$n - 1];
        $m[$i][$n - 1] = $t;
    }
    return $m ;
}

// Driver Code

// input in the array
$m = array( array( 8, 9, 7, 6 ),
            array (4, 7, 6, 5 ),
            array (3, 2, 1, 8 ),
            array (9, 9, 7, 7 ));

$n = 4 ;
$m = interchangeFirstLast($m,$n);

// printing the interchanged matrix
for ($i = 0; $i < $n; $i++)
{
    for ($j = 0; $j < $n; $j++)
        echo $m[$i][$j], " ";

    echo "\n" ;
}

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript code to swap the element of first
// and last column and display the result
n = 4

function interchangeFirstLast(m)
{
    // swapping of element between first
    // and last columns
    for (var i = 0; i < n; i++)
    {
        var t = m[i][0];
        m[i][0] = m[i][n - 1];
        m[i][n - 1] = t;
    }
}

// Driver function
// input in the array
m = [ [ 8, 9, 7, 6 ],
                [ 4, 7, 6, 5 ],
                [ 3, 2, 1, 8 ],
                [ 9, 9, 7, 7 ] ];
interchangeFirstLast(m);

// printing the interchanged matrix
for (var i = 0; i < n; i++)
{
    for (var j = 0; j < n; j++)
        document.write( m[i][j] + " ");
    document.write("<br>");
}

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
6 9 7 8 
5 7 6 4 
8 2 1 3 
7 9 7 9
```