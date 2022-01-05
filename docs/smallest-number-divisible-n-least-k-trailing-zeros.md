# 可被 n 整除且至少有-k 个尾随零的最小数

> 原文:[https://www . geeksforgeeks . org/最小可除数 n-最小 k-尾随零/](https://www.geeksforgeeks.org/smallest-number-divisible-n-least-k-trailing-zeros/)

给出了两个整数 n 和 k。我们的任务是打印 n 的 K-rounding . K-rounding 是最小正整数 X，这样 X 以 K 个或更多个零结束，并且可以被 n 整除.
**示例:**

```
Input :  n = 30, k = 3.
Output : 3000
3000 is the smallest number that
has at-least k 0s and is divisible
by n.

Input : n = 375, k = 4.
Output : 30000
```

**方法 1 :**
蛮力法是从结果= 10 <sup>k</sup> 开始。检查结果是否除以 n，如果是，就是答案，否则增加 10 <sup>k</sup>
**方法二:**高效的方法是计算 10 <sup>k</sup> 和 n
的 LCM，假设 n = 375，k = 4。
结果= 10000。
现在 375 和 10000 的 LCM 是两者除以的最低数。
它将包含 k 个或更多的零(因为它是 10 的倍数 <sup>k</sup> )并且也是 n 的倍数。
下面是实现:

## C++

```
// CPP code to print K-rounded value of n
#include <bits/stdc++.h>
using namespace std;

// Function to compute the rounded value
long long getRounding(long long n, long long k)
{
    long long rounding = pow(10, k);

    // Computing GCD
    long long result = __gcd(rounding, n);

    // Returning LCM (GCD * LCM = n * k)
    return ((rounding * n) / result);
}

// Driver Code
int main()
{

    long long n = 375, k = 4;

    // Function call
    cout << getRounding(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Smallest number divisible by
// n and has at-least k trailing zeros
import java.util.*;

class GFG {

     // Function to find gcd
     static long gcd(long a, long b)
        {
            // Everything divides 0
            if (a == 0 || b == 0)
               return 0;

            // base case
            if (a == b)
                return a;

            // a is greater
            if (a > b)
                return gcd(a-b, b);
            return gcd(a, b-a);
        }

    // Function to compute the rounded value
    public static long getRounding(long n, long k)
    {
        long rounding = (long)Math.pow(10, k);

        // Computing GCD
        long result = gcd(rounding, n);

        // Returning LCM (GCD * LCM = n * k)
        return ((rounding * n) / result);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        long n = 375, k = 4;

        // Function call
        System.out.println( getRounding(n, k));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# python Code For Smallest number
# divisible by n and has
# at-least k trailing zeros

# Function to find gcd
def gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return gcd(a - b, b)

    return gcd(a, b - a)

# Function to compute the
# rounded value
def getRounding(n, k):

    rounding = pow(10, k);

    # Computing GCD
    result = gcd(rounding, n)

    # Returning LCM (GCD * LCM
    # = n * k)
    return ((rounding * n) / result)

# Driver Code

n = 375
k = 4

# Function call
print( int(getRounding(n, k)))

# This code is contributed by Sam007
```

## C#

```
// C# Code For Smallest number
// divisible by n and has
// at-least k trailing zeros
using System;

class GFG {

    // Function to find gcd
    static long gcd(long a, long b)
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

    // Function to compute the rounded value
    public static long getRounding(long n, long k)
    {
        long rounding = (long)Math.Pow(10, k);

        // Computing GCD
        long result = gcd(rounding, n);

        // Returning LCM (GCD * LCM = n * k)
        return ((rounding * n) / result);
    }

    // Driver Code
    public static void Main()
    {
        long n = 375, k = 4;

        // Function call
        Console.Write( getRounding(n, k));

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code For Smallest number
// divisible by n and has
// at-least k trailing zeros
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

// Function to compute
// the rounded value
function getRounding($n, $k)
{
    $rounding = intval(pow(10, $k));

    // Computing GCD
    $result = gcd($rounding, $n);

    // Returning LCM (GCD * LCM = n * k)
    return intval(($rounding * $n) /
                   $result);
}

// Driver code
$n = 375;
$k = 4;

// Function call
echo getRounding($n, $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// javascript Code For Smallest number divisible by
// n and has at-least k trailing zeros

    // Function to find gcd
    function gcd(a , b)
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

    // Function to compute the rounded value
    function getRounding(n , k)
    {
        var rounding =  Math.pow(10, k);

        // Computing GCD
        var result = gcd(rounding, n);

        // Returning LCM (GCD * LCM = n * k)
        return ((rounding * n) / result);
    }

    /* Driver program to test above function */
        var n = 375, k = 4;

        // Function call
        document.write(getRounding(n, k));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
30000
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。