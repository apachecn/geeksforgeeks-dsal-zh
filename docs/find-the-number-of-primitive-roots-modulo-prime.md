# 求本原根模素数

> 原文:[https://www . geeksforgeeks . org/find-本原根数-模-质数/](https://www.geeksforgeeks.org/find-the-number-of-primitive-roots-modulo-prime/)

给定一个质数![p ](img/a51d7abe813b8734c255a7254c4a08d8.png "Rendered by QuickLaTeX.com")。任务是统计![p ](img/a51d7abe813b8734c255a7254c4a08d8.png "Rendered by QuickLaTeX.com")的所有原始根。
A [**本原根**](https://en.wikipedia.org/wiki/Primitive_root_modulo_n) 是整数 **x (1 < = x < p)** ，使得整数**x–1，x<sup>2</sup>–1，…，x<sup>p–2</sup>–1**可被![p ](img/a51d7abe813b8734c255a7254c4a08d8.png "Rendered by QuickLaTeX.com")整除，但**x<sup>p–1</sup>–1**可被![p ](img/a51d7abe813b8734c255a7254c4a08d8.png "Rendered by QuickLaTeX.com")整除。
**例:**

> **输入:** P = 3
> **输出:** 1
> 模 3 的唯一本原根是 2。
> **输入:** P = 5
> **输出:** 2
> 模 5 的本原根是 2 和 3。

**方法:**所有素数总是至少有一个本原根。因此，使用[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)我们可以说 f(p-1)是必需的答案，其中 f(n)是欧拉全能函数。
以下是上述方法的实施:

## C++

```
// CPP program to find the number of
// primitive roots modulo prime
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// primitive roots modulo p
int countPrimitiveRoots(int p)
{
    int result = 1;
    for (int i = 2; i < p; i++)
        if (__gcd(i, p) == 1)
            result++;

    return result;
}

// Driver code
int main()
{
    int p = 5;

    cout << countPrimitiveRoots(p - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of
// primitive roots modulo prime

import java.io.*;

class GFG {
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

// Function to return the count of
// primitive roots modulo p
static int countPrimitiveRoots(int p)
{
    int result = 1;
    for (int i = 2; i < p; i++)
        if (__gcd(i, p) == 1)
            result++;

    return result;
}

// Driver code
    public static void main (String[] args) {
            int p = 5;

    System.out.println( countPrimitiveRoots(p - 1));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find the number
# of primitive roots modulo prime
from math import gcd

# Function to return the count of
# primitive roots modulo p
def countPrimitiveRoots(p):
    result = 1
    for i in range(2, p, 1):
        if (gcd(i, p) == 1):
            result += 1

    return result

# Driver code
if __name__ == '__main__':
    p = 5

    print(countPrimitiveRoots(p - 1))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number of
// primitive roots modulo prime

using System;

class GFG {
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

// Function to return the count of
// primitive roots modulo p
static int countPrimitiveRoots(int p)
{
    int result = 1;
    for (int i = 2; i < p; i++)
        if (__gcd(i, p) == 1)
            result++;

    return result;
}

// Driver code
     static public void Main (String []args) {
            int p = 5;

    Console.WriteLine( countPrimitiveRoots(p - 1));
    }
}
// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// primitive roots modulo prime

// Recursive function to return
// gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0)
    return b;

    if ($b == 0)
    return $a;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// Function to return the count of
// primitive roots modulo p
function countPrimitiveRoots($p)
{
    $result = 1;
    for ($i = 2; $i < $p; $i++)
        if (__gcd($i, $p) == 1)
            $result++;

    return $result;
}

// Driver code
$p = 5;

echo countPrimitiveRoots($p - 1);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number of
// primitive roots modulo prime

 // Recursive function to return gcd of a and b 
 function __gcd( a,  b) 
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

// Function to return the count of
// primitive roots modulo p
function countPrimitiveRoots(p)
{
    var result = 1;
    for (var i = 2; i < p; i++)
        if (__gcd(i, p) == 1)
            result++;

    return result;
}

// Driver code
var p = 5;
document.write( countPrimitiveRoots(p - 1));

</script>
```

**Output:** 

```
2
```