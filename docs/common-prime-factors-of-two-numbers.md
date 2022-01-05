# 两个数的公共质因数

> 原文:[https://www . geesforgeks . org/common-prime-factors-of-two-numbers/](https://www.geeksforgeeks.org/common-prime-factors-of-two-numbers/)

给定两个整数![A   ](img/7456c3bc5a86a019fcdcf0ba5362b608.png "Rendered by QuickLaTeX.com")和![B   ](img/9baf1a3ec2b5758d598d7afc0f892827.png "Rendered by QuickLaTeX.com")，任务是找出这些数的公共质因数。
**例:**

> **输入:** A = 6，B = 12
> **输出:** 2 3
> 2 和 3 是 6 和 12
> **的唯一公共质因数输入:** A = 4，B = 8
> **输出:** 2

**天真方法:** [从 **1** 迭代](https://www.geeksforgeeks.org/loops-in-c/)到 **min(A，B)** 并检查 **i** 是否为素数以及 **A** 和 **B** 的因子，如果是则显示数字。
**高效方法**是做以下几点:

1.  求给定数的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (gcd)。
2.  [找到 GCD 的质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

**多查询的高效方法:**如果对公共因子有多个查询，则可以进一步优化上述解决方案。这个想法是基于[质因数分解，对多个查询使用 0(对数 n)筛](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN   100001

bool prime[MAXN];
void SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.

    memset(prime, true, sizeof(prime));

    // 0 and 1 are not prime numbers
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= MAXN; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p as non-prime
            for (int i = p * p; i <= MAXN; i += p)
                prime[i] = false;
        }
    }
}

// Find the common prime divisors
void common_prime(int a, int b)
{

    // Get the GCD of the given numbers
    int gcd = __gcd(a, b);

    // Find the prime divisors of the gcd
    for (int i = 2; i <= (gcd); i++) {

        // If i is prime and a divisor of gcd
        if (prime[i] && gcd % i == 0) {
            cout << i << " ";
        }
    }
}

// Driver code
int main()
{
    // Create the Sieve
    SieveOfEratosthenes();

    int a = 6, b = 12;

    common_prime(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach

class GFG {

static final int MAXN = 100001;
static boolean prime[] = new boolean[MAXN];

static void SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.

        for(int i = 0;i<prime.length;i++)
            prime[i]=true;

    // 0 and 1 are not prime numbers
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p < MAXN; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p as non-prime
            for (int i = p * p; i < MAXN; i += p)
                prime[i] = false;
        }
    }
}

// Find the common prime divisors
static void common_prime(int a, int b)
{

    // Get the GCD of the given numbers
    int gcd = (int) __gcd(a, b);

    // Find the prime divisors of the gcd
    for (int i = 2; i <= (gcd); i++) {

        // If i is prime and a divisor of gcd
        if (prime[i] && gcd % i == 0) {
            System.out.print(i + " ");
        }
    }
}
static long __gcd(long a, long b) 
{ 
    if (a == 0) 
        return b; 
    return __gcd(b % a, a); 
}
// Driver code
    public static void main(String[] args) {
        // Create the Sieve
    SieveOfEratosthenes();

    int a = 6, b = 12;

    common_prime(a, b);
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python implementation of above approach
from math import gcd, sqrt

# Create a boolean array "prime[0..n]"
# and initialize all entries it as true.
# A value in prime[i] will finally be
# false if i is Not a prime, else true.
prime = [True] * 100001

def SieveOfEratosthenes() :

    # 0 and 1 are not prime numbers
    prime[0] = False
    prime[1] = False

    for p in range(2, int(sqrt(100001)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True :

            # Update all multiples of
            # p as non-prime
            for i in range(p**2, 100001, p) :
                prime[i] = False

# Find the common prime divisors
def common_prime(a, b) :

    # Get the GCD of the given numbers
    __gcd = gcd(a, b)

    # Find the prime divisors of the gcd
    for i in range(2, __gcd + 1) :

        # If i is prime and a divisor of gcd
        if prime[i] and __gcd % i == 0 :
            print(i, end = " ")

# Driver code
if __name__ == "__main__" :

    # Create the Sieve
    SieveOfEratosthenes()
    a, b = 6, 12

    common_prime(a, b)

# This code is contributed by ANKITRAI1
```

## C#

```
//C# implementation of above approach
using System;
public class GFG {

    static bool []prime = new bool[100001];
    static void SieveOfEratosthenes()
    {

        // Create a boolean array "prime[0..n]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.

            for(int i = 0;i<prime.Length;i++)
                prime[i]=true;

        // 0 and 1 are not prime numbers
        prime[0] = false;
        prime[1] = false;

        for (int p = 2; p * p < 100001; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p as non-prime
                for (int i = p * p; i < 100001; i += p)
                    prime[i] = false;
            }
        }
    }

    // Find the common prime divisors
    static void common_prime(int a, int b)
    {

        // Get the GCD of the given numbers
        int gcd = (int) __gcd(a, b);

        // Find the prime divisors of the gcd
        for (int i = 2; i <= (gcd); i++) {

            // If i is prime and a divisor of gcd
            if (prime[i] && gcd % i == 0) {
                Console.Write(i + " ");
            }
        }
    }
    static long __gcd(long a, long b) 
    { 
        if (a == 0) 
            return b; 
        return __gcd(b % a, a); 
    }
    // Driver code
    public static void Main() {
        // Create the Sieve
    SieveOfEratosthenes();

    int a = 6, b = 12;

    common_prime(a, b);
    }
}

/*This code is contributed by 29AjayKumar*/
```

## java 描述语言

```
<script>
// Javascript program to implement the above approach

MAXN = parseInt(100001);
prime = new Array(MAXN);

function __gcd(a, b) 
{ 
    if (a == 0) 
        return b; 
    return __gcd(b % a, a); 
}
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.

    prime.fill(true);

    // 0 and 1 are not prime numbers
    prime[0] = false;
    prime[1] = false;

    for (var p = 2; p * p <= MAXN; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p as non-prime
            for (var i = p * p; i <= MAXN; i += p)
                prime[i] = false;
        }
    }
}

// Find the common prime divisors
function common_prime( a, b)
{

    // Get the GCD of the given numbers
    var gcd = __gcd(a, b);

    // Find the prime divisors of the gcd
    for (var i = 2; i <= (gcd); i++) {

        // If i is prime and a divisor of gcd
        if (prime[i] && gcd % i == 0) {
            document.write( i + " ");
       }
    }
}

SieveOfEratosthenes();
var a = 6, b = 12;
common_prime(a, b);

//This code is contributed by SoumikModnal
</script>
```

**Output:** 

```
2 3
```