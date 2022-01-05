# 给定的 3 个数字应除以的最大数字，以使它们剩下相同的余数

> 原文:[https://www . geesforgeks . org/最大数字-叶子-余数-除-给定-三个数字/](https://www.geeksforgeeks.org/largest-number-leaves-remainder-divided-given-three-numbers/)

给定三个数，我们的任务是找到最大的数，当给定三个数时，除以这个数会得到相同的余数。可以假设所有给定的数字都是以递增的顺序给出的。

示例:

```
Input : a = 62, b = 132, c = 237 
Output : 35
35 leads to same remainder 27 when divides 
62, 132 and 237.

Input : a = 74, b = 272, c = 584
Output : 6
```

这个想法是基于这样一个事实，如果一个数剩下相同的余数 a，b 和 c，那么它将划分它们的差异。让我们理解假设 x 是我们的结果。设 **a = x*d1 + r** 其中 r 是 a 除以 x 的余数，同样我们可以写出 **b = x*d2 + r** 和 **b = x*d3 + r** 。这里的逻辑是，我们首先找到所有三对的差，然后找到差的最大公约数，以使结果最大化。

以下是上述想法的实现。

## C++

```
// C++ program to find the largest numbers that
// leads to same remainder when divides given
// three sorted numbers
#include <bits/stdc++.h>
using namespace std;

//__gcd function
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// function return number which divides these
// three number and leaves same remainder .
int sameRemainder(int a, int b, int c)
{
    // We find the differences of all three  pairs
    int a1 = (b - a), b1 = (c - b), c1 = (c - a);

    // Return GCD of three differences.
    return gcd(a1, gcd(b1, c1));
}

// driver program
int main()
{
    int a = 62, b = 132, c = 237;
    cout << sameRemainder(a, b, c) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// numbers that leads to same
// remainder when divides given
// three sorted numbers

class GFG {

//__gcd function
static int gcd(int a, int b)
{
    if (a == 0)
    return b;
    return gcd(b % a, a);
}

// function return number which divides these
// three number and leaves same remainder .
static int sameRemainder(int a, int b, int c)
{
    // We find the differences of all three pairs
    int a1 = (b - a), b1 = (c - b), c1 = (c - a);

    // Return GCD of three differences.
    return gcd(a1, gcd(b1, c1));
}

// Driver code
public static void main(String[] args)
{
    int a = 62, b = 132, c = 237;
    System.out.println(sameRemainder(a, b, c));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# the largest numbers that
# leads to same remainder
# when divides given
# three sorted numbers

#__gcd function
def gcd(a,b):

    if (a == 0):
        return b
    return gcd(b % a, a)

# function return number
# which divides these
# three number and leaves
# same remainder .
def sameRemainder(a,b,c):

    # We find the differences
    # of all three  pairs
    a1 = (b - a)
    b1 = (c - b)
    c1 = (c - a)

    # Return GCD of three differences.
    return gcd(a1, gcd(b1, c1))

# Driver program

a = 62
b = 132
c = 237
print(sameRemainder(a, b, c))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find the largest
// numbers that leads to same
// remainder when divides given
// three sorted numbers
using System;

class GFG {

// gcd function
static int gcd(int a, int b)
{
    if (a == 0)
    return b;
    return gcd(b % a, a);
}

// function return number which divides
// these three number and leaves same
// remainder .
static int sameRemainder(int a, int b, int c)
{
    // We find the differences of all three pairs
    int a1 = (b - a), b1 = (c - b), c1 = (c - a);

    // Return GCD of three differences.
    return gcd(a1, gcd(b1, c1));
}

// Driver code
public static void Main()
{
    int a = 62, b = 132, c = 237;
    Console.WriteLine(sameRemainder(a, b, c));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// largest numbers that leads
// to same remainder when
// divides given three sorted
// numbers

//__gcd function
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// function return number
// which divides these
// three number and
// leaves same remainder .
function sameRemainder( $a, $b, $c)
{

    // We find the differences
    // of all three pairs
    $a1 = ($b - $a);
    $b1 = ($c - $b);
    $c1 = ($c - $a);

    // Return GCD of
    // three differences.
    return gcd($a1, gcd($b1, $c1));
}

    // Driver Code
    $a = 62;
    $b = 132;
    $c = 237;
    echo sameRemainder($a, $b, $c) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the largest
// numbers that leads to same remainder
// when divides given three sorted numbers

//__gcd function
function gcd(a, b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function return number which divides these
// three number and leaves same remainder .
function sameRemainder(a, b, c)
{

    // We find the differences of all three pairs
    var a1 = (b - a), b1 = (c - b), c1 = (c - a);

    // Return GCD of three differences.
    return gcd(a1, gcd(b1, c1));
}

// Driver code
var a = 62, b = 132, c = 237;

document.write(sameRemainder(a, b, c));

// This code is contributed by noob2000

</script>
```

**输出:**

```
35
```

**时间复杂度:** O(对数 N)

**辅助空间:** O(1)