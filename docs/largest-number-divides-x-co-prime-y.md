# 除 x 且与 y 同素的最大数

> 原文:[https://www . geesforgeks . org/maximum-number-divides-x-co-prime-y/](https://www.geeksforgeeks.org/largest-number-divides-x-co-prime-y/)

给定两个正数 x 和 y，求最大值整数 a，这样:

1.  a 除以 x，即 x % a = 0
2.  a 和 y 是同素的，即 gcd(a，y) = 1

**例:**

```
Input : x = 15
        y = 3 
Output : a = 5
Explanation: 5 is the max integer 
which satisfies both the conditions.
             15 % 5 =0
             gcd(5, 3) = 1
Hence, output is 5\. 

Input : x = 14
        y = 28
Output : a = 1
Explanation: 14 % 1 =0
             gcd(1, 28) = 1
Hence, output is 1\. 
```

**方法:**在这里，首先我们将通过找到 x 和 y 的最大公约数(gcd)并将 x 除以 gcd 来从 x 中移除 x 和 y 的公因数。
数学上:

```
 *x = x / gcd(x, y) —— STEP1* 
```

现在，我们重复*步骤 1* 直到得到 gcd(x，y) = 1。
最后，我们返回 a = x

## C++

```
// CPP program to find the
// Largest Coprime Divisor

#include <bits/stdc++.h>
using namespace std;

// Recursive function to return gcd
// of a and b
int gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// function to find largest
// coprime divisor
int cpFact(int x, int y)
{
    while (gcd(x, y) != 1) {
        x = x / gcd(x, y);
    }
    return x;
}

// divisor code
int main()
{
    int x = 15;
    int y = 3;
    cout << cpFact(x, y) << endl;
    x = 14;
    y = 28;
    cout << cpFact(x, y) << endl;
    x = 7;
    y = 3;
    cout << cpFact(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find the
// Largest Coprime Divisor
import java.io.*;

class GFG {
    // Recursive function to return gcd
    // of a and b
    static int gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);
        return gcd(a, b - a);
    }

    // function to find largest
    // coprime divisor
    static int cpFact(int x, int y)
    {
        while (gcd(x, y) != 1) {
            x = x / gcd(x, y);
        }
        return x;
    }

    // divisor code
    public static void main(String[] args)
    {
        int x = 15;
        int y = 3;
        System.out.println(cpFact(x, y));
        x = 14;
        y = 28;
        System.out.println(cpFact(x, y));
        x = 7;
        y = 3;
        System.out.println(cpFact(x, y));
    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find the
# Largest Coprime Divisor

# Recursive function to return
# gcd of a and b
def gcd (a, b):

    # Everything divides 0
    if a == 0 or b == 0:
        return 0

    # base case
    if a == b:
        return a

    # a is greater
    if a > b:
        return gcd(a - b, b)

    return gcd(a, b - a)

# function to find largest
# coprime divisor
def cpFact(x, y):
    while gcd(x, y) != 1:
        x = x / gcd(x, y)
    return int(x)

# divisor code
x = 15
y = 3
print(cpFact(x, y))
x = 14
y = 28
print(cpFact(x, y))
x = 7
y = 3
print(cpFact(x, y))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find the
// Largest Coprime Divisor
using System;

class GFG {

    // Recursive function to return gcd
    // of a and b
    static int gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);

        return gcd(a, b - a);
    }

    // function to find largest
    // coprime divisor
    static int cpFact(int x, int y)
    {
        while (gcd(x, y) != 1) {
            x = x / gcd(x, y);
        }

        return x;
    }

    // divisor code
    public static void Main()
    {

        int x = 15;
        int y = 3;
        Console.WriteLine(cpFact(x, y));

        x = 14;
        y = 28;
        Console.WriteLine(cpFact(x, y));

        x = 7;
        y = 3;
        Console.WriteLine(cpFact(x, y));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// Largest Coprime Divisor

// Recursive function to
// return gcd of a and b
function gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return gcd($a - $b, $b);
    return gcd($a, $b - $a);
}

// function to find largest
// coprime divisor
function cpFact( $x, $y)
{
    while (gcd($x, $y) != 1)
    {
        $x = $x / gcd($x, $y);
    }
    return $x;
}

// Driver Code
$x = 15;
$y = 3;
echo cpFact($x, $y), "\n";
$x = 14;
$y = 28;
echo cpFact($x, $y), "\n";
$x = 7;
$y = 3;
echo cpFact($x, $y);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// Largest Coprime Divisor

// Recursive function to
// return gcd of a and b
function gcd(a, b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// function to find largest
// coprime divisor
function cpFact(x, y)
{
    while (gcd(x, y) != 1)
    {
        x = x / gcd(x, y);
    }
    return x;
}

// Driver Code
let x = 15;
let y = 3;
document.write(cpFact(x, y) + "<br>");
x = 14;
y = 28;
document.write(cpFact(x, y), "<br>");
x = 7;
y = 3;
document.write(cpFact(x, y));

// This code is contributed by gfgking

</script>
```

**输出:**

```
5
1
7
```