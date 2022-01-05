# 用给定的指数求 N 个斐波那契数的 GCD

> 原文:[https://www . geeksforgeeks . org/find-the-gcd-of-n-Fibonacci-numbers-with-given-index/](https://www.geeksforgeeks.org/find-the-gcd-of-n-fibonacci-numbers-with-given-indices/)

给定 N 个斐波那契数的指数。任务是找到给定指数下斐波那契数的 GCD。
前几个斐波那契数是:

> **0、1、1、2、3、5、8、13、21、34、55、89……**

**注**:指数从零开始。即第 0 个斐波那契数= 0。
**示例** :

```
Input: Indices = {2, 3, 4, 5}
Output: GCD of the fibonacci numbers = 1

Input: Indices = {3, 6, 9} 
Output: GCD of the fibonacci numbers = 2
```

**蛮力法**:蛮力法的解决方法是找出给定指数处存在的所有斐波那契数，计算所有这些数的 GCD，并打印结果。
**有效方法**:有效方法是使用属性:

```
GCD(Fib(M), Fib(N)) = Fib(GCD(M, N))
```

其思想是计算所有指数的 gcd，然后在指数 gcd_1 处找到斐波那契数(其中 gcd_1 是给定指数的 GCD)。
以下是上述方法的实现:

## C++

```
// C++ program to Find the GCD of N Fibonacci
// Numbers with given Indices
#include <bits/stdc++.h>
using namespace std;

// Function to return n'th
// Fibonacci number
int getFib(int n)
{
    /* Declare an array to store Fibonacci numbers. */
    int f[n + 2]; // 1 extra to handle case, n = 0
    int i;

    // 0th and 1st number of the series
    // are 0 and 1
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {
        // Add the previous 2 numbers in the series
        // and store it
        f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Function to Find the GCD of N Fibonacci
// Numbers with given Indices
int find(int arr[], int n)
{
    int gcd_1 = 0;
    // find the gcd of the indices
    for (int i = 0; i < n; i++) {
        gcd_1 = __gcd(gcd_1, arr[i]);
    }

    // find the fibonacci number at
    // index gcd_1
    return getFib(gcd_1);
}

// Driver code
int main()
{
    int indices[] = { 3, 6, 9 };
    int N = sizeof(indices) / sizeof(int);

    cout << find(indices, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the GCD of N Fibonacci
// Numbers with given Indices
import java.io.*;

// Function to return n'th
// Fibonacci number

public class GFG {
    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
        return b;
        if (b == 0)
        return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

static int getFib(int n)
{
    /* Declare an array to store Fibonacci numbers. */
    int f[] = new int[n + 2];
    // 1 extra to handle case, n = 0
    int i;

    // 0th and 1st number of the series
    // are 0 and 1
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {
        // Add the previous 2 numbers in the series
        // and store it
        f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Function to Find the GCD of N Fibonacci
// Numbers with given Indices
static int find(int arr[], int n)
{
    int gcd_1 = 0;
    // find the gcd of the indices
    for (int i = 0; i < n; i++) {
        gcd_1 = __gcd(gcd_1, arr[i]);
    }

    // find the fibonacci number at
    // index gcd_1
    return getFib(gcd_1);
}

// Driver code
    public static void main (String[] args) {
        int indices[] = { 3, 6, 9 };
    int N = indices.length;

    System.out.println( find(indices, N));
    }
}
```

## 蟒蛇 3

```
# Python program to Find the
# GCD of N Fibonacci Numbers
# with given Indices
from math import *

# Function to return n'th
# Fibonacci number
def getFib(n) :

    # Declare an array to store
    # Fibonacci numbers.
    f = [0] * (n + 2) # 1 extra to handle case, n = 0

    # 0th and 1st number of the
    # series are 0 and 1
    f[0], f[1] = 0, 1

    # Add the previous 2 numbers
    # in the series and store it
    for i in range(2, n + 1) :

        f[i] = f[i - 1] + f[i - 2]

    return f[n]

# Function to Find the GCD of N Fibonacci
# Numbers with given Indices
def find(arr, n) :

    gcd_1 = 0

    # find the gcd of the indices
    for i in range(n) :
        gcd_1 = gcd(gcd_1, arr[i])

    # find the fibonacci number
    # at index gcd_1
    return getFib(gcd_1)

# Driver code    
if __name__ == "__main__" :

    indices = [3, 6, 9]
    N = len(indices)

    print(find(indices, N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to Find the GCD
// of N Fibonacci Numbers with
// given Indices
using System;

// Function to return n'th
// Fibonacci number
class GFG
{
// Recursive function to
// return gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0)
    return b;
    if (b == 0)
    return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

static int getFib(int n)
{
    /* Declare an array to
    store Fibonacci numbers. */
    int []f = new int[n + 2];

    // 1 extra to handle case, n = 0
    int i;

    // 0th and 1st number of
    // the series are 0 and 1
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++)
    {
        // Add the previous 2 numbers
        // in the series and store it
        f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Function to Find the GCD
// of N Fibonacci Numbers
// with given Indices
static int find(int []arr, int n)
{
    int gcd_1 = 0;

    // find the gcd of the indices
    for (int i = 0; i < n; i++)
    {
        gcd_1 = __gcd(gcd_1, arr[i]);
    }

    // find the fibonacci number
    // at index gcd_1
    return getFib(gcd_1);
}

// Driver code
public static void Main ()
{
    int []indices = { 3, 6, 9 };
    int N = indices.Length;

    Console.WriteLine(find(indices, N));
}
}

// This code is contributed
// by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find the GCD of
// N Fibonacci Numbers with given
// Indices

// Function to return n'th
// Fibonacci number
function gcd($a, $b)
{
    return $b ? gcd($b, $a % $b) : $a;
}

function getFib($n)
{
    /* Declare an array to store
    Fibonacci numbers. */

    // 1 extra to handle case, n = 0
    $f = array_fill(0, ($n + 2), NULL);

    // 0th and 1st number of the
    // series are 0 and 1
    $f[0] = 0;
    $f[1] = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        // Add the previous 2 numbers
        // in the series and store it
        $f[$i] = $f[$i - 1] + $f[$i - 2];
    }

    return $f[$n];
}

// Function to Find the GCD of N Fibonacci
// Numbers with given Indices
function find(&$arr, $n)
{
    $gcd_1 = 0;

    // find the gcd of the indices
    for ($i = 0; $i < $n; $i++)
    {
        $gcd_1 = gcd($gcd_1, $arr[$i]);
    }

    // find the fibonacci number
    // at index gcd_1
    return getFib($gcd_1);
}

// Driver code
$indices = array(3, 6, 9 );
$N = sizeof($indices);

echo find($indices, $N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// javascript program to
// Find the GCD of N Fibonacci
// Numbers with given Indices

// Function to return n'th
// Fibonacci number

    // Recursive function to return gcd of a and b
    function __gcd(a , b) {
        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    function getFib(n) {
        /* Declare an array to store Fibonacci numbers. */
        var f = Array(n + 2).fill(0);
        // 1 extra to handle case, n = 0
        var i;

        // 0th and 1st number of the series
        // are 0 and 1
        f[0] = 0;
        f[1] = 1;

        for (i = 2; i <= n; i++) {
            // Add the previous 2 numbers in the series
            // and store it
            f[i] = f[i - 1] + f[i - 2];
        }

        return f[n];
    }

    // Function to Find the GCD of N Fibonacci
    // Numbers with given Indices
    function find(arr , n) {
        var gcd_1 = 0;
        // find the gcd of the indices
        for (i = 0; i < n; i++) {
            gcd_1 = __gcd(gcd_1, arr[i]);
        }

        // find the fibonacci number at
        // index gcd_1
        return getFib(gcd_1);
    }

    // Driver code

        var indices = [ 3, 6, 9 ];
        var N = indices.length;

        document.write(find(indices, N));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
2
```