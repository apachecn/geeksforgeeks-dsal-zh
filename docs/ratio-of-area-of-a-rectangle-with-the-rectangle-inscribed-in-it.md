# 矩形与内接矩形的面积比

> 原文:[https://www . geeksforgeeks . org/内接矩形的矩形面积比/](https://www.geeksforgeeks.org/ratio-of-area-of-a-rectangle-with-the-rectangle-inscribed-in-it/)

给定两个矩形，X 的长宽比分别为 **a:b** 和 Y 的长宽比分别为 **c:d** 。只要边的比例保持不变，这两个矩形都可以调整大小。任务是将第二个矩形放在第一个矩形内，使得至少有一条边相等，并且该边与两个矩形重叠，并求出(第二个矩形所占的空间):(第一个矩形所占的空间)的比率。
**例:**

```
Input: a = 1, b = 1, c = 3, d = 2
Output: 2:3
The dimensions can be 3X3 and 3X2.

Input: a = 4, b = 3, c = 2, d = 2
Output: 3:4
The dimensions can be 4X3 and 3X3
```

**方法:**如果我们使矩形的一边相等，那么所需的比值就是另一边的比值。
考虑 2 种情况:

*   我们应该让 a 和 c 相等。
*   b*c < a*d:我们应该让 b 和 d 相等。

因为比率的两边相乘不会改变它的值。首先试着让 a 和 c 相等，通过将(a:b)乘以 lcm/a，将(c:d)乘以 lcm/c，可以使其等于它们的 lcm，相乘后(b:d)的比值将是所需答案。这个比例可以通过用 gcd(b，d)除 b 和 d 来降低。
以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the ratio
void printRatio(int a, int b, int c, int d)
{
    if (b * c > a * d) {
        swap(c, d);
        swap(a, b);
    }

    // LCM of numerators
    int lcm = (a * c) / __gcd(a, c);

    int x = lcm / a;
    b *= x;

    int y = lcm / c;
    d *= y;

    // Answer in reduced form
    int k = __gcd(b, d);
    b /= k;
    d /= k;

    cout << b << ":" << d;
}

// Driver code
int main()
{
    int a = 4, b = 3, c = 2, d = 2;

    printRatio(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

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

// Function to find the ratio
 static void printRatio(int a, int b, int c, int d)
{
    if (b * c > a * d) {
        int temp = c;
        c =d;
        d =c;
        temp =a;
        a =b;
        b=temp;

    }

    // LCM of numerators
    int lcm = (a * c) / __gcd(a, c);

    int x = lcm / a;
    b *= x;

    int y = lcm / c;
    d *= y;

    // Answer in reduced form
    int k = __gcd(b, d);
    b /= k;
    d /= k;

    System.out.print( b + ":" + d);
}

    // Driver code
    public static void main (String[] args) {
        int a = 4, b = 3, c = 2, d = 2;

    printRatio(a, b, c, d);
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
import math
# Python3 implementation of above approach

# Function to find the ratio
def printRatio(a, b, c, d):
    if (b * c > a * d):
        swap(c, d)
        swap(a, b)

    # LCM of numerators
    lcm = (a * c) / math.gcd(a, c)

    x = lcm / a
    b = int(b * x)

    y = lcm / c
    d = int(d * y)

    # Answer in reduced form
    k = math.gcd(b,d)
    b =int(b / k)
    d = int(d / k)

    print(b,":",d)

# Driver code
if __name__ == '__main__':
    a = 4
    b = 3
    c = 2
    d = 2

    printRatio(a, b, c, d)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach

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

// Function to find the ratio
static void printRatio(int a, int b, int c, int d)
{
    if (b * c > a * d) {
        int temp = c;
        c =d;
        d =c;
        temp =a;
        a =b;
        b=temp;

    }

    // LCM of numerators
    int lcm = (a * c) / __gcd(a, c);

    int x = lcm / a;
    b *= x;

    int y = lcm / c;
    d *= y;

    // Answer in reduced form
    int k = __gcd(b, d);
    b /= k;
    d /= k;

    Console.WriteLine( b + ":" + d);
}

// Driver code

    public static void Main () {
        int a = 4, b = 3, c = 2, d = 2;

    printRatio(a, b, c, d);
    }
}

// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Recursive function to return
// gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0)
        return $b;
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

// Function to find the ratio
function printRatio($a, $b, $c, $d)
{
    if ($b * $c > $a * $d)
    {
        $temp = $c;
        $c = $d;
        $d = $c;

        $temp = $a;
        $a = $b;
        $b = $temp;
    }

    // LCM of numerators
    $lcm = ($a * $c) / __gcd($a, $c);

    $x = $lcm / $a;
    $b *= $x;

    $y = $lcm / $c;
    $d *= $y;

    // Answer in reduced form
    $k = __gcd($b, $d);
    $b /= $k;
    $d /= $k;

    echo $b . ":" . $d;
}

// Driver code
$a = 4; $b = 3; $c = 2; $d = 2;

printRatio($a, $b, $c, $d);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Recursive function to return 
// gcd of a and b 
function __gcd(a, b) 
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
        return __gcd(a - b,b); 
    return __gcd(a, b - a); 
} 

// Function to find the ratio
function printRatio(a, b, c, d)
{
     if (b * c > a * d) 
    {
        temp = c;
        c = d;
        d = c;

        temp = a;
        a = b;
        b = temp;
    }

    // LCM of numerators
    let lcm = (a * c) / __gcd(a, c);

    let x = lcm / a;
    b *= x;

    let y = lcm / c;
    d *= y;

    // Answer in reduced form
    let k = __gcd(b, d);
    b /= k;
    d /= k;

    document.write(b + ":" + d);
}

// Driver code

    let a = 4, b = 3, c = 2, d = 2;
    printRatio(a, b, c, d);

// This code is contributed by Manoj

</script>
```

**Output:** 

```
3:4
```