# n 的因子数！

> 原文:[https://www.geeksforgeeks.org/no-factors-n/](https://www.geeksforgeeks.org/no-factors-n/)

给定一个正整数 n，求 n 中的因子个数！其中 n <= 10 <sup>5</sup> 。
**例:**

```
Input : n = 3
Output : 4
Factors of 3! are 1, 2, 3, 6

Input : n = 4
Output : 8
Factors of 4! are 1, 2, 3, 4, 
                 6, 8, 12, 24

Input : n = 16
Output : 5376
```

请注意，暴力方法在这里甚至不起作用，因为我们找不到 n！对于如此大的 n .我们需要一个更现实的方法来解决这个问题。

这个想法是基于[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。
任何正整数都可以表示为其素因子的幂的乘积。假设一个数 n = p<sub>1</sub>T5】a1x p<sub>2</sub>T9】a2x p<sub>3</sub>T13】a3，…。，p <sub>k</sub> <sup>ak</sup> 其中 p <sub>1</sub> ，p <sub>2</sub> ，p <sub>3</sub> ，…。，p <sub>k</sub> 是不同的素数和 a1，a2，a3，……..，ak 是它们各自的指数。
那么 n 的除数=(a1+1)x(a2+1)x(a3+1)…x(AK+1)
这样，n 的因子数！现在可以很容易地通过首先找到素因子直到 n，然后计算它们各自的指数来计算。
我们算法的主要步骤是:

1.  从 p = 1 迭代到 p = n，每次迭代时检查 p 是否为素数。
2.  如果 p 是质数，那么意味着它是 n 的质因数！所以我们在 n 中找到了 p 的指数！哪个是
3.  找到所有质因数的各自指数后，假设它们是 a1，a2，a3，…，ak 那么 n 的因子！=(a1+1)x(a2+1)x(a3+1)………………(AK+1)

```
Here is an illustration on how the algorithm works 
for finding factors of 16!:

All prime less than 16 will be the prime factors of 16!. 
so instead of finding all the prime factor of 16!.
we just need to find the primes less than 16 that will 
automatically be the prime factors of 16!

Prime factors of 16! are: 2,3,5,7,11,13

Now to the exponent of 2 in 16!  
              = ⌊16/2⌋+ ⌊16/4⌋+ ⌊16/8⌋ + ⌊16/16⌋ 
              = 8 + 4 + 2 + 1
              = 15

Similarly, 
   exponent of 3 in 16! =  ⌊16/3⌋ + ⌊16/9⌋ = 6
   exponent of 5 in 16! = 3 
   exponent of 7 in 16! = 2
   exponent of 11 in 16! = 1
   exponent of 13 in 16! = 1

So, the no of factors of 16! 
         = (15+1) * (6+1) * (3+1) *(2+1)* (1+1) * (1+1)
         = 5376 
```

以下是上述思路的实现:

## C++

```
// C++ program to count number of factors of n
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Sieve of Eratosthenes to mark all prime number
// in array prime as 1
void sieve(int n, bool prime[])
{
    // Initialize all numbers as prime
    for (int i=1; i<=n; i++)
        prime[i] = 1;

    // Mark composites
    prime[1] = 0;
    for (int i=2; i*i<=n; i++)
    {
        if (prime[i])
        {
            for (int j=i*i; j<=n; j += i)
                prime[j] = 0;
        }
    }
}

// Returns the highest exponent of p in n!
int expFactor(int n, int p)
{
    int x = p;
    int exponent = 0;
    while ((n/x) > 0)
    {
        exponent += n/x;
        x *= p;
    }
    return exponent;
}

// Returns the no of factors in n!
ll countFactors(int n)
{
    // ans stores the no of factors in n!
    ll ans = 1;

    // Find all primes upto n
    bool prime[n+1];
    sieve(n, prime);

    // Multiply exponent (of primes) added with 1
    for (int p=1; p<=n; p++)
    {
        // if p is a prime then p is also a
        // prime factor of n!
        if (prime[p]==1)
            ans *= (expFactor(n, p) + 1);
    }

    return ans;
}

// Driver code
int main()
{
    int n = 16;
    printf("Count of factors of %d! is %lld\n",
                                n, countFactors(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of factors of n
import java.io.*;
class GFG {

    // Sieve of Eratosthenes to mark all prime number
    // in array prime as 1
    static void sieve(int n, int prime[])
    {
        // Initialize all numbers as prime
        for (int i = 1; i <= n; i++)
            prime[i] = 1;

        // Mark composites
        prime[1] = 0;
        for (int i = 2; i * i <= n; i++) {
            if (prime[i] == 1) {
                for (int j = i * i; j <= n; j += i)
                    prime[j] = 0;
            }
        }
    }

    // Returns the highest exponent of p in n!
    static int expFactor(int n, int p)
    {
        int x = p;
        int exponent = 0;
        while ((n / x) > 0) {
            exponent += n / x;
            x *= p;
        }
        return exponent;
    }

    // Returns the no of factors in n!
    static long countFactors(int n)
    {
        // ans stores the no of factors in n!
        long ans = 1;

        // Find all primes upto n
        int prime[] = new int[n + 1];
        sieve(n, prime);

        // Multiply exponent (of primes) added with 1
        for (int p = 1; p <= n; p++) {

            // if p is a prime then p is also a
            // prime factor of n!
            if (prime[p] == 1)
                ans *= (expFactor(n, p) + 1);
        }

        return ans;
    }

    // Driver code
     public static void main(String args[])
    {
        int n = 16;
        System.out.println("Count of factors of " +
                       n + " is " + countFactors(n));
    }
}
// This code is contributed by Nikita Tiwari
```

## 蟒蛇 3

```
# python 3 program to count
# number of factors of n

# Returns the highest
# exponent of p in n!
def expFactor(n, p):
    x = p
    exponent = 0
    while n // x > 0:

        exponent += n // x
        x *= p
    return exponent

# Returns the no
# of factors in n!
def countFactors(n):

    # ans stores the no
    # of factors in n!
    ans = 1

    # Find all primes upto n
    prime = [None]*(n+1)

    # Initialize all
    # numbers as prime
    for i in range(1,n+1):
        prime[i] = 1

    # Mark composites
    prime[1] = 0
    i = 2
    while i * i <= n:

        if (prime[i]):

            for j in range(i * i,n+1,i):
                prime[j] = 0
        i += 1

    # Multiply exponent (of
    # primes) added with 1
    for p in range(1,n+1):

        # if p is a prime then p
        # is also a prime factor of n!
        if (prime[p] == 1):
            ans *= (expFactor(n, p) + 1)

    return ans

# Driver Code
if __name__=='__main__':
    n = 16
    print("Count of factors of " + str(n) +
         "! is " +str( countFactors(n)))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to count number
// of factors of n
using System;

class GFG {

    // Sieve of Eratosthenes to mark all
    // prime number in array prime as 1
    static void sieve(int n, int []prime)
    {

        // Initialize all numbers as prime
        for (int i = 1; i <= n; i++)
            prime[i] = 1;

        // Mark composites
        prime[1] = 0;
        for (int i = 2; i * i <= n; i++)
        {
            if (prime[i] == 1)
            {
                for (int j = i * i; j <= n; j += i)
                    prime[j] = 0;
            }
        }
    }

    // Returns the highest exponent of p in n!
    static int expFactor(int n, int p)
    {
        int x = p;
        int exponent = 0;
        while ((n / x) > 0)
        {
            exponent += n / x;
            x *= p;
        }
        return exponent;
    }

    // Returns the no of factors in n!
    static long countFactors(int n)
    {
        // ans stores the no of factors in n!
        long ans = 1;

        // Find all primes upto n
        int []prime = new int[n + 1];
        sieve(n, prime);

        // Multiply exponent (of primes)
        // added with 1
        for (int p = 1; p <= n; p++)
        {

            // if p is a prime then p is
            // also a prime factor of n!
            if (prime[p] == 1)
                ans *= (expFactor(n, p) + 1);
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 16;
        Console.Write("Count of factors of " +
                       n + " is " + countFactors(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of factors of n

// Returns the highest
// exponent of p in n!
function expFactor($n, $p)
{
    $x = $p;
    $exponent = 0;
    while (intval($n / $x) > 0)
    {
        $exponent += intval($n / $x);
        $x *= $p;
    }
    return $exponent;
}

// Returns the no
// of factors in n!
function countFactors($n)
{
    // ans stores the no
    // of factors in n!
    $ans = 1;

    // Find all primes upto n
    $prime = array();

    // Initialize all
    // numbers as prime
    for ($i = 1; $i <= $n; $i++)
        $prime[$i] = 1;

    // Mark composites
    $prime[1] = 0;
    for ($i = 2; $i * $i <= $n; $i++)
    {
        if ($prime[$i])
        {
            for ($j = $i * $i; $j <= $n; $j += $i)
                $prime[$j] = 0;
        }
    }

    // Multiply exponent (of
    // primes) added with 1
    for ($p = 1; $p <= $n; $p++)
    {
        // if p is a prime then p
        // is also a prime factor of n!
        if ($prime[$p] == 1)
            $ans *= intval(expFactor($n, $p) + 1);
    }

    return $ans;
}

// Driver Code
$n = 16;
echo "Count of factors of " . $n .
       "! is " . countFactors($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript program to count number of factors of n   

    // Sieve of Eratosthenes to mark all prime number
    // in array prime as 1
    function sieve(n, prime)
    {

        // Initialize all numbers as prime
        for (let i = 1; i <= n; i++)
            prime[i] = 1;

        // Mark composites
        prime[1] = 0;
        for (let i = 2; i * i <= n; i++)
        {
            if (prime[i] == 1)
            {
                for (let j = i * i; j <= n; j += i)
                    prime[j] = 0;
            }
        }
    }

    // Returns the highest exponent of p in n!
    function expFactor(n,p)
    {
        let x = p;
        let exponent = 0;
        while ((n / x) > 0)
        {
            exponent += Math.floor(n / x);
            x *= p;
        }
        return exponent;
    }

    // Returns the no of factors in n!
    function countFactors(n)
    {

        // ans stores the no of factors in n!
        let ans = 1;

        // Find all primes upto n
        let prime = new Array(n + 1);
        for(let i = 0; i < n + 1; i++)
        {
            prime[i] = 0;
        }
        sieve(n, prime);

        // Multiply exponent (of primes) added with 1
        for (let p = 1; p <= n; p++)
        {

            // if p is a prime then p is also a
            // prime factor of n!
            if (prime[p] == 1)
                ans *= (expFactor(n, p) + 1);
        }

        return ans;
    }

     // Driver code
    let n = 16;
    document.write("Count of factors of " +
                       n + "! is " + countFactors(n));

    //  This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Count of factors of 16! is 5376 
```

**注意:**如果任务是对多个输入值的因子进行计数，那么我们可以预计算所有素数，最多不超过最大限制 10 <sup>5</sup> 。
本文由**马达尔·莫迪**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。