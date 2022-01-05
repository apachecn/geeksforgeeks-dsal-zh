# 高效计算 nCr 值的程序

> 原文:[https://www . geeksforgeeks . org/高效计算 ncr 价值的程序/](https://www.geeksforgeeks.org/program-to-calculate-the-value-of-ncr-efficiently/)

给定两个数字 n，r ( n>=r)。任务是为 n 的大值找到 C(n，r)的值。

**示例:**

```
Input: n = 30, r = 15
Output: 155117520
C(30, 15) is 155117520 by  30!/((30-15)!*15!)

Input: n = 50, r = 25
Output: 126410606437752
```

**方法:**利用以下知识可以创建一个简单的代码:

```
C(n, r) = [n * (n-1) * .... * (n-r+1)] / [r * (r-1) * .... * 1]
```

然而，对于大的 n，r 值，乘积可能溢出，因此在每次迭代中，我们用当前变量的 gcd 除以乘积的值。

以下是所需的实现:

## C++

```
// C++ implementation to find nCr
#include <bits/stdc++.h>
using namespace std;

// Function to find the nCr
void printNcR(int n, int r)
{

    // p holds the value of n*(n-1)*(n-2)...,
    // k holds the value of r*(r-1)...
    long long p = 1, k = 1;

    // C(n, r) == C(n, n-r),
    // choosing the smaller value
    if (n - r < r)
        r = n - r;

    if (r != 0) {
        while (r) {
            p *= n;
            k *= r;

            // gcd of p, k
            long long m = __gcd(p, k);

            // dividing by gcd, to simplify
            // product division by their gcd
            // saves from the overflow
            p /= m;
            k /= m;

            n--;
            r--;
        }

        // k should be simplified to 1
        // as C(n, r) is a natural number
        // (denominator should be 1 ) .
    }

    else
        p = 1;

    // if our approach is correct p = ans and k =1
    cout << p << endl;
}

// Driver code
int main()
{
    int n = 50, r = 25;

    printNcR(n, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find nCr

class GFG {

    // Function to find the nCr
    static void printNcR(int n, int r)
    {

        // p holds the value of n*(n-1)*(n-2)...,
        // k holds the value of r*(r-1)...
        long p = 1, k = 1;

        // C(n, r) == C(n, n-r),
        // choosing the smaller value
        if (n - r < r) {
            r = n - r;
        }

        if (r != 0) {
            while (r > 0) {
                p *= n;
                k *= r;

                // gcd of p, k
                long m = __gcd(p, k);

                // dividing by gcd, to simplify
                // product division by their gcd
                // saves from the overflow
                p /= m;
                k /= m;

                n--;
                r--;
            }

            // k should be simplified to 1
            // as C(n, r) is a natural number
            // (denominator should be 1 ) .
        }
        else {
            p = 1;
        }

        // if our approach is correct p = ans and k =1
        System.out.println(p);
    }

    static long __gcd(long n1, long n2)
    {
        long gcd = 1;

        for (int i = 1; i <= n1 && i <= n2; ++i) {
            // Checks if i is factor of both integers
            if (n1 % i == 0 && n2 % i == 0) {
                gcd = i;
            }
        }
        return gcd;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 50, r = 25;

        printNcR(n, r);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find nCr

from math import *

# Function to find the nCr

def printNcR(n, r):

    # p holds the value of n*(n-1)*(n-2)...,
    # k holds the value of r*(r-1)...
    p = 1
    k = 1

    # C(n, r) == C(n, n-r),
    # choosing the smaller value
    if (n - r < r):
        r = n - r

    if (r != 0):
        while (r):
            p *= n
            k *= r

            # gcd of p, k
            m = gcd(p, k)

            # dividing by gcd, to simplify product
            # division by their gcd saves from
            # the overflow
            p //= m
            k //= m

            n -= 1
            r -= 1

        # k should be simplified to 1
        # as C(n, r) is a natural number
        # (denominator should be 1 )

    else:
        p = 1

    # if our approach is correct p = ans and k =1
    print(p)

# Driver code
if __name__ == "__main__":
    n = 50
    r = 25

    printNcR(n, r)

# this code is contributed by
# ChitraNayal
```

## C#

```
// C# implementation to find nCr

using System;

public class GFG {

    // Function to find the nCr
    static void printNcR(int n, int r)
    {

        // p holds the value of n*(n-1)*(n-2)...,
        // k holds the value of r*(r-1)...
        long p = 1, k = 1;

        // C(n, r) == C(n, n-r),
        // choosing the smaller value
        if (n - r < r) {
            r = n - r;
        }

        if (r != 0) {
            while (r > 0) {
                p *= n;
                k *= r;

                // gcd of p, k
                long m = __gcd(p, k);

                // dividing by gcd, to simplify
                // product division by their gcd
                // saves from the overflow
                p /= m;
                k /= m;

                n--;
                r--;
            }

            // k should be simplified to 1
            // as C(n, r) is a natural number
            // (denominator should be 1 ) .
        }
        else {
            p = 1;
        }

        // if our approach is correct p = ans and k =1
        Console.WriteLine(p);
    }

    static long __gcd(long n1, long n2)
    {
        long gcd = 1;

        for (int i = 1; i <= n1 && i <= n2; ++i) {
            // Checks if i is factor of both integers
            if (n1 % i == 0 && n2 % i == 0) {
                gcd = i;
            }
        }
        return gcd;
    }

    // Driver code
    static public void Main()
    {
        int n = 50, r = 25;
        printNcR(n, r);
    }
    // This code is contributed by ajit.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find nCr

// Function to find the nCr
function printNcR($n, $r) {

        // p holds the value of n*(n-1)*(n-2)...,
        // k holds the value of r*(r-1)...
        $p = 1;
        $k = 1;

        // C(n, r) == C(n, n-r),
        // choosing the smaller value
        if ($n - $r < $r) {
            $r = $n - $r;
        }

        if ($r != 0) {
            while ($r > 0) {
                $p *= $n;
                $k *= $r;

                // gcd of p, k
                $m = __gcd($p, $k);

                // dividing by gcd, to simplify product
                // division by their gcd saves from the overflow
                $p /= $m;
                $k /= $m;

                $n--;
                $r--;
            }

            // k should be simplified to 1
            // as C(n, r) is a natural number
            // (denominator should be 1 ) .
        } else {
            $p = 1;
        }

        // if our approach is correct p = ans and k =1
        echo ($p);
    }

    function  __gcd($n1, $n2) {
         $gcd = 1;

        for ($i = 1; $i <= $n1 && $i <= $n2; ++$i) {
            // Checks if i is factor of both integers
            if ($n1 % $i == 0 && $n2 % $i == 0) {
                $gcd = $i;
            }
        }
        return $gcd;
    }

        // Driver code
        $n = 50;
        $r = 25;
        printNcR($n, $r);

//This code is contributed by Sachin.

?>
```

## java 描述语言

```
<script>

// Javascript implementation to find nCr

function __gcd(n1, n2)
{
    var gcd = 1;

    for (var i = 1; i <= n1 && i <= n2; ++i) {
        // Checks if i is factor of both integers
        if (n1 % i == 0 && n2 % i == 0) {
            gcd = i;
        }
    }
    return gcd;
}

// Function to find the nCr
function printNcR(n, r)
{

    // p holds the value of n*(n-1)*(n-2)...,
    // k holds the value of r*(r-1)...
    var p = 1, k = 1;

    // C(n, r) == C(n, n-r),
    // choosing the smaller value
    if (n - r < r)
        r = n - r;

    if (r != 0) {
        while (r) {
            p *= n;
            k *= r;

            // gcd of p, k
            var m = __gcd(p, k);

            // dividing by gcd, to simplify
            // product division by their gcd
            // saves from the overflow
            p /= m;
            k /= m;

            n--;
            r--;
        }

        // k should be simplified to 1
        // as C(n, r) is a natural number
        // (denominator should be 1 ) .
    }

    else
        p = 1;

    // if our approach is correct p = ans and k =1
    document.write(p);
}

// Driver code
var n = 50, r = 25;
printNcR(n, r);

</script>
```

**Output**

```
126410606437752
```

**时间复杂度:**O(R Log N)
T3】辅助空间: O(1)