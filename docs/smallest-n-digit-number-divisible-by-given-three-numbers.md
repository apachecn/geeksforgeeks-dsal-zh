# 可被给定三个数整除的最小 n 位数

> 原文:[https://www . geesforgeks . org/最小 n 位数可被给定三位数除尽/](https://www.geeksforgeeks.org/smallest-n-digit-number-divisible-by-given-three-numbers/)

给定 x，y，z 和 n，求能被 x，y 和 z 整除的最小 n 位数。

示例:

```
Input : x = 2, y = 3, z = 5
        n = 4
Output : 1020

Input : x = 3, y = 5, z = 7
        n = 2
Output : Not possible
```

1)求最小 n 位数为幂(10，n-1)。
2)求给定的 3 个数 x，y 和 z 的 LCM。
3)求 LCM 除以幂(10，n-1)的余数。
4)将“LCM–余数”加到幂(10，n-1)上。如果这个加法仍然是一个 n 位数，我们返回结果。否则我们就回去了不可能。

**图解:**
假设 n = 4，x，y，z 分别为 2，3，5。
1)首先找到最少的四位数，即 1000，
2) LCM 为 2、3、5，因此 LCM 为 30。
3)找到 1000 % 30 = 10 的提醒
4)从 LCM 中减去余数，30–10 = 20。结果是 1000 + 20 = 1020。

下面是上述方法的实现:

## C++

```
// C++ program to find smallest n digit number
// which is divisible by x, y and z.
#include <bits/stdc++.h>
using namespace std;

// LCM for x, y, z
int LCM(int x, int y, int z)
{
    int ans = ((x * y) / (__gcd(x, y)));
    return ((z * ans) / (__gcd(ans, z)));
}

// returns smallest n digit number divisible
// by x, y and z
int findDivisible(int n, int x, int y, int z)
{
    // find the LCM
    int lcm = LCM(x, y, z);

    // find power of 10 for least number
    int ndigitnumber = pow(10, n-1);

    // reminder after
    int reminder = ndigitnumber % lcm;

    // If smallest number itself divides
    // lcm.
    if (reminder == 0)
         return ndigitnumber;

    // add lcm- reminder number for
    // next n digit number
    ndigitnumber += lcm - reminder;

    // this condition check the n digit
    // number is possible or not
    // if it is possible it return
    // the number else return 0
    if (ndigitnumber < pow(10, n))
        return ndigitnumber;
    else
        return 0;
}

// driver code
int main()
{
    int n = 4, x = 2, y = 3, z = 5;
    int res = findDivisible(n, x, y, z);

    // if number is possible then
    // it print the number
    if (res != 0)
        cout << res;
    else
        cout << "Not possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest n digit number
// which is divisible by x, y and z.
import java.io.*;

public class GFG {

    static int __gcd(int a, int b)
    {

        if (b == 0) {
            return a;
        }
        else {
            return __gcd(b, a % b);
        }
    }

    // LCM for x, y, z
    static int LCM(int x, int y, int z)
    {
        int ans = ((x * y) / (__gcd(x, y)));
        return ((z * ans) / (__gcd(ans, z)));
    }

    // returns smallest n digit number
    // divisible by x, y and z
    static int findDivisible(int n, int x,
                                  int y, int z)
    {

        // find the LCM
        int lcm = LCM(x, y, z);

        // find power of 10 for least number
        int ndigitnumber = (int)Math.pow(10, n - 1);

        // reminder after
        int reminder = ndigitnumber % lcm;

        // If smallest number itself divides
        // lcm.
        if (reminder == 0)
            return ndigitnumber;

        // add lcm- reminder number for
        // next n digit number
        ndigitnumber += lcm - reminder;

        // this condition check the n digit
        // number is possible or not
        // if it is possible it return
        // the number else return 0
        if (ndigitnumber < Math.pow(10, n))
            return ndigitnumber;
        else
            return 0;
    }

    // driver code
    static public void main(String[] args)
    {

        int n = 4, x = 2, y = 3, z = 5;
        int res = findDivisible(n, x, y, z);

        // if number is possible then
        // it print the number
        if (res != 0)
            System.out.println(res);
        else
            System.out.println("Not possible");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find smallest n digit
# number which is divisible by x, y and z.
from fractions import gcd
import math

# LCM for x, y, z
def LCM( x , y , z ):
    ans = int((x * y) / (gcd(x, y)))
    return int((z * ans) / (gcd(ans, z)))

# returns smallest n digit number
# divisible by x, y and z
def findDivisible (n, x, y, z):

    # find the LCM
    lcm = LCM(x, y, z)

    # find power of 10 for least number
    ndigitnumber = math.pow(10, n-1)

    # reminder after
    reminder = ndigitnumber % lcm

    # If smallest number itself
    # divides lcm.
    if reminder == 0:
        return ndigitnumber

    # add lcm- reminder number for
    # next n digit number
    ndigitnumber += lcm - reminder

    # this condition check the n digit
    # number is possible or not
    # if it is possible it return
    # the number else return 0
    if ndigitnumber < math.pow(10, n):
        return int(ndigitnumber)
    else:
        return 0

# driver code
n = 4
x = 2
y = 3
z = 5
res = findDivisible(n, x, y, z)

# if number is possible then
# it print the number
if res != 0:
    print( res)
else:
    print("Not possible")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find smallest n digit number
// which is divisible by x, y and z.
using System;

public class GFG
{

    static int __gcd(int a, int b)
        {

            if(b == 0)
            {
                return a;
            }
            else
            {
                return __gcd(b, a % b);
            }
        }

    // LCM for x, y, z
    static int LCM(int x, int y, int z)
    {
        int ans = ((x * y) / (__gcd(x, y)));
        return ((z * ans) / (__gcd(ans, z)));
    }

    // returns smallest n digit number divisible
    // by x, y and z
    static int findDivisible(int n, int x, int y, int z)
    {
        // find the LCM
        int lcm = LCM(x, y, z);

        // find power of 10 for least number
        int ndigitnumber =(int)Math. Pow(10, n - 1);

        // reminder after
        int reminder = ndigitnumber % lcm;

        // If smallest number itself divides
        // lcm.
        if (reminder == 0)
            return ndigitnumber;

        // add lcm- reminder number for
        // next n digit number
        ndigitnumber += lcm - reminder;

        // this condition check the n digit
        // number is possible or not
        // if it is possible it return
        // the number else return 0
        if (ndigitnumber < Math.Pow(10, n))
            return ndigitnumber;
        else
            return 0;
    }

    // Driver code

    static public void Main ()
    {
        int n = 4, x = 2, y = 3, z = 5;
        int res = findDivisible(n, x, y, z);

        // if number is possible then
        // it print the number
        if (res != 0)
            Console.WriteLine(res);
        else
            Console.WriteLine("Not possible");

    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find smallest n digit number
// which is divisible by x, y and z.

// gcd function
function gcd($a, $b) {
    return ($a % $b) ? gcd($b, $a % $b) : $b;
}

// LCM for x, y, z
function LCM($x, $y, $z)
{
    $ans = floor(($x * $y) / (gcd($x, $y)));
    return floor(($z * $ans) / (gcd($ans, $z)));
}

// returns smallest n digit number divisible
// by x, y and z
function findDivisible($n, $x, $y, $z)
{

    // find the LCM
    $lcm = LCM($x, $y, $z);

    // find power of 10 for least number
    $ndigitnumber = pow(10, $n-1);

    // reminder after
    $reminder = $ndigitnumber % $lcm;

    // If smallest number itself divides
    // lcm.
    if ($reminder == 0)
        return $ndigitnumber;

    // add lcm- reminder number for
    // next n digit number
    $ndigitnumber += $lcm - $reminder;

    // this condition check the n digit
    // number is possible or not
    // if it is possible it return
    // the number else return 0
    if ($ndigitnumber < pow(10, $n))
        return $ndigitnumber;
    else
        return 0;
}

// driver code
    $n = 4;
    $x = 2;
    $y = 3;
    $z = 5;
    $res = findDivisible($n, $x, $y, $z);

    // if number is possible then
    // it print the number
    if ($res != 0)
        echo $res;
    else
        echo "Not possible";

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find smallest n digit number
// which is divisible by x, y and z.
   function __gcd(a, b)
        {

            if(b == 0)
            {
                return a;
            }
            else
            {
                return __gcd(b, a % b);
            }
        }

    // LCM for x, y, z
    function LCM(x, y, z)
    {
        let ans = ((x * y) / (__gcd(x, y)));
        return ((z * ans) / (__gcd(ans, z)));
    }

    // returns smallest n digit number divisible
    // by x, y and z
    function findDivisible(n, x, y, z)
    {

        // find the LCM
        let lcm = LCM(x, y, z);

        // find power of 10 for least number
        let ndigitnumber = Math.pow(10, n - 1);

        // reminder after
        let reminder = ndigitnumber % lcm;

        // If smallest number itself divides
        // lcm.
        if (reminder == 0)
            return ndigitnumber;

        // add lcm- reminder number for
        // next n digit number
        ndigitnumber += lcm - reminder;

        // this condition check the n digit
        // number is possible or not
        // if it is possible it return
        // the number else return 0
        if (ndigitnumber < Math.pow(10, n))
            return ndigitnumber;
        else
            return 0;
    }

// Driver Code

        let n = 4, x = 2, y = 3, z = 5;
        let res = findDivisible(n, x, y, z);

        // if number is possible then
        // it print the number
        if (res != 0)
            document.write(res);
        else
            document.write("Not possible");

      // This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
1020
```