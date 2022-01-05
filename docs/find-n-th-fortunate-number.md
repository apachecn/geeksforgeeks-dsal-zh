# 找到第 n 个幸运数字

> 原文:[https://www.geeksforgeeks.org/find-n-th-fortunate-number/](https://www.geeksforgeeks.org/find-n-th-fortunate-number/)

幸运数是最小的整数 m > 1，因此，对于给定的正整数 n，p <sub>n</sub> + m 是素数。这里 p <sub>n</sub> 是前 n 个素数的乘积，即 n 阶
**的素阶乘(或[素阶乘](https://www.geeksforgeeks.org/primorial-of-a-number/))例如:**

```
p3 = 2 × 3 × 5 = 30
p4 = 2 × 3 × 5 × 7 = 210
p5 = 2 × 3 × 5 × 7 × 11 = 2310
```

现在，质因数 p <sub>n</sub> 和大于 p <sub>n</sub> 的第一个质数之间的最小差 m(m>1)是一个质数。
**例:**

```
Input : n = 3
Output : 7
Explanation : 7 must be added to the product
of first n prime numbers to make the product 
prime. 2 x 3 x 5 = 30, need to add 7 to make 
it 37, which is a prime

Input : n = 5
Output : 23
```

**逼近**:求第 n 个幸运数，计算前 n 个素数(primorial)的乘积。让这个乘积是 p，然后我们找到大于 p 的质数，并返回找到的质数和 p 的差

```
p4 + 13 = 223, where m = 13, a fortunate number
p5 + 23 = 2333, where m = 23, a fortunate number
p6 + 17 = 30047, where m = 17, a fortunate number
```

## C++

```
// C++ program to find n-th Fortunate number
#include <bits/stdc++.h>
using namespace std;

bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)  return false;
    if (n <= 3)  return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
           return false;

    return true;
}

// Function to Find primorial of order n
// (product of first n prime numbers).
long long int primorial(long long int n)
{
    long long int p = 2;
    n--;
    for (int i = 3; n != 0; i++) {
        if (isPrime(i)) {
            p = p * i;
            n--;
        }
        i++;
    }
    return p;
}

// Function to find next prime number greater
// than n
long long int findNextPrime(long long int n)
{
    // Note that difference (or m) should be
    // greater than 1.
    long long int nextPrime = n + 2;

    // loop continuously until isPrime
    // returns true for a number above n
    while (true) {

        // Ignoring the prime number that
        // is 1 greater than n
        if (isPrime(nextPrime))
            break;

        nextPrime++;
    }

    return nextPrime;
}

// Returns n-th Fortunate number
long long int fortunateNumber(int n)
{
   long long int p = primorial(n);
   return findNextPrime(p) - p;
}

// Driver function
int main()
{
    long long int n = 5;
    cout << fortunateNumber(n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th Fortunate number
import java.lang.*;
import java.util.*;

class GFG
{

    public static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0) return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
            return false;

        return true;
    }

    // Function to Find primorial of order n
    // (product of first n prime numbers).
    public static int primorial(int n)
    {
        int p = 2;
        n--;
        for (int i = 3; n != 0; i++) {
            if (isPrime(i) == true) {
                p = p * i;
                n--;
            }
            i++;
        }
        return p;
    }

    // Function to find next prime number greater
    // than n
    public static int findNextPrime(int n)
    {
        // Note that difference (or m) should be
        // greater than 1.
        int nextPrime = n + 2;

        // loop continuously until isPrime
        // returns true for a number above n
        while (true) {

            // Ignoring the prime number that
            // is 1 greater than n
            if (isPrime(nextPrime) == true)
                break;

            nextPrime++;
       }

    return nextPrime;
    }

    // Returns n-th Fortunate number
    public static int fortunateNumber(int n)
    {
        int p = primorial(n);
        return findNextPrime(p)-p;
    }

    //Driver function
    public static void main (String[] args) {
        int n = 5;
        System.out.println(fortunateNumber(n));
    }
}

/*This code is contributed by Akash Singh*/
```

## 蟒蛇 3

```
# Python3 program to find
# n-th Fortunate number

def isPrime(n):

    # Corner cases
    if (n <= 1): return False
    if (n <= 3): return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while(i * i <= n):
        if (n % i == 0 or
            n % (i + 2) == 0):
            return False
        i += 6

    return True

# Function to Find primorial of order n
# (product of first n prime numbers).
def primorial(n):

    p = 2; n -= 1; i = 3
    while(n != 0):
        if (isPrime(i)):
            p = p * i
            n -= 1

        i += 1

    return p

# Function to find next prime
# number greater than n
def findNextPrime(n):

    # Note that difference (or m)
    # should be greater than 1.
    nextPrime = n + 2

    # loop continuously until isPrime
    # returns true for a number above n
    while (True):

        # Ignoring the prime number that
        # is 1 greater than n
        if (isPrime(nextPrime)):
            break

        nextPrime += 1

    return nextPrime

# Returns n-th Fortunate number
def fortunateNumber(n):
    p = primorial(n)
    return findNextPrime(p) - p

# Driver Code
n = 5
print(fortunateNumber(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find
// n-th Fortunate number
using System;

class GFG
{
    public static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that
        // we can skip middle five
        // numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5;
                 i * i <= n; i = i + 6)
            if (n % i == 0 ||
                n % (i + 2) == 0)
            return false;

        return true;
    }

    // Function to Find primorial
    // of order n (product of first
    // n prime numbers).
    public static int primorial(int n)
    {
        int p = 2;
        n--;
        for (int i = 3; n != 0; i++)
        {
            if (isPrime(i) == true)
            {
                p = p * i;
                n--;
            }
            i++;
        }
        return p;
    }

    // Function to find next
    // prime number greater than n
    public static int findNextPrime(int n)
    {
        // Note that difference (or m)
        // should be greater than 1.
        int nextPrime = n + 2;

        // loop continuously until
        // isPrime returns true
        // for a number above n
        while (true)
        {

            // Ignoring the prime number
            // that is 1 greater than n
            if (isPrime(nextPrime) == true)
                break;

            nextPrime++;
    }

    return nextPrime;
    }

    // Returns n-th
    // Fortunate number
    public static int fortunateNumber(int n)
    {
        int p = primorial(n);
        return findNextPrime(p) - p;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 5;
        Console.WriteLine(fortunateNumber(n));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// Fortunate number

function isPrime($n)
{

    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for($i = 5; $i * $i <= $n;
                  $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
        return false;

    return true;
}

// Function to Find primorial of order n
// (product of first n prime numbers).
function primorial($n)
{
    $p = 2;
    $n--;
    for ($i = 3; $n != 0; $i++)
    {
        if (isPrime($i))
        {
            $p = $p * $i;
            $n--;
        }
        $i++;
    }
    return $p;
}

// Function to find next prime
// number greater than n
function findNextPrime($n)
{

    // Note that difference (or m)
    // should be greater than 1.
    $nextPrime = $n + 2;

    // loop continuously until isPrime
    // returns true for a number above n
    while (true)
    {

        // Ignoring the prime number that
        // is 1 greater than n
        if (isPrime($nextPrime))
            break;

        $nextPrime++;
    }

    return $nextPrime;
}

// Returns n-th Fortunate number
function fortunateNumber($n)
{
    $p = primorial($n);
    return findNextPrime($p) - $p;
}

    // Driver Code
    $n = 5;
    echo fortunateNumber($n) , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find n-th Fortunate number

    function isPrime(n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0) return false;

        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
            return false;

        return true;
    }

    // Function to Find primorial of order n
    // (product of first n prime numbers).
    function primorial(n)
    {
        let p = 2;
        n--;
        for (let i = 3; n != 0; i++) {
            if (isPrime(i) == true) {
                p = p * i;
                n--;
            }
            i++;
        }
        return p;
    }

    // Function to find next prime number greater
    // than n
    function findNextPrime(n)
    {
        // Note that difference (or m) should be
        // greater than 1.
        let nextPrime = n + 2;

        // loop continuously until isPrime
        // returns true for a number above n
        while (true) {

            // Ignoring the prime number that
            // is 1 greater than n
            if (isPrime(nextPrime) == true)
                break;

            nextPrime++;
       }

    return nextPrime;
    }

    // Returns n-th Fortunate number
    function fortunateNumber(n)
    {
        let p = primorial(n);
        return findNextPrime(p)-p;
    }

// Driver Code

        let n = 5;
        document.write(fortunateNumber(n));

</script>
```

**Output:** 

```
23
```

**优化**:以上方案可以使用厄拉多塞的[筛进行优化。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)