# 计算 nCr % p |集合 3(使用费马小定理)

> 原文:[https://www . geesforgeks . org/compute-NCR-p-set-3-using-Fermat-little-定理/](https://www.geeksforgeeks.org/compute-ncr-p-set-3-using-fermat-little-theorem/)

给定三个数字 n，r 和 p，计算 <sup>n</sup> C <sub>r</sub> mod p 的值，这里 p 是大于 n 的质数，这里 <sup>n</sup> C <sub>r</sub> 是[二项式系数](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)。
**示例:**

```
Input:  n = 10, r = 2, p = 13
Output: 6
Explanation: 10C2 is 45 and 45 % 13 is 6.

Input:  n = 6, r = 2, p = 13
Output: 2
```

我们在之前的帖子中讨论过以下方法。
[计算 <sup>n</sup> C <sub>r</sub> % p |集合 1(引论与动态规划解法)](https://www.geeksforgeeks.org/compute-ncr-p-set-1-introduction-and-dynamic-programming-solution/)
T8】计算 <sup>n</sup> C <sub>r</sub> % p |集合 2(卢卡斯定理)
本文讨论基于费马定理的解法。
**背景:**
**费马小定理与模逆**
费马小定理说明如果 p 是素数，那么对于任意整数 a，数**a<sup>p</sup>–a**是 p 的整数倍，在模算术的记数法中，这表示为:
**a<sup>p</sup>= a(mod p)**

如果 a 不能被 p 整除，费马小定理相当于陈述**a<sup>p–1</sup>–1**是 p 的整数倍，即
**a<sup>p-1</sup>= 1(mod p)**
如果我们把两边乘以 a <sup>-1</sup> ，就得到。
**a<sup>p-2</sup>= a<sup>-1</sup>(mod p)**
所以我们可以找到[模逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)为 <sup>p-2</sup> 。
T60】计算:

```
We know the formula for  nCr 
nCr = fact(n) / (fact(r) x fact(n-r)) 
Here fact() means factorial.

 nCr % p = (fac[n]* modIverse(fac[r]) % p *
               modIverse(fac[n-r]) % p) % p;
Here modIverse() means modular inverse under
modulo p.
```

下面是上述算法的实现。在下面的实现中，数组 fac[]用于存储所有计算的阶乘值。

## C++

```
// A modular inverse based solution to
// compute nCr % p
#include <bits/stdc++.h>
using namespace std;

/* Iterative Function to calculate (x^y)%p
in O(log y) */
unsigned long long power(unsigned long long x,
                                  int y, int p)
{
    unsigned long long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
unsigned long long modInverse(unsigned long long n, 
                                            int p)
{
    return power(n, p - 2, p);
}

// Returns nCr % p using Fermat's little
// theorem.
unsigned long long nCrModPFermat(unsigned long long n,
                                 int r, int p)
{
    // If n<r, then nCr should return 0
    if (n < r)
        return 0;
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    unsigned long long fac[n + 1];
    fac[0] = 1;
    for (int i = 1; i <= n; i++)
        fac[i] = (fac[i - 1] * i) % p;

    return (fac[n] * modInverse(fac[r], p) % p
            * modInverse(fac[n - r], p) % p)
           % p;
}

// Driver program
int main()
{
    // p must be a prime greater than n.
    int n = 10, r = 2, p = 13;
    cout << "Value of nCr % p is "
         << nCrModPFermat(n, r, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A modular inverse based solution to
// compute nCr %
import java.io.*;

class GFG {

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }

        return res;
    }

    // Returns n^(-1) mod p
    static int modInverse(int n, int p)
    {
        return power(n, p - 2, p);
    }

    // Returns nCr % p using Fermat's
    // little theorem.
    static int nCrModPFermat(int n, int r,
                             int p)
    {

          if (n<r)
              return 0;
      // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n-r
        int[] fac = new int[n + 1];
        fac[0] = 1;

        for (int i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[n] * modInverse(fac[r], p)
                % p * modInverse(fac[n - r], p)
                % p)
            % p;
    }

    // Driver program
    public static void main(String[] args)
    {

        // p must be a prime greater than n.
        int n = 10, r = 2, p = 13;
        System.out.println("Value of nCr % p is "
                           + nCrModPFermat(n, r, p));
    }
}

// This code is contributed by Anuj_67.
```

## 蟒蛇 3

```
# Python3 function to
# calculate nCr % p
def ncr(n, r, p):
    # initialize numerator
    # and denominator
    num = den = 1
    for i in range(r):
        num = (num * (n - i)) % p
        den = (den * (i + 1)) % p
    return (num * pow(den,
            p - 2, p)) % p

# p must be a prime
# greater than n
n, r, p = 10, 11, 13
print("Value of nCr % p is",
               ncr(n, r, p))
```

## C#

```
// A modular inverse based solution to
// compute nCr % p
using System;

class GFG {

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }

        return res;
    }

    // Returns n^(-1) mod p
    static int modInverse(int n, int p)
    {
        return power(n, p - 2, p);
    }

    // Returns nCr % p using Fermat's
    // little theorem.
    static int nCrModPFermat(int n, int r,
                             int p)
    {

      if (n<r)
            return 0;
      // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n-r
        int[] fac = new int[n + 1];
        fac[0] = 1;

        for (int i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[n] * modInverse(fac[r], p)
                % p * modInverse(fac[n - r], p)
                % p)
            % p;
    }

    // Driver program
    static void Main()
    {

        // p must be a prime greater than n.
        int n = 10, r = 11, p = 13;
        Console.Write("Value of nCr % p is "
                      + nCrModPFermat(n, r, p));
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A modular inverse
// based solution to
// compute nCr % p

// Iterative Function to
// calculate (x^y)%p
// in O(log y)
function power($x, $y, $p)
{

    // Initialize result
    $res = 1;

    // Update x if it
    // is more than or
    // equal to p
    $x = $x % $p;

    while ($y > 0)
    {

        // If y is odd,
        // multiply x
        // with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be
        // even now
        // y = y/2
        $y = $y >> 1;
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Returns n^(-1) mod p
function modInverse($n, $p)
{
    return power($n, $p - 2, $p);
}

// Returns nCr % p using
// Fermat's little
// theorem.
function nCrModPFermat($n, $r, $p)
{

    if ($n<$r)
          return 0;
      // Base case
    if ($r==0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    //$fac[$n+1];
    $fac[0] = 1;
    for ($i = 1; $i <= $n; $i++)
        $fac[$i] = $fac[$i - 1] *
                        $i % $p;

    return ($fac[$n] * modInverse($fac[$r], $p) % $p *
             modInverse($fac[$n - $r], $p) % $p) % $p;
}

    // Driver Code
    // p must be a prime
    // greater than n.
    $n = 10;
    $r = 2;
    $p = 13;
    echo "Value of nCr % p is ",
         nCrModPFermat($n, $r, $p);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

    // A modular inverse based solution
    // to compute nCr % p

    /* Iterative Function to calculate
    (x^y)%p in O(log y) */
    function power(x, y, p)
    {

        // Initialize result
        let res = 1;

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x
            // with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }

        return res;
    }

    // Returns n^(-1) mod p
    function modInverse(n, p)
    {
        return power(n, p - 2, p);
    }

    // Returns nCr % p using Fermat's
    // little theorem.
    function nCrModPFermat(n, r, p)
    {

      if (n<r)
      {
          return 0;
      }

      // Base case
      if (r == 0)
        return 1;

      // Fill factorial array so that we
      // can find all factorial of r, n
      // and n-r
      let fac = new Array(n + 1);
      fac[0] = 1;

      for (let i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

      return (fac[n] * modInverse(fac[r], p) % p *
              modInverse(fac[n - r], p) % p) % p;
    }

    // p must be a prime greater than n.
    let n = 10, r = 2, p = 13;
    document.write("Value of nCr % p is " +
                    nCrModPFermat(n, r, p));

</script>
```

**Output:** 

```
Value of nCr % p is 6
```

**改进:**
在竞争性编程中，我们可以为给定的上限预先计算 fac[]，这样我们就不必为每个测试用例计算它。我们还可以在任何地方使用无符号 long long int 来避免溢出。
本文由**尼克尔·帕皮塞特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。