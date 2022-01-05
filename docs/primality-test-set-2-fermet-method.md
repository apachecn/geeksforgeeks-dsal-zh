# 素性检验|集合 2(费马方法)

> 原文:[https://www . geesforgeks . org/primate-test-set-2-fermet-method/](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)

给定一个数字 n，检查它是否是质数。我们已经在集合 1 中介绍并讨论了素性检验的学校方法。
[素性测验|第 1 集(引论与学校方法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)
本文讨论费马的方法。该方法是一种概率方法，基于费马小定理。

```
**Fermat's Little Theorem:**
If n is a prime number, then for every a, 1 < a < n-1,

a<sup>n-1 ≡ 1 (mod n)</sup>
 <sup>OR</sup> 
a<sup>n-1</sup> % n = 1 

Example: Since 5 is prime, 24 ≡ 1 (mod 5) [or 24%5 = 1],
         34 ≡ 1 (mod 5) and 44 ≡ 1 (mod 5) 

         Since 7 is prime, 26 ≡ 1 (mod 7),
         36 ≡ 1 (mod 7), 46 ≡ 1 (mod 7) 
         56 ≡ 1 (mod 7) and 66 ≡ 1 (mod 7) 

Refer this for different proofs.
```

如果给定的数字是质数，那么这个方法总是返回真。如果给定的数字是复合的(或非质数)，那么它可能返回真或假，但是为复合产生不正确结果的概率很低，并且可以通过做更多的迭代来降低。

下面是算法:

```
// Higher value of k indicates probability of correct
// results for composite inputs become higher. For prime
// inputs, result is always correct
1)  Repeat following k times:
      a) Pick a randomly in the range [2, n - 2]
      b) If gcd(a, n) ≠ 1, then return false
      c) If an-1 &nequiv; 1 (mod n), then return false
2) Return true [probably prime].
```

下面是上述算法的实现。代码使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)的幂函数

## C++

```
// C++ program to find the smallest twin in given range
#include <bits/stdc++.h>
using namespace std;

/* Iterative Function to calculate (a^n)%p in O(logy) */
int power(int a, unsigned int n, int p)
{
    int res = 1;      // Initialize result
    a = a % p;  // Update 'a' if 'a' >= p

    while (n > 0)
    {
        // If n is odd, multiply 'a' with result
        if (n & 1)
            res = (res*a) % p;

        // n must be even now
        n = n>>1; // n = n/2
        a = (a*a) % p;
    }
    return res;
}

/*Recursive function to calculate gcd of 2 numbers*/
int gcd(int a, int b)
{
    if(a < b)
        return gcd(b, a);
    else if(a%b == 0)
        return b;
    else return gcd(b, a%b); 
}

// If n is prime, then always returns true, If n is
// composite than returns false with high probability
// Higher value of k increases probability of correct
// result.
bool isPrime(unsigned int n, int k)
{
   // Corner cases
   if (n <= 1 || n == 4)  return false;
   if (n <= 3) return true;

   // Try k times
   while (k>0)
   {
       // Pick a random number in [2..n-2]       
       // Above corner cases make sure that n > 4
       int a = 2 + rand()%(n-4); 

       // Checking if a and n are co-prime
       if (gcd(n, a) != 1)
          return false;

       // Fermat's little theorem
       if (power(a, n-1, n) != 1)
          return false;

       k--;
    }

    return true;
}

// Driver Program to test above function
int main()
{
    int k = 3;
    isPrime(11, k)?  cout << " true\n": cout << " false\n";
    isPrime(15, k)?  cout << " true\n": cout << " false\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// smallest twin in given range

import java.io.*;
import java.math.*;

class GFG {

    /* Iterative Function to calculate
    // (a^n)%p in O(logy) */
    static int power(int a,int n, int p)
    {
        // Initialize result
        int res = 1;

        // Update 'a' if 'a' >= p
        a = a % p;

        while (n > 0)
        {
            // If n is odd, multiply 'a' with result
            if ((n & 1) == 1)
                res = (res * a) % p;

            // n must be even now
            n = n >> 1; // n = n/2
            a = (a * a) % p;
        }
        return res;
    }

    // If n is prime, then always returns true,
    // If n is composite than returns false with
    // high probability Higher value of k increases
    //  probability of correct result.
    static boolean isPrime(int n, int k)
    {
    // Corner cases
    if (n <= 1 || n == 4) return false;
    if (n <= 3) return true;

    // Try k times
    while (k > 0)
    {
        // Pick a random number in [2..n-2]    
        // Above corner cases make sure that n > 4
        int a = 2 + (int)(Math.random() % (n - 4));

        // Fermat's little theorem
        if (power(a, n - 1, n) != 1)
            return false;

        k--;
        }

        return true;
    }

    // Driver Program
    public static void main(String args[])
    {
        int k = 3;
        if(isPrime(11, k))
            System.out.println(" true");
        else
            System.out.println(" false");
        if(isPrime(15, k))
            System.out.println(" true");
        else
            System.out.println(" false");

    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# twin in given range
import random

# Iterative Function to calculate
# (a^n)%p in O(logy)
def power(a, n, p):

    # Initialize result
    res = 1

    # Update 'a' if 'a' >= p
    a = a % p 

    while n > 0:

        # If n is odd, multiply
        # 'a' with result
        if n % 2:
            res = (res * a) % p
            n = n - 1
        else:
            a = (a ** 2) % p

            # n must be even now
            n = n // 2

    return res % p

# If n is prime, then always returns true,
# If n is composite than returns false with
# high probability Higher value of k increases
# probability of correct result
def isPrime(n, k):

    # Corner cases
    if n == 1 or n == 4:
        return False
    elif n == 2 or n == 3:
        return True

    # Try k times
    else:
        for i in range(k):

            # Pick a random number
            # in [2..n-2]     
            # Above corner cases make
            # sure that n > 4
            a = random.randint(2, n - 2)

            # Fermat's little theorem
            if power(a, n - 1, n) != 1:
                return False

    return True

# Driver code
k = 3
if isPrime(11, k):
  print("true")
else:
  print("false")

if isPrime(15, k):
  print("true")
else:
  print("false")

# This code is contributed by Aanchal Tiwari
```

## C#

```
// C# program to find the
// smallest twin in given range
using System;
class GFG {

    /* Iterative Function to calculate
    // (a^n)%p in O(logy) */
    static int power(int a,int n, int p)
    {
        // Initialize result
        int res = 1;

        // Update 'a' if 'a' >= p
        a = a % p;

        while (n > 0)
        {
            // If n is odd, multiply 'a' with result
            if ((n & 1) == 1)
                res = (res * a) % p;

            // n must be even now
            n = n >> 1; // n = n/2
            a = (a * a) % p;
        }
        return res;
    }

    // If n is prime, then always returns true,
    // If n is composite than returns false with
    // high probability Higher value of k increases
    //  probability of correct result.
    static bool isPrime(int n, int k)
    {
        // Corner cases
        if (n <= 1 || n == 4) return false;
        if (n <= 3) return true;

        // Try k times
        while (k > 0)
        {
            // Pick a random number in [2..n-2]    
            // Above corner cases make sure that n > 4
            Random rand = new Random();
            int a = 2 + (int)(rand.Next() % (n - 4));

            // Fermat's little theorem
            if (power(a, n - 1, n) != 1)
                return false;

            k--;
        }

        return true;
    }

  static void Main() {
        int k = 3;
        if(isPrime(11, k))
            Console.WriteLine(" true");
        else
            Console.WriteLine(" false");
        if(isPrime(15, k))
            Console.WriteLine(" true");
        else
            Console.WriteLine(" false");
  }
}

// This code is contributed by divyesh072019
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// smallest twin in given range

// Iterative Function to calculate
// (a^n)%p in O(logy)
function power($a, $n, $p)
{

    // Initialize result
    $res = 1;

    // Update 'a' if 'a' >= p
    $a = $a % $p;

    while ($n > 0)
    {

        // If n is odd, multiply
        // 'a' with result
        if ($n & 1)
            $res = ($res * $a) % $p;

        // n must be even now
        $n = $n >> 1; // n = n/2
        $a = ($a * $a) % $p;
    }
    return $res;
}

// If n is prime, then always
// returns true, If n is
// composite than returns
// false with high probability
// Higher value of k increases
// probability of correct
// result.
function isPrime($n, $k)
{

    // Corner cases
    if ($n <= 1 || $n == 4)
    return false;
    if ($n <= 3)
    return true;

    // Try k times
    while ($k > 0)
    {

        // Pick a random number
        // in [2..n-2]
        // Above corner cases
        // make sure that n > 4
        $a = 2 + rand() % ($n - 4);

        // Fermat's little theorem
        if (power($a, $n-1, $n) != 1)
            return false;

        $k--;
    }

    return true;
}

// Driver Code
$k = 3;
$res = isPrime(11, $k) ? " true\n": " false\n";
echo($res);

$res = isPrime(15, $k) ? " true\n": " false\n";
echo($res);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// smallest twin in given range

/* Iterative Function to calculate
// (a^n)%p in O(logy) */
function power( a, n, p)
{
    // Initialize result
    let res = 1;

    // Update 'a' if 'a' >= p
    a = a % p;

    while (n > 0)
    {
        // If n is odd, multiply 'a' with result
        if ((n & 1) == 1)
            res = (res * a) % p;

        // n must be even now
        n = n >> 1; // n = n/2
        a = (a * a) % p;
    }
    return res;
}

// If n is prime, then always returns true,
// If n is composite than returns false with
// high probability Higher value of k increases
// probability of correct result.
function isPrime( n, k)
{
// Corner cases
if (n <= 1 || n == 4) return false;
if (n <= 3) return true;

// Try k times
while (k > 0)
{
    // Pick a random number in [2..n-2]   
    // Above corner cases make sure that n > 4
    let a = Math.floor(Math.random()* (n-1 - 2) + 2);

    // Fermat's little theorem
    if (power(a, n - 1, n) != 1)
        return false;

    k--;
    }

    return true;
}

// Driver Code

let k = 3;
if(isPrime(11, k))
    document.write(" true" + "</br>");
else
    document.write(" false"+ "</br>");
if(isPrime(15, k))
    document.write(" true"+ "</br>");
else
    document.write(" false"+ "</br>");

</script>
```

**输出:**

```
true
false
```

这个解决方案的时间复杂度是 O(k Log n)。请注意，幂函数需要 0(对数 n)时间。
注意，即使我们增加迭代次数(更高的 k)，上述方法也可能失败。存在一些复合数，其性质是每一个 a < n，gcd(a，n) = 1 和 **a <sup>n-1</sup> ≡ 1 (mod n)** 。这样的数字被称为[卡迈克尔数字](https://en.wikipedia.org/wiki/Carmichael_number)。如果需要快速方法进行过滤，例如在 RSA 公钥密码算法的密钥生成阶段，通常会使用费马的素性测试。

我们将很快讨论更多的素性测试方法。

**参考文献:**
[【https://en.wikipedia.org/wiki/Fermat_primality_test】](https://en.wikipedia.org/wiki/Fermat_primality_test)
[https://en.wikipedia.org/wiki/Prime_number](https://en.wikipedia.org/wiki/Prime_number)
[http://www . CSE . iitk . AC . in/users/manindra/presentations/fltbasedtests . pdf](http://www.cse.iitk.ac.in/users/manindra/presentations/FLTBasedTests.pdf)
[https://en.wikipedia.org/wiki/Primality_test](https://en.wikipedia.org/wiki/Primality_test)
本文由 **Ajay** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息