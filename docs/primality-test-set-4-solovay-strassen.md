# 素性检验|集合 4(索洛维-斯特拉森)

> 原文:[https://www . geesforgeks . org/primality-test-set-4-solovay-strassen/](https://www.geeksforgeeks.org/primality-test-set-4-solovay-strassen/)

在本系列的前几篇文章中，我们已经介绍了素性测试。

*   [素性测验|第一套(入门和学校方法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)
*   [素性检验|集合 2(费马方法)](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)
*   [素性检验|集合 3(米勒-拉宾)](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)

索洛维-斯特拉森素性检验是一种概率检验，用来确定一个数是复合数还是可能是素数。
在深入研究代码之前，我们需要了解一些关键术语和概念，以便能够对该算法进行编码。

**背景:**
**勒让德符号:**这个符号被定义为一对整数 a 和 p，这样 p 就是质数。它由(a/p)表示，计算如下:

```
      = 0    if a%p = 0
(a/p) = 1    if there exists an integer k such that k2 = a(mod p)
      = -1   otherwise.
```

欧拉证明了:

```
 (a/p) = a((p-1)/2)%p Condition (i)
```

**雅可比符号:**这个符号是勒让德符号的推广，其中 p 被 n 代替，其中 n 是

```
n = p1k1 * .. * pnkn
```

，那么雅可比符号定义为:

```
(a/n) = ((a/p1)k1) * ((a/p2)k2) *.....* ((a/pn)kn)
```

如果 n 取质数，那么雅可比等于勒让德符号。这些符号具有某些**属性**–
1)(a/n)= 0，如果 gcd(a，n)！= 1，因此(0/n) = 0。这是因为如果 gcd(a，n)！= 1，那么必须有一个素数π，这样π就能同时除 a 和 n。在这种情况下(a/pi)= 0[根据勒让德符号的定义]。
2) (ab/n) = (a/n) * (b/n)。很容易从事实(ab/p) = (a/p)(b/p)中推导出来(这里(a/p)是勒让德符号)。
3)如果 a 是偶数，那么(a/n) = (2/n)*((a/2)/n)。可以看出:

```
      = 1 if n = 1 ( mod 8 ) or n = 7 ( mod 8 )
(2/n) = -1 if n = 3 ( mod 8 ) or n = 5 ( mod 8 )
      = 0 otherwise
```

```
4) (a/n) = (n/a) * (-1)((a - 1)(n - 1) / 4)  if a and n are both odd.
```

**算法:**
我们选择一个数 n 来测试它的素性和一个在[2，n-1]范围内的随机数 a，并计算它的雅可比(a/n)，如果 n 是一个素数，那么雅可比将等于勒让德，它将满足欧拉给出的条件(I)。如果它不满足给定的条件，那么 n 是复合的，程序将停止。就像其他概率素性测试一样，它的准确性也与迭代次数成正比。因此，我们对测试进行了多次迭代，以获得更准确的结果。

**注:**我们对计算偶数的雅可比不感兴趣，因为我们已经知道除了 2 以外，它们都不是素数。

**伪代码:**

```
Algorithm for Jacobian:
Step 1    //base cases omitted
Step 2     if a>n then
Step 3         return (a mod n)/n
Step 4     else

Step 5         return (-1)((a - 1)/2)((n - 1)/2)(a/n)
Step 6     endif
```

```
Algorithm for Solovay-Strassen:
Step 1    Pick a random element a < n
Step 2    if gcd(a, n) > 1 then
Step 3        return COMPOSITE
Step 4    end if
Step 5    Compute a(n - 1)/2 using repeated squaring
          and (a/n) using Jacobian algorithm.
Step 6    if (a/n) not equal to a(n - 1)/2 then
Step 7        return composite
Step 8    else
Step 9        return prime
Step 10   endif
```

**实施:**

## C++

```
// C++ program to implement Solovay-Strassen
// Primality Test
#include <bits/stdc++.h>
using namespace std;

// modulo function to perform binary exponentiation
long long modulo(long long base, long long exponent,
                                      long long mod)
{
    long long x = 1;
    long long y = base;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            x = (x * y) % mod;

        y = (y * y) % mod;
        exponent = exponent / 2;
    }

    return x % mod;
}

// To calculate Jacobian symbol of a given number
int calculateJacobian(long long a, long long n)
{
    if (!a)
        return 0;// (0/n) = 0

    int ans = 1;
    if (a < 0)
    {
        a = -a; // (a/n) = (-a/n)*(-1/n)
        if (n % 4 == 3)
            ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
    }

    if (a == 1)
        return ans;// (1/n) = 1

    while (a)
    {
        if (a < 0)
        {
            a = -a;// (a/n) = (-a/n)*(-1/n)
            if (n % 4 == 3)
                ans = -ans;// (-1/n) = -1 if n = 3 (mod 4)
        }

        while (a % 2 == 0)
        {
            a = a / 2;
            if (n % 8 == 3 || n % 8 == 5)
                ans = -ans;

        }

        swap(a, n);

        if (a % 4 == 3 && n % 4 == 3)
            ans = -ans;
        a = a % n;

        if (a > n / 2)
            a = a - n;

    }

    if (n == 1)
        return ans;

    return 0;
}

// To perform the Solovay-Strassen Primality Test
bool solovoyStrassen(long long p, int iterations)
{
    if (p < 2)
        return false;
    if (p != 2 && p % 2 == 0)
        return false;

    for (int i = 0; i < iterations; i++)
    {
        // Generate a random number a
        long long a = rand() % (p - 1) + 1;
        long long jacobian = (p + calculateJacobian(a, p)) % p;
        long long mod = modulo(a, (p - 1) / 2, p);

        if (!jacobian || mod != jacobian)
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    int iterations = 50;
    long long num1 = 15;
    long long num2 = 13;

    if (solovoyStrassen(num1, iterations))
        printf("%d is prime\n",num1);
    else
        printf("%d is composite\n",num1);

    if (solovoyStrassen(num2, iterations))
        printf("%d is prime\n",num2);
    else
        printf("%d is composite\n",num2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Solovay-Strassen
// Primality Test
import java.util.Scanner;
import java.util.Random;

class GFG{

// Modulo function to perform
// binary exponentiation
static long modulo(long base,
                   long exponent,
                   long mod)
{
    long x = 1;
    long y = base;

    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            x = (x * y) % mod;

        y = (y * y) % mod;
        exponent = exponent / 2;

    }
    return x % mod;
}

// To calculate Jacobian symbol of
// a given number
static long calculateJacobian(long a, long n)
{
    if (n <= 0 || n % 2 == 0)
        return 0;

    long ans = 1L;

    if (a < 0)
    {
        a = -a; // (a/n) = (-a/n)*(-1/n)
        if (n % 4 == 3)
            ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
    }

    if (a == 1)
        return ans; // (1/n) = 1

    while (a != 0)
    {
        if (a < 0)
        {
            a = -a; // (a/n) = (-a/n)*(-1/n)
            if (n % 4 == 3)
                ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
        }

        while (a % 2 == 0)
        {
            a /= 2;
            if (n % 8 == 3 || n % 8 == 5)
                ans = -ans;
        }

        long temp = a;
        a = n;
        n = temp;

        if (a % 4 == 3 && n % 4 == 3)
            ans = -ans;

        a %= n;
        if (a > n / 2)
            a = a - n;
    }

    if (n == 1)
        return ans;

    return 0;
}

// To perform the Solovay-Strassen Primality Test
static boolean solovoyStrassen(long p,
                               int iteration)
{
    if (p < 2)
        return false;
    if (p != 2 && p % 2 == 0)
        return false;

    // Create Object for Random Class
    Random rand = new Random();
    for(int i = 0; i < iteration; i++)
    {

        // Generate a random number r
        long r = Math.abs(rand.nextLong());           
        long a = r % (p - 1) + 1;
        long jacobian = (p + calculateJacobian(a, p)) % p;
        long mod = modulo(a, (p - 1) / 2, p);

        if (jacobian == 0 || mod != jacobian)
            return false;
    }
    return true;       
}

// Driver code
public static void main (String[] args)
{
    int iter = 50;
    long num1 = 15;
    long num2 = 13;

    if (solovoyStrassen(num1, iter))
        System.out.println(num1 + " is prime");
    else
        System.out.println(num1 + " is composite");   

     if (solovoyStrassen(num2,iter))
        System.out.println(num2 + " is prime");
    else
        System.out.println(num2 + " is composite");
}
}

// This code is contributed by Srishtik Dutta
```

## 蟒蛇 3

```
# Python3 program to implement Solovay-Strassen
# Primality Test
import random

# modulo function to perform binary
# exponentiation
def modulo(base, exponent, mod):
    x = 1;
    y = base;
    while (exponent > 0):
        if (exponent % 2 == 1):
            x = (x * y) % mod;

        y = (y * y) % mod;
        exponent = exponent // 2;

    return x % mod;

# To calculate Jacobian symbol of a
# given number
def calculateJacobian(a, n):

    if (a == 0):
        return 0;# (0/n) = 0

    ans = 1;
    if (a < 0):

        # (a/n) = (-a/n)*(-1/n)
        a = -a;
        if (n % 4 == 3):

            # (-1/n) = -1 if n = 3 (mod 4)
            ans = -ans;

    if (a == 1):
        return ans; # (1/n) = 1

    while (a):
        if (a < 0):

            # (a/n) = (-a/n)*(-1/n)
            a = -a;
            if (n % 4 == 3):

                # (-1/n) = -1 if n = 3 (mod 4)
                ans = -ans;

        while (a % 2 == 0):
            a = a // 2;
            if (n % 8 == 3 or n % 8 == 5):
                ans = -ans;

        # swap
        a, n = n, a;

        if (a % 4 == 3 and n % 4 == 3):
            ans = -ans;
        a = a % n;

        if (a > n // 2):
            a = a - n;

    if (n == 1):
        return ans;

    return 0;

# To perform the Solovay- Strassen
# Primality Test
def solovoyStrassen(p, iterations):

    if (p < 2):
        return False;
    if (p != 2 and p % 2 == 0):
        return False;

    for i in range(iterations):

        # Generate a random number a
        a = random.randrange(p - 1) + 1;
        jacobian = (p + calculateJacobian(a, p)) % p;
        mod = modulo(a, (p - 1) / 2, p);

        if (jacobian == 0 or mod != jacobian):
            return False;

    return True;

# Driver Code
iterations = 50;
num1 = 15;
num2 = 13;

if (solovoyStrassen(num1, iterations)):
    print(num1, "is prime ");
else:
    print(num1, "is composite");

if (solovoyStrassen(num2, iterations)):
    print(num2, "is prime");
else:
    print(num2, "is composite");

# This code is contributed by mits
```

## C#

```
/// C# program to implement Solovay-Strassen
// Primality Test
using System;
using System.Collections.Generic;  
class GFG {

    // Modulo function to perform
    // binary exponentiation
    static long modulo(long Base, long exponent, long mod)
    {
        long x = 1;
        long y = Base;

        while (exponent > 0)
        {
            if (exponent % 2 == 1)
                x = (x * y) % mod;

            y = (y * y) % mod;
            exponent = exponent / 2;

        }
        return x % mod;
    }

    // To calculate Jacobian symbol of
    // a given number
    static long calculateJacobian(long a, long n)
    {
        if (n <= 0 || n % 2 == 0)
            return 0;

        long ans = 1L;

        if (a < 0)
        {
            a = -a; // (a/n) = (-a/n)*(-1/n)
            if (n % 4 == 3)
                ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
        }

        if (a == 1)
            return ans; // (1/n) = 1

        while (a != 0)
        {
            if (a < 0)
            {
                a = -a; // (a/n) = (-a/n)*(-1/n)
                if (n % 4 == 3)
                    ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
            }

            while (a % 2 == 0)
            {
                a /= 2;
                if (n % 8 == 3 || n % 8 == 5)
                    ans = -ans;
            }

            long temp = a;
            a = n;
            n = temp;

            if (a % 4 == 3 && n % 4 == 3)
                ans = -ans;

            a %= n;
            if (a > n / 2)
                a = a - n;
        }

        if (n == 1)
            return ans;

        return 0;
    }

    // To perform the Solovay-Strassen Primality Test
    static bool solovoyStrassen(long p, int iteration)
    {
        if (p < 2)
            return false;
        if (p != 2 && p % 2 == 0)
            return false;

        // Create Object for Random Class
        Random rand = new Random();
        for(int i = 0; i < iteration; i++)
        {

            // Generate a random number r
            long r = Math.Abs(rand.Next());           
            long a = r % (p - 1) + 1;
            long jacobian = (p + calculateJacobian(a, p)) % p;
            long mod = modulo(a, (p - 1) / 2, p);

            if (jacobian == 0 || mod != jacobian)
                return false;
        }
        return true;       
    }

  // Driver code
  static void Main()
  {
        int iter = 50;
        long num1 = 15;
        long num2 = 13;

        if (solovoyStrassen(num1, iter))
            Console.WriteLine(num1 + " is prime");
        else
            Console.WriteLine(num1 + " is composite");   

         if (solovoyStrassen(num2,iter))
            Console.WriteLine(num2 + " is prime");
        else
            Console.WriteLine(num2 + " is composite");
  }
}

// This code is contributed by divyeshrabadiya07
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// Solovay-Strassen Primality Test

// modulo function to perform
// binary exponentiation
function modulo($base, $exponent, $mod)
{
    $x = 1;
    $y = $base;
    while ($exponent > 0)
    {
        if ($exponent % 2 == 1)
            $x = ($x * $y) % $mod;

        $y = ($y * $y) % $mod;
        $exponent = $exponent / 2;
    }

    return $x % $mod;
}

// To calculate Jacobian
// symbol of a given number
function calculateJacobian($a, $n)
{
    if (!$a)
        return 0;// (0/n) = 0

    $ans = 1;
    if ($a < 0)
    {
        // (a/n) = (-a/n)*(-1/n)
        $a = -$a;
        if ($n % 4 == 3)

            // (-1/n) = -1 if n = 3 (mod 4)
            $ans = -$ans;
    }

    if ($a == 1)
        return $ans;// (1/n) = 1

    while ($a)
    {
        if ($a < 0)
        {
            // (a/n) = (-a/n)*(-1/n)
            $a = -$a;
            if ($n % 4 == 3)

                // (-1/n) = -1 if n = 3 (mod 4)
                $ans = -$ans;
        }

        while ($a % 2 == 0)
        {
            $a = $a / 2;
            if ($n % 8 == 3 || $n % 8 == 5)
                $ans = -$ans;

        }
        //swap
        list($a, $n) = array($n, $a);

        if ($a % 4 == 3 && $n % 4 == 3)
            $ans = -$ans;
        $a = $a % $n;

        if ($a > $n / 2)
            $a = $a - $n;

    }

    if ($n == 1)
        return $ans;

    return 0;
}

// To perform the Solovay-
// Strassen Primality Test
function solovoyStrassen($p, $iterations)
{
    if ($p < 2)
        return false;
    if ($p != 2 && $p % 2 == 0)
        return false;

    for ($i = 0; $i < $iterations; $i++)
    {
        // Generate a random number a
        $a = rand() % ($p - 1) + 1;
        $jacobian = ($p +
                     calculateJacobian($a,
                                       $p)) % $p;
        $mod = modulo($a, ($p - 1) / 2, $p);

        if (!$jacobian || $mod != $jacobian)
            return false;
    }
    return true;
}

// Driver Code
$iterations = 50;
$num1 = 15;
$num2 = 13;

if (solovoyStrassen($num1, $iterations))
    echo $num1," is prime ","\n";
else
    echo $num1," is composite\n";

if (solovoyStrassen($num2, $iterations))
    echo $num2," is prime\n";
else
    echo $num2," is composite\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to implement Solovay-Strassen
// Primality Test

// Modulo function to perform
// binary exponentiation
function modulo( base, exponent,mod)
{
    let x = 1;
    let y = base;

    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            x = (x * y) % mod;

        y = (y * y) % mod;
        exponent = Math.floor(exponent / 2);

    }
    return x % mod;
}

// To calculate Jacobian symbol of
// a given number
function calculateJacobian( a, n)
{
    if (n <= 0 || n % 2 == 0)
        return 0;

    let ans = 1;

    if (a < 0)
    {
        a = -a; // (a/n) = (-a/n)*(-1/n)
        if (n % 4 == 3)
            ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
    }

    if (a == 1)
        return ans; // (1/n) = 1

    while (a != 0)
    {
        if (a < 0)
        {
            a = -a; // (a/n) = (-a/n)*(-1/n)
            if (n % 4 == 3)
                ans = -ans; // (-1/n) = -1 if n = 3 (mod 4)
        }

        while (a % 2 == 0)
        {
            a = Math.floor(a/2);
            if (n % 8 == 3 || n % 8 == 5)
                ans = -ans;
        }

        let temp= a;
        a = n;
        n = temp;

        if (a % 4 == 3 && n % 4 == 3)
            ans = -ans;

        a %= n;
        if (a > Math.floor(n / 2))
            a = a - n;
    }

    if (n == 1)
        return ans;

    return 0;
}

// To perform the Solovay-Strassen Primality Test
function solovoyStrassen( p, iteration)
{
    if (p < 2)
        return false;
    if (p != 2 && p % 2 == 0)
        return false;

    for(let i = 0; i < iteration; i++)
    {

        // Generate a random number r
        let r = Math.floor(Math.random()* (Number.MAX_VALUE, 2) );   
        let a = r % (p - 1) + 1;
        let jacobian = (p + calculateJacobian(a, p)) % p;
        let mod = modulo(a, Math.floor((p - 1) / 2), p);

        if (jacobian == 0 || mod != jacobian)
            return false;
    }
    return true;   
}

// Driver Code

let iter = 50;
let num1 = 15;
let num2 = 13;

if (solovoyStrassen(num1, iter))
    document.write(num1 + " is prime"+ "</br>");
else
    document.write(num1 + " is composite" + "</br>");

if (solovoyStrassen(num2,iter))
    document.write(num2 + " is prime"+ "</br>");
else
    document.write(num2 + " is composite"+ "</br>");

</script>
```

**输出:**

```
15 is composite
13 is prime
```

**运行时间:**使用快速算法进行模幂运算，该算法的运行时间为 O(k ![log^3 ](img/84e7d0bf1e6db6ee002b87f17b6e7424.png "Rendered by QuickLaTeX.com") n)，其中 k 是我们测试的不同值的个数。

**准确率:**算法有可能返回不正确的答案。如果输入 n 确实是质数，那么输出可能总是正确的质数。然而，如果输入 n 是复合的，那么输出可能是不正确的素数。然后，数字 n 被称为欧拉-雅可比伪素数。

本文由 [Palash Nigam](https://www.linkedin.com/in/palash25) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。