# 斐波那契数的空间高效迭代法

> 原文:[https://www . geesforgeks . org/space-efficient-iterative-method-Fibonacci-number-set-2/](https://www.geeksforgeeks.org/space-efficient-iterative-method-fibonacci-number-set-2/)

给定一个数字 n，求第 n 个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。注意，F0 = 0，F1 = 1，F2 = 2，…..

**示例:**

```
Input : n = 5
Output : 5

Input :  n = 10
Output : 89
```

我们已经在下面讨论了斐波那契数程序的方法 4 中的递归解。

```
F[2][2] = |1, 1|
          |1, 0|

M[2][2] = |1, 1|
          |1, 0|
F[n][n] = fib(n)  | fib(n-1)
          ------------------
          fib(n-1)| fib(n-2)
```

在这篇文章中，讨论了一种避免额外递归调用堆栈空间的迭代方法。我们还使用了按位运算符来进一步优化。在前面的方法中，我们用 2 除这个数，这样最后我们得到 1，然后我们开始乘法过程

在这种方法中，我们得到第二个 MSB，然后开始与 FxF 矩阵相乘，如果位被设置，则再次与 FxM 矩阵相乘，以此类推。然后我们得到最终的结果。

```
Approach :
1\. First get the MSB of a number.
2\. while (MSB > 0)
      multiply(F, F);
      if (n & MSB)
      multiply(F, M);
      and then shift MSB till MSB != 0
```

## C++

```
// C++ code to find nth fibonacci
#include <bits/stdc++.h>
using namespace std;

// get second MSB
int getMSB(int n)
{
    // consectutively set all the bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // returns the second MSB
    return ((n + 1) >> 2);
}

// Multiply function
void multiply(int F[2][2], int M[2][2])
{
    int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function to calculate F[][]
// raise to the power n
void power(int F[2][2], int n)
{
    // Base case
    if (n == 0 || n == 1)
        return;

    // take 2D array to store number's
    int M[2][2] = { 1, 1, 1, 0 };

    // run loop till MSB > 0
    for (int m = getMSB(n); m; m = m >> 1) {
        multiply(F, F);

        if (n & m) {
            multiply(F, M);
        }
    }
}

// To return fibonacci number
int fib(int n)
{
    int F[2][2] = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1);
    return F[0][0];
}

// Driver Code
int main()
{
    // Given n
    int n = 6;

    cout << fib(n) << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to
// find nth fibonacci

class GFG
{

// get second MSB
static int getMSB(int n)
{
    // consectutively set
    // all the bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // returns the
    // second MSB
    return ((n + 1) >> 2);
}

// Multiply function
static void multiply(int F[][],
                     int M[][])
{
    int x = F[0][0] * M[0][0] +
            F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] +
            F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] +
            F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] +
            F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function to calculate F[][]
// raise to the power n
static void power(int F[][],
                  int n)
{
    // Base case
    if (n == 0 || n == 1)
        return;

    // take 2D array to
    // store number's
    int[][] M ={{1, 1},
                {1, 0}};

    // run loop till MSB > 0
    for (int m = getMSB(n);
             m > 0; m = m >> 1)
    {
        multiply(F, F);

        if ((n & m) > 0)
        {
            multiply(F, M);
        }
    }
}

// To return
// fibonacci number
static int fib(int n)
{
    int[][] F = {{1, 1},   
                 {1, 0}};
    if (n == 0)
        return 0;
    power(F, n - 1);
    return F[0][0];
}

// Driver Code
public static void main(String[] args)
{
    // Given n
    int n = 6;

    System.out.println(fib(n));
}
}

// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python3 code to find nth fibonacci

# get second MSB
def getMSB(n):

    # consectutively set all the bits
    n |= n >> 1
    n |= n >> 2
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    # returns the second MSB
    return ((n + 1) >> 2)

# Multiply function
def multiply(F, M):
    x = F[0][0] * M[0][0] + F[0][1] * M[1][0]
    y = F[0][0] * M[0][1] + F[0][1] * M[1][1]
    z = F[1][0] * M[0][0] + F[1][1] * M[1][0]
    w = F[1][0] * M[0][1] + F[1][1] * M[1][1]

    F[0][0] = x
    F[0][1] = y
    F[1][0] = z
    F[1][1] = w

# Function to calculate F[][]
# raise to the power n
def power(F, n):

    # Base case
    if (n == 0 or n == 1):
        return

    # take 2D array to store number's
    M = [[1, 1], [1, 0]]

    # run loop till MSB > 0
    m = getMSB(n)

    while m:
        multiply(F, F)

        if (n & m):
            multiply(F, M)

        m = m >> 1

# To return fibonacci number
def fib(n):
    F = [[1, 1 ], [1, 0 ]]
    if (n == 0):
        return 0
    power(F, n - 1)
    return F[0][0]

# Driver Code

# Given n
n = 6

print(fib(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# code to find nth fibonacci
using System;

class GFG {

// get second MSB
static int getMSB(int n)
{

    // consectutively set
    // all the bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // returns the
    // second MSB
    return ((n + 1) >> 2);
}

// Multiply function
static void multiply(int [,]F,
                     int [,]M)
{

    int x = F[0,0] * M[0,0] +
            F[0,1] * M[1,0];
    int y = F[0,0] * M[0,1] +
            F[0,1] * M[1,1];
    int z = F[1,0] * M[0,0] +
            F[1,1] * M[1,0];
    int w = F[1,0] * M[0,1] +
            F[1,1] * M[1,1];

    F[0,0] = x;
    F[0,1] = y;
    F[1,0] = z;
    F[1,1] = w;
}

// Function to calculate F[][]
// raise to the power n
static void power(int [,]F,
                    int n)
{

    // Base case
    if (n == 0 || n == 1)
        return;

    // take 2D array to
    // store number's
    int[,] M ={{1, 1},
                {1, 0}};

    // run loop till MSB > 0
    for (int m = getMSB(n);
            m > 0; m = m >> 1)
    {
        multiply(F, F);

        if ((n & m) > 0)
        {
            multiply(F, M);
        }
    }
}

// To return
// fibonacci number
static int fib(int n)
{
    int[,] F = {{1, 1},
                {1, 0}};
    if (n == 0)
        return 0;
    power(F, n - 1);
    return F[0,0];
}

// Driver Code
static public void Main ()
{

    // Given n
    int n = 6;

    Console.WriteLine(fib(n));
}
}

// This code is contributed ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find nth fibonacci

// get second MSB
function getMSB($n)
{

    // consectutively set all the bits
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // returns the second MSB
    return (($n + 1) >> 2);
}

// Multiply function
function multiply(&$F, &$M)
{
    $x = $F[0][0] * $M[0][0] +
         $F[0][1] * $M[1][0];
    $y = $F[0][0] * $M[0][1] +
         $F[0][1] * $M[1][1];
    $z = $F[1][0] * $M[0][0] +
         $F[1][1] * $M[1][0];
    $w = $F[1][0] * $M[0][1] +
         $F[1][1] * $M[1][1];

    $F[0][0] = $x;
    $F[0][1] = $y;
    $F[1][0] = $z;
    $F[1][1] = $w;
}

// Function to calculate F[][]
// raise to the power n
function power(&$F, $n)
{
    // Base case
    if ($n == 0 || $n == 1)
        return;

    // take 2D array to store number's
    $M = array(array(1, 1), array(1, 0));

    // run loop till MSB > 0
    for ($m = getMSB($n); $m; $m = $m >> 1)
    {
        multiply($F, $F);

        if ($n & $m)
        {
            multiply($F, $M);
        }
    }
}

// To return fibonacci number
function fib($n)
{
    $F = array(array( 1, 1 ),
               array( 1, 0 ));
    if ($n == 0)
        return 0;
    power($F, $n - 1);
    return $F[0][0];
}

// Driver Code

// Given n
$n = 6;

echo fib($n) . " ";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript code to find nth fibonacci

// Get second MSB
function getMSB(n)
{

    // Consectutively set
    // all the bits
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Returns the
    // second MSB
    return ((n + 1) >> 2);
}

// Multiply function
function multiply(F, M)
{
    let x = F[0][0] * M[0][0] +
            F[0][1] * M[1][0];
    let y = F[0][0] * M[0][1] +
            F[0][1] * M[1][1];
    let z = F[1][0] * M[0][0] +
            F[1][1] * M[1][0];
    let w = F[1][0] * M[0][1] +
            F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function to calculate F[][]
// raise to the power n
function power(F, n)
{

    // Base case
    if (n == 0 || n == 1)
        return;

    // Take 2D array to
    // store number's
    let M = [ [ 1, 1 ], [ 1, 0 ] ];

    // Run loop till MSB > 0
    for(let m = getMSB(n); m > 0; m = m >> 1)
    {
        multiply(F, F);

        if ((n & m) > 0)
        {
            multiply(F, M);
        }
    }
}

// To return
// fibonacci number
function fib(n)
{
    let F = [ [ 1, 1 ], [ 1, 0 ] ];
    if (n == 0)
        return 0;

    power(F, n - 1);
    return F[0][0];
}

// Driver code

// Given n
let n = 6;

document.write(fib(n));

// This code is contributed by decode2207  

</script>
```

**Output:** 

```
8
```

**时间复杂度:-**O(logn)**空间复杂度:-** O(1)。