# 素性检验|集合 3(米勒-拉宾)

> 原文:[https://www . geeksforgeeks . org/primality-test-set-3-miller-rabin/](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)

给定一个数字 n，检查它是否是质数。我们已经介绍并讨论了素性检验的 School 和 Fermat 方法。
[素性测验|第 1 集(引论与学派方法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)
[素性测验|第 2 集(费马方法)](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)
在这篇文章中，讨论了米勒-拉宾方法。这种方法是一种概率方法(像费马方法)，但它通常比费马方法更受欢迎。

**算法:**

```
// It returns false if n is composite and returns true if n
// is probably prime.  k is an input parameter that determines
// accuracy level. Higher value of k indicates more accuracy.
bool isPrime(int n, int k)
1) Handle base cases for n < 3
2) If n is even, return false.
3) Find an odd number d such that n-1 can be written as d*2r. 
   Note that since n is odd, (n-1) must be even and r must be 
   greater than 0.
4) Do following k times
     if (millerTest(n, d) == false)
          return false
5) Return true.

// This function is called for all k trials. It returns 
// false if n is composite and returns true if n is probably
// prime.  
// d is an odd number such that d*2r = n-1 for some r>=1
bool millerTest(int n, int d)
1) Pick a random number 'a' in range [2, n-2]
2) Compute: x = pow(a, d) % n
3) If x == 1 or x == n-1, return true.

// Below loop mainly runs 'r-1' times.
4) Do following while d doesn't become n-1.
     a) x = (x*x) % n.
     b) If (x == 1) return false.
     c) If (x == n-1) return true. 
```

**示例:**

```
Input: n = 13,  k = 2.

1) Compute d and r such that d*2r = n-1, 
     d = 3, r = 2\. 
2) Call millerTest k times.

1<sup>st Iteration:</sup>
1) Pick a random number 'a' in range [2, n-2]
      Suppose a = 4

2) Compute: x = pow(a, d) % n
     x = 43 % 13 = 12

3) Since x = (n-1), return true.

II<sup>nd Iteration:</sup>
1) Pick a random number 'a' in range [2, n-2]
      Suppose a = 5

2) Compute: x = pow(a, d) % n
     x = 53 % 13 = 8

3) x neither 1 nor 12.

4) Do following (r-1) = 1 times
   a) x = (x * x) % 13 = (8 * 8) % 13 = 12
   b) Since x = (n-1), return true.

Since both iterations return true, we return true. 
```

**实现:**
下面是上面算法的实现。

## C++

```
// C++ program Miller-Rabin primality test
#include <bits/stdc++.h>
using namespace std;

// Utility function to do modular exponentiation.
// It returns (x^y) % p
int power(int x, unsigned int y, int p)
{
    int res = 1;      // Initialize result
    x = x % p;  // Update x if it is more than or
                // equal to p
    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

// This function is called for all k trials. It returns
// false if n is composite and returns true if n is
// probably prime.
// d is an odd number such that  d*2<sup>r</sup> = n-1
// for some r >= 1
bool miillerTest(int d, int n)
{
    // Pick a random number in [2..n-2]
    // Corner cases make sure that n > 4
    int a = 2 + rand() % (n - 4);

    // Compute a^d % n
    int x = power(a, d, n);

    if (x == 1  || x == n-1)
       return true;

    // Keep squaring x while one of the following doesn't
    // happen
    // (i)   d does not reach n-1
    // (ii)  (x^2) % n is not 1
    // (iii) (x^2) % n is not n-1
    while (d != n-1)
    {
        x = (x * x) % n;
        d *= 2;

        if (x == 1)      return false;
        if (x == n-1)    return true;
    }

    // Return composite
    return false;
}

// It returns false if n is composite and returns true if n
// is probably prime.  k is an input parameter that determines
// accuracy level. Higher value of k indicates more accuracy.
bool isPrime(int n, int k)
{
    // Corner cases
    if (n <= 1 || n == 4)  return false;
    if (n <= 3) return true;

    // Find r such that n = 2^d * r + 1 for some r >= 1
    int d = n - 1;
    while (d % 2 == 0)
        d /= 2;

    // Iterate given nber of 'k' times
    for (int i = 0; i < k; i++)
         if (!miillerTest(d, n))
              return false;

    return true;
}

// Driver program
int main()
{
    int k = 4;  // Number of iterations

    cout << "All primes smaller than 100: \n";
    for (int n = 1; n < 100; n++)
       if (isPrime(n, k))
          cout << n << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program Miller-Rabin primality test
import java.io.*;
import java.math.*;

class GFG {

    // Utility function to do modular
    // exponentiation. It returns (x^y) % p
    static int power(int x, int y, int p) {

        int res = 1; // Initialize result

        //Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x with result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }

        return res;
    }

    // This function is called for all k trials.
    // It returns false if n is composite and
    // returns false if n is probably prime.
    // d is an odd number such that d*2<sup>r</sup>
    // = n-1 for some r >= 1
    static boolean miillerTest(int d, int n) {

        // Pick a random number in [2..n-2]
        // Corner cases make sure that n > 4
        int a = 2 + (int)(Math.random() % (n - 4));

        // Compute a^d % n
        int x = power(a, d, n);

        if (x == 1 || x == n - 1)
            return true;

        // Keep squaring x while one of the
        // following doesn't happen
        // (i) d does not reach n-1
        // (ii) (x^2) % n is not 1
        // (iii) (x^2) % n is not n-1
        while (d != n - 1) {
            x = (x * x) % n;
            d *= 2;

            if (x == 1)
                return false;
            if (x == n - 1)
                return true;
        }

        // Return composite
        return false;
    }

    // It returns false if n is composite
    // and returns true if n is probably
    // prime. k is an input parameter that
    // determines accuracy level. Higher
    // value of k indicates more accuracy.
    static boolean isPrime(int n, int k) {

        // Corner cases
        if (n <= 1 || n == 4)
            return false;
        if (n <= 3)
            return true;

        // Find r such that n = 2^d * r + 1
        // for some r >= 1
        int d = n - 1;

        while (d % 2 == 0)
            d /= 2;

        // Iterate given nber of 'k' times
        for (int i = 0; i < k; i++)
            if (!miillerTest(d, n))
                return false;

        return true;
    }

    // Driver program
    public static void main(String args[]) {

        int k = 4; // Number of iterations

        System.out.println("All primes smaller "
                                + "than 100: ");

        for (int n = 1; n < 100; n++)
            if (isPrime(n, k))
                System.out.print(n + " ");
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 program Miller-Rabin primality test
import random

# Utility function to do
# modular exponentiation.
# It returns (x^y) % p
def power(x, y, p):

    # Initialize result
    res = 1;

    # Update x if it is more than or
    # equal to p
    x = x % p;
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p;

        # y must be even now
        y = y>>1; # y = y/2
        x = (x * x) % p;

    return res;

# This function is called
# for all k trials. It returns
# false if n is composite and
# returns false if n is
# probably prime. d is an odd
# number such that d*2<sup>r</sup> = n-1
# for some r >= 1
def miillerTest(d, n):

    # Pick a random number in [2..n-2]
    # Corner cases make sure that n > 4
    a = 2 + random.randint(1, n - 4);

    # Compute a^d % n
    x = power(a, d, n);

    if (x == 1 or x == n - 1):
        return True;

    # Keep squaring x while one
    # of the following doesn't
    # happen
    # (i) d does not reach n-1
    # (ii) (x^2) % n is not 1
    # (iii) (x^2) % n is not n-1
    while (d != n - 1):
        x = (x * x) % n;
        d *= 2;

        if (x == 1):
            return False;
        if (x == n - 1):
            return True;

    # Return composite
    return False;

# It returns false if n is
# composite and returns true if n
# is probably prime. k is an
# input parameter that determines
# accuracy level. Higher value of
# k indicates more accuracy.
def isPrime( n, k):

    # Corner cases
    if (n <= 1 or n == 4):
        return False;
    if (n <= 3):
        return True;

    # Find r such that n =
    # 2^d * r + 1 for some r >= 1
    d = n - 1;
    while (d % 2 == 0):
        d //= 2;

    # Iterate given nber of 'k' times
    for i in range(k):
        if (miillerTest(d, n) == False):
            return False;

    return True;

# Driver Code
# Number of iterations
k = 4;

print("All primes smaller than 100: ");
for n in range(1,100):
    if (isPrime(n, k)):
        print(n , end=" ");

# This code is contributed by mits
```

## C#

```
// C# program Miller-Rabin primality test
using System;

class GFG
{

    // Utility function to do modular
    // exponentiation. It returns (x^y) % p
    static int power(int x, int y, int p)
    {

        int res = 1; // Initialize result

        // Update x if it is more than
        // or equal to p
        x = x % p;

        while (y > 0)
        {

            // If y is odd, multiply x with result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }

        return res;
    }

    // This function is called for all k trials.
    // It returns false if n is composite and
    // returns false if n is probably prime.
    // d is an odd number such that d*2<sup>r</sup>
    // = n-1 for some r >= 1
    static bool miillerTest(int d, int n)
    {

        // Pick a random number in [2..n-2]
        // Corner cases make sure that n > 4
        Random r = new Random();
        int a = 2 + (int)(r.Next() % (n - 4));

        // Compute a^d % n
        int x = power(a, d, n);

        if (x == 1 || x == n - 1)
            return true;

        // Keep squaring x while one of the
        // following doesn't happen
        // (i) d does not reach n-1
        // (ii) (x^2) % n is not 1
        // (iii) (x^2) % n is not n-1
        while (d != n - 1)
        {
            x = (x * x) % n;
            d *= 2;

            if (x == 1)
                return false;
            if (x == n - 1)
                return true;
        }

        // Return composite
        return false;
    }

    // It returns false if n is composite
    // and returns true if n is probably
    // prime. k is an input parameter that
    // determines accuracy level. Higher
    // value of k indicates more accuracy.
    static bool isPrime(int n, int k)
    {

        // Corner cases
        if (n <= 1 || n == 4)
            return false;
        if (n <= 3)
            return true;

        // Find r such that n = 2^d * r + 1
        // for some r >= 1
        int d = n - 1;

        while (d % 2 == 0)
            d /= 2;

        // Iterate given nber of 'k' times
        for (int i = 0; i < k; i++)
            if (miillerTest(d, n) == false)
                return false;

        return true;
    }

    // Driver Code
    static void Main()
    {
        int k = 4; // Number of iterations

        Console.WriteLine("All primes smaller " +
                                   "than 100: ");

        for (int n = 1; n < 100; n++)
            if (isPrime(n, k))
                Console.Write(n + " ");
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program Miller-Rabin primality test

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p
function power($x, $y, $p)
{

    // Initialize result
    $res = 1;

    // Update x if it is more than or
    // equal to p
    $x = $x % $p;
    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res*$x) % $p;

        // y must be even now
        $y = $y>>1; // $y = $y/2
        $x = ($x*$x) % $p;
    }
    return $res;
}

// This function is called
// for all k trials. It returns
// false if n is composite and
// returns false if n is
// probably prime. d is an odd
// number such that d*2<sup>r</sup> = n-1
// for some r >= 1
function miillerTest($d, $n)
{

    // Pick a random number in [2..n-2]
    // Corner cases make sure that n > 4
    $a = 2 + rand() % ($n - 4);

    // Compute a^d % n
    $x = power($a, $d, $n);

    if ($x == 1 || $x == $n-1)
    return true;

    // Keep squaring x while one
    // of the following doesn't
    // happen
    // (i) d does not reach n-1
    // (ii) (x^2) % n is not 1
    // (iii) (x^2) % n is not n-1
    while ($d != $n-1)
    {
        $x = ($x * $x) % $n;
        $d *= 2;

        if ($x == 1)     return false;
        if ($x == $n-1) return true;
    }

    // Return composite
    return false;
}

// It returns false if n is
// composite and returns true if n
// is probably prime. k is an
// input parameter that determines
// accuracy level. Higher value of
// k indicates more accuracy.
function isPrime( $n, $k)
{

    // Corner cases
    if ($n <= 1 || $n == 4) return false;
    if ($n <= 3) return true;

    // Find r such that n =
    // 2^d * r + 1 for some r >= 1
    $d = $n - 1;
    while ($d % 2 == 0)
        $d /= 2;

    // Iterate given nber of 'k' times
    for ($i = 0; $i < $k; $i++)
        if (!miillerTest($d, $n))
            return false;

    return true;
}

    // Driver Code
    // Number of iterations
    $k = 4;

    echo "All primes smaller than 100: \n";
    for ($n = 1; $n < 100; $n++)
    if (isPrime($n, $k))
        echo $n , " ";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program Miller-Rabin primality test

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p
function power(x, y, p)
{

    // Initialize result
    let res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;
    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

// This function is called
// for all k trials. It returns
// false if n is composite and
// returns false if n is
// probably prime. d is an odd
// number such that d*2<sup>r</sup> = n-1
// for some r >= 1
function miillerTest(d, n)
{

    // Pick a random number in [2..n-2]
    // Corner cases make sure that n > 4
    let a = 2 + Math.floor(Math.random() * (n-2)) % (n - 4);

    // Compute a^d % n
    let x = power(a, d, n);

    if (x == 1 || x == n-1)
        return true;

    // Keep squaring x while one
    // of the following doesn't
    // happen
    // (i) d does not reach n-1
    // (ii) (x^2) % n is not 1
    // (iii) (x^2) % n is not n-1
    while (d != n-1)
    {
        x = (x * x) % n;
        d *= 2;

        if (x == 1)    
            return false;
        if (x == n-1)
              return true;
    }

    // Return composite
    return false;
}

// It returns false if n is
// composite and returns true if n
// is probably prime. k is an
// input parameter that determines
// accuracy level. Higher value of
// k indicates more accuracy.
function isPrime( n, k)
{

    // Corner cases
    if (n <= 1 || n == 4) return false;
    if (n <= 3) return true;

    // Find r such that n =
    // 2^d * r + 1 for some r >= 1
    let d = n - 1;
    while (d % 2 == 0)
        d /= 2;

    // Iterate given nber of 'k' times
    for (let i = 0; i < k; i++)
        if (!miillerTest(d, n))
            return false;

    return true;
}

// Driver Code
// Number of iterations
let k = 4;

document.write("All primes smaller than 100: <br>");
for (let n = 1; n < 100; n++)
    if (isPrime(n, k))
        document.write(n , " ");

// This code is contributed by gfgking
</script>
```

**输出:**

```
All primes smaller than 100: 
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 
61 67 71 73 79 83 89 97 
```

**这是如何工作的？**
以下是算法背后的一些重要事实:

1.  [费马定理](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)指出，如果 n 是素数，那么每 a，1 < = a < n，a <sup>n-1</sup> % n = 1
2.  基本情况确保 n 必须是奇数。因为 n 是奇数，所以 n-1 必须是偶数。偶数可以写成 d * 2 <sup>s</sup> ，其中 d 是奇数，s > 0。
3.  根据以上两点，对于[2，n-2]范围内的每一个随机选取的数字，a <sup>d*2r</sup> % n 的值必须为 1。
4.  根据[欧几里德引理](https://www.geeksforgeeks.org/euclids-lemma/)，如果 x <sup>2</sup> % n = 1 或者(x<sup>2</sup>–1)% n = 0 或者(x-1)(x+1)% n = 0。然后，n 要成为素数，要么 n 除(x-1)，要么 n 除(x+1)。也就是说要么 x % n = 1 要么 x % n = -1。
5.  从第 2 点和第 3 点，我们可以得出结论

```
    For n to be prime, either
    ad % n = 1 
         OR 
    ad*2i % n = -1 
    for some i, where 0 <= i <= r-1.
```

**下一篇:**
[素性检验|第 4 集(索洛维-斯特拉森)](https://www.geeksforgeeks.org/primality-test-set-4-solovay-strassen/)

本文由 **Ruchir Garg** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息