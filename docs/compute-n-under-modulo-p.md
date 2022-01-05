# 计算 n！在模 p 下

> 原文:[https://www.geeksforgeeks.org/compute-n-under-modulo-p/](https://www.geeksforgeeks.org/compute-n-under-modulo-p/)

给定一个大数 n 和一个素数 p，如何高效计算 n！% p？
**例:**

```
Input:  n = 5, p = 13
Output: 3
5! = 120 and 120 % 13 = 3

Input:  n = 6, p = 11
Output: 5
6! = 720 and 720 % 11 = 5
```

一个**天真的解决方案**是先计算 n！，然后计算 n！% p .当值为 n！很小。n 的值！当 n！无法放入变量，并导致溢出。所以计算 n！然后使用模块化运算符并不是一个好主意，因为即使 n 和 r 的值稍微大一点也会有溢出现象。
下面是不同的方法。
**方法 1(简单)**
一个简单的解决方案是在模 p 下用 I 将结果一一相乘，这样在下一次迭代之前，结果的值不会超过 p。

## C++

```
// Simple method to compute n! % p
#include <bits/stdc++.h>
using namespace std;

// Returns value of n! % p
int modFact(int n, int p)
{
    if (n >= p)
        return 0;

    int result = 1;
    for (int i = 1; i <= n; i++)
        result = (result * i) % p;

    return result;
}

// Driver program
int main()
{
    int n = 25, p = 29;
    cout << modFact(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple method to compute n! % p
import java.io.*;

class GFG
{
    // Returns value of n! % p
    static int modFact(int n,
                       int p)
    {
        if (n >= p)
            return 0;

        int result = 1;
        for (int i = 1; i <= n; i++)
            result = (result * i) % p;

        return result;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 25, p = 29;
        System.out.print(modFact(n, p));
    }
}

// This code is contributed
// by aj_36
```

## 蟒蛇 3

```
# Simple method to compute n ! % p

# Returns value of n ! % p
def modFact(n, p):
    if n >= p:
        return 0   

    result = 1
    for i in range(1, n + 1):
        result = (result * i) % p

    return result

# Driver Code
n = 25; p = 29
print (modFact(n, p))

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// Simple method to compute n! % p
using System;

class GFG {

    // Returns value of n! % p
    static int modFact(int n, int p)
    {
        if (n >= p)
            return 0;

        int result = 1;
        for (int i = 1; i <= n; i++)
            result = (result * i) % p;

        return result;
    }

    // Driver program
    static void Main()
    {
        int n = 25, p = 29;
        Console.Write(modFact(n, p));
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Simple method to compute n! % p

// Returns value of n! % p
function modFact($n, $p)
{
    if ($n >= $p)
    return 0;

    $result = 1;
    for ($i = 1; $i <= $n; $i++)
        $result = ($result * $i) % $p;

    return $result;
}

// Driver Code
$n = 25; $p = 29;
echo modFact($n, $p);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Simple method to compute n! % p

    // Returns value of n! % p
     function modFact(n,p)
    {
        if (n >= p)
            return 0;

        let result = 1;
        for (let i = 1; i <= n; i++)
            result = (result * i) % p;

        return result;
    }

    // Driver Code

        let n = 25, p = 29;
        document.write(modFact(n, p));

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
5
```

该解决方案的时间复杂度为 0(n)。
**方法 2(使用筛子)**
这个想法是基于下面讨论的公式[这里](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。

```
The largest possible power of a prime pi that divides n is,
    ⌊n/pi⌋ + ⌊n/(pi2)⌋ +  ⌊n/(pi3)⌋ + .....+ 0 

Every integer can be written as multiplication of powers of primes.  So,
  n! = p1k<sup>1</sup> * p2k<sup>2</sup> * p3k<sup>3</sup> * ....
  Where p1, p2, p3, .. are primes and 
        k1, k2, k3, .. are integers greater than or equal to 1.
```

这个想法是使用厄拉多塞的[筛寻找所有小于 n 的素数。对于每一个质数 p <sub>i</sub> ，找到它最大的除 n 次方！。让最大的力量成为 k <sub>i</sub> 。使用](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[模幂运算](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)计算 p<sub>I</sub>k<sub>I</sub>% p。将其与模 p 下的最终结果相乘
下面是上述思想的实现。

## C++

```
// C++ program to Returns n % p
// using Sieve of Eratosthenes
#include <bits/stdc++.h>
using namespace std;

// Returns largest power of p that divides n!
int largestPower(int n, int p)
{
    // Initialize result
    int x = 0;

    // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while (n) {
        n /= p;
        x += n;
    }
    return x;
}

// Utility function to do modular exponentiation.
// It returns (x^y) % p
int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p
    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns n! % p
int modFact(int n, int p)
{
    if (n >= p)
        return 0;

    int res = 1;

    // Use Sieve of Eratosthenes to find all primes
    // smaller than n
    bool isPrime[n + 1];
    memset(isPrime, 1, sizeof(isPrime));
    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for (int j = 2 * i; j <= n; j += i)
                isPrime[j] = 0;
        }
    }

    // Consider all primes found by Sieve
    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) {
            // Find the largest power of prime 'i' that divides n
            int k = largestPower(n, i);

            // Multiply result with (i^k) % p
            res = (res * power(i, k, p)) % p;
        }
    }
    return res;
}

// Driver method
int main()
{
    int n = 25, p = 29;
    cout << modFact(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program Returns n % p using Sieve of Eratosthenes
public class GFG {

// Returns largest power of p that divides n!
    static int largestPower(int n, int p) {
        // Initialize result
        int x = 0;

        // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
        while (n > 0) {
            n /= p;
            x += n;
        }
        return x;
    }

// Utility function to do modular exponentiation.
// It returns (x^y) % p
    static int power(int x, int y, int p) {
        int res = 1; // Initialize result
        x = x % p; // Update x if it is more than or
        // equal to p
        while (y > 0) {
            // If y is odd, multiply x with result
            if (y % 2 == 1) {
                res = (res * x) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

// Returns n! % p
    static int modFact(int n, int p) {
        if (n >= p) {
            return 0;
        }

        int res = 1;

        // Use Sieve of Eratosthenes to find all primes
        // smaller than n
        boolean isPrime[] = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        for (int i = 2; i * i <= n; i++) {
            if (isPrime[i]) {
                for (int j = 2 * i; j <= n; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Consider all primes found by Sieve
        for (int i = 2; i <= n; i++) {
            if (isPrime[i]) {
                // Find the largest power of prime 'i' that divides n
                int k = largestPower(n, i);

                // Multiply result with (i^k) % p
                res = (res * power(i, k, p)) % p;
            }
        }
        return res;
    }

// Driver method
    static public void main(String[] args) {
        int n = 25, p = 29;
        System.out.println(modFact(n, p));

    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to Returns n % p
# using Sieve of Eratosthenes

# Returns largest power of p that divides n!
def largestPower(n, p):

    # Initialize result
    x = 0

    # Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while (n):
        n //= p
        x += n
    return x

# Utility function to do modular exponentiation.
# It returns (x^y) % p
def power( x, y, p):
    res = 1 # Initialize result
    x = x % p # Update x if it is more than
              # or equal to p
    while (y > 0) :

        # If y is odd, multiply x with result
        if (y & 1) :
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Returns n! % p
def modFact( n, p) :

    if (n >= p) :
        return 0

    res = 1

    # Use Sieve of Eratosthenes to find
    # all primes smaller than n
    isPrime = [1] * (n + 1)
    i = 2
    while(i * i <= n):
        if (isPrime[i]):
            for j in range(2 * i, n, i) :
                isPrime[j] = 0
        i += 1

    # Consider all primes found by Sieve
    for i in range(2, n):
        if (isPrime[i]) :

            # Find the largest power of prime 'i'
            # that divides n
            k = largestPower(n, i)

            # Multiply result with (i^k) % p
            res = (res * power(i, k, p)) % p

    return res

# Driver code
if __name__ =="__main__":
    n = 25
    p = 29
    print(modFact(n, p))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program Returns n % p using Sieve of Eratosthenes
using System;

public class GFG {

// Returns largest power of p that divides n!
    static int largestPower(int n, int p) {
        // Initialize result
        int x = 0;

        // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
        while (n > 0) {
            n /= p;
            x += n;
        }
        return x;
    }

// Utility function to do modular exponentiation.
// It returns (x^y) % p
    static int power(int x, int y, int p) {
        int res = 1; // Initialize result
        x = x % p; // Update x if it is more than or
        // equal to p
        while (y > 0) {
            // If y is odd, multiply x with result
            if (y % 2 == 1) {
                res = (res * x) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

// Returns n! % p
    static int modFact(int n, int p) {
        if (n >= p) {
            return 0;
        }

        int res = 1;

        // Use Sieve of Eratosthenes to find all primes
        // smaller than n
        bool []isPrime = new bool[n + 1];
        for(int i = 0;i<n+1;i++)
            isPrime[i] = true;
        for (int i = 2; i * i <= n; i++) {
            if (isPrime[i]) {
                for (int j = 2 * i; j <= n; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Consider all primes found by Sieve
        for (int i = 2; i <= n; i++) {
            if (isPrime[i]) {
                // Find the largest power of prime 'i' that divides n
                int k = largestPower(n, i);

                // Multiply result with (i^k) % p
                res = (res * power(i, k, p)) % p;
            }
        }
        return res;
    }

// Driver method
    static public void Main() {
        int n = 25, p = 29;
        Console.WriteLine(modFact(n, p));

    }
}
// This code is contributed by PrinciRaj19992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Returns n % p
// using Sieve of Eratosthenes

// Returns largest power of p that
// divides n!
function largestPower($n, $p)
{
    // Initialize result
    $x = 0;

    // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while ($n)
    {
        $n = (int)($n / $p);
        $x += $n;
    }
    return $x;
}

// Utility function to do modular exponentiation.
// It returns (x^y) % p
function power($x, $y, $p)
{
    $res = 1; // Initialize result
    $x = $x % $p; // Update x if it is more
                  // than or equal to p
    while ($y > 0)
    {
        // If y is odd, multiply x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Returns n! % p
function modFact($n, $p)
{
    if ($n >= $p)
        return 0;

    $res = 1;

    // Use Sieve of Eratosthenes to find
    // all primes smaller than n
    $isPrime = array_fill(0, $n + 1, true);
    for ($i = 2; $i * $i <= $n; $i++)
    {
        if ($isPrime[$i])
        {
            for ($j = 2 * $i; $j <= $n; $j += $i)
                $isPrime[$j] = 0;
        }
    }

    // Consider all primes found by Sieve
    for ($i = 2; $i <= $n; $i++)
    {
        if ($isPrime[$i])
        {
            // Find the largest power of
            // prime 'i' that divides n
            $k = largestPower($n, $i);

            // Multiply result with (i^k) % p
            $res = ($res * power($i, $k, $p)) % $p;
        }
    }
    return $res;
}

// Driver Code
$n = 25;
$p = 29;
echo modFact($n, $p);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript program Returns n % p
    // using Sieve of Eratosthenes

    // Returns largest power of p
    // that divides n!
    function largestPower(n, p)
    {
        // Initialize result
        let x = 0;

        // Calculate x = n/p + n/(p^2) +
        // n/(p^3) + ....
        while (n > 0) {
            n = parseInt(n / p, 10);
            x += n;
        }
        return x;
    }

    // Utility function to do
    // modular exponentiation.
    // It returns (x^y) % p
    function power(x, y, p)
    {
    // Initialize result
        let res = 1;
   // Update x if it is more than or
        x = x % p;
        // equal to p
        while (y > 0) {
   // If y is odd, multiply x with result
            if (y % 2 == 1) {
                res = (res * x) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Returns n! % p
    function modFact(n, p) {
        if (n >= p) {
            return 0;
        }

        let res = 1;

        // Use Sieve of Eratosthenes
        // to find all primes
        // smaller than n
        let isPrime = new Array(n + 1);
        for(let i = 0;i<n+1;i++)
            isPrime[i] = true;
        for (let i = 2; i * i <= n; i++) {
            if (isPrime[i]) {
                for (let j = 2 * i; j <= n; j += i)
                {
                    isPrime[j] = false;
                }
            }
        }

        // Consider all primes found by Sieve
        for (let i = 2; i <= n; i++) {
            if (isPrime[i]) {
                // Find the largest power of
                // prime 'i' that divides n
                let k = largestPower(n, i);

                // Multiply result with (i^k) % p
                res = (res * power(i, k, p)) % p;
            }
        }
        return res;
    }

    let n = 25, p = 29;
      document.write(modFact(n, p));

</script>
```

**输出:**

```
5
```

这是一个有趣的方法，但是它的时间复杂度比 Simple Method 更高，因为 screen 本身的时间复杂度是 O(n log log n)。如果我们有小于或等于 n 的素数列表，这种方法会很有用。
**方法 3(利用威尔逊定理)**
威尔逊定理指出自然数 p > 1 是素数的当且仅当

```
    (p - 1) ! ≡ -1   mod p 
OR  (p - 1) ! ≡  (p-1) mod p 
```

注意 n！n >= p 时% p 为 0，该方法主要用于 p 接近输入数 n 时，例如(25！% 29).从威尔逊定理，我们知道 28！是-1。所以我们基本上需要求[ (-1) *逆(28，29) *逆(27，29) *逆(26) ] % 29。反函数逆(x，p)返回模 p 下 x 的逆(详见[本](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/))。

## C++

```
// C++ program to comput n! % p using Wilson's Theorem
#include <bits/stdc++.h>
using namespace std;

// Utility function to do modular exponentiation.
// It returns (x^y) % p
int power(int x, unsigned int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p
    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find modular inverse of a under modulo p
// using Fermat's method. Assumption: p is prime
int modInverse(int a, int p)
{
    return power(a, p - 2, p);
}

// Returns n! % p using Wilson's Theorem
int modFact(int n, int p)
{
    // n! % p is 0 if n >= p
    if (p <= n)
        return 0;

    // Initialize result as (p-1)! which is -1 or (p-1)
    int res = (p - 1);

    // Multiply modulo inverse of all numbers from (n+1)
    // to p
    for (int i = n + 1; i < p; i++)
        res = (res * modInverse(i, p)) % p;
    return res;
}

// Driver method
int main()
{
    int n = 25, p = 29;
    cout << modFact(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute n! % p
// using Wilson's Theorem
class GFG
{

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p
static int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p;   // Update x if it is more
                 // than or equal to p
    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find modular
// inverse of a under modulo p
// using Fermat's method.
// Assumption: p is prime
static int modInverse(int a, int p)
{
    return power(a, p - 2, p);
}

// Returns n! % p using
// Wilson's Theorem
static int modFact(int n, int p)
{
    // n! % p is 0 if n >= p
    if (p <= n)
        return 0;

    // Initialize result as (p-1)!
    // which is -1 or (p-1)
    int res = (p - 1);

    // Multiply modulo inverse of
    // all numbers from (n+1) to p
    for (int i = n + 1; i < p; i++)
        res = (res * modInverse(i, p)) % p;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int n = 25, p = 29;
    System.out.println(modFact(n, p));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to comput
# n! % p using Wilson's Theorem

# Utility function to do modular
# exponentiation. It returns (x^y) % p
def power(x, y,p):

    res = 1; # Initialize result
    x = x % p; # Update x if it is more
               # than or equal to p
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p;

        # y must be even now
        y = y >> 1; # y = y/2
        x = (x * x) % p;

    return res

# Function to find modular inverse
# of a under modulo p using Fermat's
# method. Assumption: p is prime
def modInverse(a, p):

    return power(a, p - 2, p)

# Returns n! % p using
# Wilson's Theorem
def modFact(n , p):

    # n! % p is 0 if n >= p
    if (p <= n):
        return 0

    # Initialize result as (p-1)!
    # which is -1 or (p-1)
    res = (p - 1)

    # Multiply modulo inverse of
    # all numbers from (n+1) to p
    for i in range (n + 1, p):
        res = (res * modInverse(i, p)) % p
    return res

# Driver code
n = 25
p = 29
print(modFact(n, p))

# This code is contributed by ihritik
```

## C#

```
// C# program to comput n! % p
// using Wilson's Theorem
using System;

// Utility function to do modular
// exponentiation. It returns (x^y) % p
class GFG
{
public int power(int x, int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more
               // than or equal to p
    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find modular inverse
// of a under modulo p using Fermat's
// method. Assumption: p is prime
public int modInverse(int a, int p)
{
    return power(a, p - 2, p);
}

// Returns n! % p using
// Wilson's Theorem
public int modFact(int n, int p)
{
    // n! % p is 0 if n >= p
    if (p <= n)
        return 0;

    // Initialize result as (p-1)!
    // which is -1 or (p-1)
    int res = (p - 1);

    // Multiply modulo inverse of all
    // numbers from (n+1) to p
    for (int i = n + 1; i < p; i++)
        res = (res * modInverse(i, p)) % p;
    return res;
}

// Driver method
public static void Main()
{
    GFG g = new GFG();
    int n = 25, p = 29;
    Console.WriteLine(g.modFact(n, p));
}
}

// This code is contributed by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to comput
// n!% p using Wilson's Theorem

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p
function power($x, $y, $p)
{
    $res = 1; // Initialize result
    $x = $x % $p; // Update x if it is
                  // more than or equal to p
    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Function to find modular
// inverse of a under modulo
// p using Fermat's method.
// Assumption: p is prime
function modInverse($a, $p)
{
    return power($a, $p - 2, $p);
}

// Returns n! % p
// using Wilson's Theorem
function modFact( $n, $p)
{
    // n! % p is 0
    // if n >= p
    if ($p <= $n)
        return 0;

    // Initialize result as
    // (p-1)! which is -1 or (p-1)
    $res = ($p - 1);

    // Multiply modulo inverse
    // of all numbers from (n+1)
    // to p
    for ($i = $n + 1; $i < $p; $i++)
        $res = ($res *
                modInverse($i, $p)) % $p;
    return $res;
}

// Driver Code
$n = 25; $p = 29;
echo modFact($n, $p);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to comput n! % p
    // using Wilson's Theorem

    // Utility function to do modular
    // exponentiation. It returns (x^y) % p
    function power(x, y, p)
    {
        let res = 1; // Initialize result
        x = x % p; // Update x if it is more
                   // than or equal to p
        while (y > 0)
        {

            // If y is odd, multiply
            // x with result
            if((y & 1) > 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to find modular inverse
    // of a under modulo p using Fermat's
    // method. Assumption: p is prime
    function modInverse(a, p)
    {
        return power(a, p - 2, p);
    }

    // Returns n! % p using
    // Wilson's Theorem
    function modFact(n, p)
    {

        // n! % p is 0 if n >= p
        if (p <= n)
            return 0;

        // Initialize result as (p-1)!
        // which is -1 or (p-1)
        let res = (p - 1);

        // Multiply modulo inverse of all
        // numbers from (n+1) to p
        for (let i = n + 1; i < p; i++)
            res = (res * modInverse(i, p)) % p;
        return res;
    }

    let n = 25, p = 29;
    document.write(modFact(n, p));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
5
```

该方法的时间复杂度为 O((p-n)*Logn)
**方法 4(使用素性检验算法)**

```
1) Initialize: result = 1
2) While n is not prime
    result = (result * n) % p
3) result = (result * (n-1)) % p  // Using Wilson's Theorem 
4) Return result.
```

请注意，上述算法的时间复杂度步骤 2 取决于所使用的素性测试算法和小于 n 的最大素值。以 [AKS](https://en.wikipedia.org/wiki/AKS_primality_test) 算法为例，取 O(Log <sup>10.5</sup> n)时间。
本文由 **Ruchir Garg** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息