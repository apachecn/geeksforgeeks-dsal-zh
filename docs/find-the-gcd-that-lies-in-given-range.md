# 找到给定范围内的 GCD

> 原文:[https://www . geeksforgeeks . org/find-the-gcd-躺在给定范围内/](https://www.geeksforgeeks.org/find-the-gcd-that-lies-in-given-range/)

给定两个正整数 **a** 和 **b** 和一个范围**【低，高】**。任务是找出在给定范围内的 a 和 b 的最大公约数。如果范围内没有除数，打印-1。
**举例:**

```
Input : a = 9, b = 27, low = 1, high = 5
Output : 3
3 is the highest number that lies in range 
[1, 5] and is common divisor of 9 and 27.

Input : a = 9, b = 27, low = 10, high = 11
Output : -1
```

思路是求 a 和 b 的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) GCD(a，b)现在观察，GCD(a，b)的除数也是 a 和 b 的除数，所以我们将迭代一个循环 **i** 从 1 到 sqrt(GCD(a，b))，检查 **i** 是否除了 GCD(a，b)。另外，观察如果 **i** 是 GCD(a，b)的除数，那么 **GCD(a，b)/i** 也将是除数。所以，对于每次迭代，如果我对 GCD(a，b)进行除法，我们会发现 **i** 和 **GCD(a，b)/i** 的最大值，如果它们在范围内的话。
以下是本办法的实施情况:

## C++

```
// CPP Program to find the Greatest Common divisor
// of two number which is in given range
#include <bits/stdc++.h>
using namespace std;

// Return the greatest common divisor
// of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Return the gretest common divisor of a
// and b which lie in the given range.
int maxDivisorRange(int a, int b, int l, int h)
{
    int g = gcd(a, b);
    int res = -1;

    // Loop from 1 to sqrt(GCD(a, b).
    for (int i = l; i * i <= g && i <= h; i++)

        // if i divides the GCD(a, b), then
        // find maximum of three numbers res,
        // i and g/i
        if (g % i == 0)
            res = max({res, i, g / i});

    return res;
}

// Driven Program
int main()
{
    int a = 3, b = 27, l = 1, h = 5;
    cout << maxDivisorRange(a, b, l, h) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Greatest Common
// divisor of two number which is in given
// range
import java.io.*;

class GFG {

    // Return the greatest common divisor
    // of two numbers
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Return the gretest common divisor of a
    // and b which lie in the given range.
    static int maxDivisorRange(int a, int b,
                                   int l, int h)
    {
        int g = gcd(a, b);
        int res = -1;

        // Loop from 1 to sqrt(GCD(a, b).
        for (int i = l; i * i <= g && i <= h; i++)

            // if i divides the GCD(a, b), then
            // find maximum of three numbers res,
            // i and g/i
            if (g % i == 0)
                res = Math.max(res,
                             Math.max(i, g / i));

        return res;
    }

    // Driven Program
    public static void main (String[] args)
    {
        int a = 3, b = 27, l = 1, h = 5;
        System.out.println(
             maxDivisorRange(a, b, l, h));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to find the
# Greatest Common divisor
# of two number which is
# in given range

# Return the greatest common
# divisor of two numbers
def gcd(a, b):
    if(b == 0):
        return a;
    return gcd(b, a % b);

# Return the gretest common
# divisor of a and b which
# lie in the given range.
def maxDivisorRange(a, b, l, h):
    g = gcd(a, b);
    res = -1;
    # Loop from 1 to
    # sqrt(GCD(a, b).
    i = l;
    while(i * i <= g and i <= h):
        # if i divides the GCD(a, b),
        # then find maximum of three
        # numbers res, i and g/i
        if(g % i == 0):
            res = max(res,max(i, g/i));
        i+=1;
    return int(res);

# Driver Code
if __name__ == "__main__":
    a = 3;
    b = 27;
    l = 1;
    h = 5;

    print(maxDivisorRange(a, b, l, h));

# This code is contributed by mits
```

## C#

```
// C# Program to find the Greatest Common
// divisor of two number which is in given
// range
using System;

class GFG {

    // Return the greatest common divisor
    // of two numbers
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Return the gretest common divisor of a
    // and b which lie in the given range.
    static int maxDivisorRange(int a, int b,
                                int l, int h)
    {
        int g = gcd(a, b);
        int res = -1;

        // Loop from 1 to sqrt(GCD(a, b).
        for (int i = l; i * i <= g && i <= h; i++)

            // if i divides the GCD(a, b), then
            // find maximum of three numbers res,
            // i and g/i
            if (g % i == 0)
                res = Math.Max(res,
                            Math.Max(i, g / i));

        return res;
    }

    // Driven Program
    public static void Main ()
    {
        int a = 3, b = 27, l = 1, h = 5;
        Console.WriteLine(
            maxDivisorRange(a, b, l, h));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// Greatest Common divisor
// of two number which is
// in given range

// Return the greatest common
// divisor of two numbers
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// Return the gretest common
// divisor of a and b which
// lie in the given range.
function maxDivisorRange($a, $b,
                         $l, $h)
{
    $g = gcd($a, $b);
    $res = -1;

    // Loop from 1 to
    // sqrt(GCD(a, b).
    for ($i = $l; $i * $i <= $g and
                  $i <= $h; $i++)

        // if i divides the GCD(a, b),
        // then find maximum of three
        // numbers res, i and g/i
        if ($g % $i == 0)
            $res = max($res,
                   max($i, $g / $i));

    return $res;
}

// Driver Code
$a = 3; $b = 27;
$l = 1; $h = 5;

echo maxDivisorRange($a, $b, $l, $h);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find the Greatest Common
// divisor of two number which is in given
// range

    // Return the greatest common divisor
    // of two numbers
    function gcd(a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Return the gretest common divisor of a
    // and b which lie in the given range.
    function maxDivisorRange(a , b , l , h) {
        var g = gcd(a, b);
        var res = -1;

        // Loop from 1 to sqrt(GCD(a, b).
        for (i = l; i * i <= g && i <= h; i++)

            // if i divides the GCD(a, b), then
            // find maximum of three numbers res,
            // i and g/i
            if (g % i == 0)
                res = Math.max(res, Math.max(i, g / i));

        return res;
    }

    // Driven Program

        var a = 3, b = 27, l = 1, h = 5;
        document.write(maxDivisorRange(a, b, l, h));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
3
```