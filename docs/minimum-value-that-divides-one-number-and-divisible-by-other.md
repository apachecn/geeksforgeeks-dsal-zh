# 一个数除以另一个数的最小值

> 原文:[https://www . geeksforgeeks . org/除以一并被其他整除的最小值/](https://www.geeksforgeeks.org/minimum-value-that-divides-one-number-and-divisible-by-other/)

给定两个整数 **p** 和 **q** ，任务是找到最小可能数 **x** ，使得 **q % x = 0** 和 **x % p = 0** 。如果任何数字的条件不成立，则打印 **-1** 。
**示例:**

> **输入:** p = 3，q = 99
> **输出:** 3
> 99 % 3 = 0
> 3 % 3 = 0
> **输入:** p = 2，q = 7
> **输出:** -1

**逼近:**如果一个数 **x** 满足给定条件那么很明显 **q** 将被 **p** 除，即 **q % p = 0** ，因为 **x** 是 **p** 的倍数 **q** 是 **x** 的倍数。
所以 **x** 的最小可能值将是 **p** 和 **q** 的 GCD，当 **q** 不能被 **p** 整除时，则没有数满足给定条件。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum valid number
// that satisfies the given conditions
int minValidNumber(int p, int q)
{
    // If possible
    if (q % p == 0)
        return __gcd(p, q);
    else
        return -1;
}

// Driver Code
int main()
{
    int p = 2, q = 6;
    cout << minValidNumber(p, q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java  implementation of the approach

import java.io.*;

class GFG {

    // Function to calculate gcd
    static int __gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

// Function to return the minimum valid number
// that satisfies the given conditions
static int minValidNumber(int p, int q)
{
    // If possible
    if (q % p == 0)
        return __gcd(p, q);
    else
        return -1;
}

// Driver Code
    public static void main (String[] args) {
        int p = 2, q = 6;
        System.out.print(minValidNumber(p, q));

    // THis code is contributed by  Sachin.
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the minimum
# valid number that satisfies the
# given conditions
def minValidNumber(p, q) :

    # If possible
    if (q % p == 0) :
        return gcd(p, q)
    else :
        return -1

# Driver Code
if __name__ == "__main__" :

    p, q = 2, 6;
    print(minValidNumber(p, q))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to calculate gcd
    static int __gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

// Function to return the minimum valid number
// that satisfies the given conditions
static int minValidNumber(int p, int q)
{
    // If possible
    if (q % p == 0)
        return __gcd(p, q);
    else
        return -1;
}

// Driver Code
public static void Main()
{
    int p = 2, q = 6;
    Console.Write(minValidNumber(p, q));
}
}

// THis code is contributed
// by Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

function gcd($a, $b)
{

    // Everything divides 0
    if($b == 0)

        return $a ;

    return gcd($b , $a % $b);
}

// Function to return the minimum valid
// number that satisfies the given conditions
function minValidNumber($p, $q)
{
    // If possible
    if ($q % $p == 0)
        return gcd($p, $q);
    else
        return -1;
}

// Driver Code
$p = 2;
$q = 6;
echo minValidNumber($p, $q);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to calculate gcd
    function __gcd(a, b)
    {

        // Everything divides 0 
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

    // Function to return the minimum valid number
    // that satisfies the given conditions
    function minValidNumber(p, q)
    {
        // If possible
        if (q % p == 0)
            return __gcd(p, q);
        else
            return -1;
    }  

    let p = 2, q = 6;
    document.write(minValidNumber(p, q));

</script>
```

**Output:** 

```
2
```