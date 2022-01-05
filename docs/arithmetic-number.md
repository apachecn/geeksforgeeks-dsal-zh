# 算术数

> 原文:[https://www.geeksforgeeks.org/arithmetic-number/](https://www.geeksforgeeks.org/arithmetic-number/)

在数论中，[算术数](https://en.wikipedia.org/wiki/Arithmetic_number)是一个整数，它的正整数因子的平均值也是一个整数。或者换句话说，如果除数除以除数之和，N 就是算术数。
给定正整数 **n** 。任务是检查 n 是否是算术数。
**例:**

```
Input : n = 6
Output : Yes
Sum of divisor of 6 = 1 + 2 + 3 + 6 = 12.
Number of divisor of 6 = 4.
So, on dividing Sum of divisor by Number of divisor
= 12/4 = 3, which is an integer.

Input : n = 2
Output : No
```

**算法**

1.  求[一个数的所有因子的和](https://www.geeksforgeeks.org/sum-factors-number/)，说和。
2.  找到[除数](https://www.geeksforgeeks.org/count-divisors-n-on13/)(说计数)。
3.  检查总和是否能被计数整除。

## C++

```
// CPP program to check if a number is Arithmetic
// number or not
#include <bits/stdc++.h>
using namespace std;

// Sieve Of Eratosthenes
void SieveOfEratosthenes(int n, bool prime[],
                         bool primesquare[], int a[])
{
    for (int i = 2; i <= n; i++)
        prime[i] = true;

    for (int i = 0; i <= (n * n + 1); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    int j = 0;
    for (int p = 2; p <= n; p++) {
        if (prime[p]) {
            // Storing primes in an array
            a[j] = p;

            // Update value in primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
int countDivisors(int n)
{
    // If number is 1, then it will have only 1
    // as a factor. So, total factors will be 1.
    if (n == 1)
        return 1;

    bool prime[n + 1], primesquare[n * n + 1];

    int a[n]; // for storing primes upto n

    // Calling SieveOfEratosthenes to store prime
    // factors of n and to store square of prime
    // factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number of
    // distinct divisors
    int ans = 1;

    // Loop for counting factors of n
    for (int i = 0;; i++) {

        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        // cnt is power of prime a[i] in n.
        int cnt = 1;

        // if a[i] is a factor of n
        while (n % a[i] == 0)
        {
            n = n / a[i];
            cnt = cnt + 1; // incrementing power
        }

        // Calculating number of divisors
        // If n = a^p * b^q then total
        // divisors of n
        // are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // if a[i] is greater than cube root of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    return ans; // Total divisors
}

// Returns sum of all factors of n.
int sumofFactors(int n)
{
    // Traversing through all prime factors.
    int res = 1;
    for (int i = 2; i <= sqrt(n); i++) {

        int count = 0, curr_sum = 1;
        int curr_term = 1;
        while (n % i == 0) {
            count++;
            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Check if number is Arithmetic Number
// or not.
bool checkArithmetic(int n)
{
    int count = countDivisors(n);
    int sum = sumofFactors(n);

    return (sum  % count == 0);
}

// Driven Program
int main()
{
    int n = 6;
    (checkArithmetic(n)) ? (cout << "Yes") :
                           (cout << "No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is Arithmetic
// number or not
class GFG
{

// Sieve Of Eratosthenes
static void SieveOfEratosthenes(int n, boolean prime[],
                        boolean primesquare[], int a[])
{
    for (int i = 2; i <= n; i++)
        prime[i] = true;

    for (int i = 0; i <= (n * n ); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for (int p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    int j = 0;
    for (int p = 2; p <= n; p++)
    {
        if (prime[p])
        {
            // Storing primes in an array
            a[j] = p;

            // Update value in primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
static int countDivisors(int n)
{
    // If number is 1, then it will have only 1
    // as a factor. So, total factors will be 1.
    if (n == 1)
        return 1;

    boolean prime[] = new boolean[n + 1],
            primesquare[] = new boolean[n * n + 1];

    int a[] = new int[n]; // for storing primes upto n

    // Calling SieveOfEratosthenes to store prime
    // factors of n and to store square of prime
    // factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number of
    // distinct divisors
    int ans = 1;

    // Loop for counting factors of n
    for (int i = 0;; i++)
    {

        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        // cnt is power of prime a[i] in n.
        int cnt = 1;

        // if a[i] is a factor of n
        while (n % a[i] == 0)
        {
            n = n / a[i];
            cnt = cnt + 1; // incrementing power
        }

        // Calculating number of divisors
        // If n = a^p * b^q then total
        // divisors of n
        // are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // if a[i] is greater than cube root of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    return ans; // Total divisors
}

// Returns sum of all factors of n.
static int sumofFactors(int n)
{
    // Traversing through all prime factors.
    int res = 1;
    for (int i = 2; i <= Math.sqrt(n); i++)
    {

        int count = 0, curr_sum = 1;
        int curr_term = 1;
        while (n % i == 0)
        {
            count++;
            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Check if number is Arithmetic Number
// or not.
static boolean checkArithmetic(int n)
{
    int count = countDivisors(n);
    int sum = sumofFactors(n);

    return (sum % count == 0);
}

// Driver Program
public static void main(String[] args)
{
    int n = 6;
    if(checkArithmetic(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if
# a number is Arithmetic
# number or not
import math

# Sieve Of Eratosthenes
def SieveOfEratosthenes(n, prime,primesquare, a):

    for i in range(2,n+1):
        prime[i] = True;

    for i in range((n * n + 1)+1):
        primesquare[i] = False;

    # 1 is not a
    # prime number
    prime[1] = False;
    p = 2;

    while (p * p <= n):

        # If prime[p] is
        # not changed, then
        # it is a prime
        if (prime[p] == True):
            # Update all multiples of p
            for i in range(p * 2,n+1,p):
                prime[i] = False;
        p+=1;

    j = 0;
    for p in range(2,n+1):
        if (prime[p]):

            # Storing primes in an array
            a[j] = p;

            # Update value in
            # primesquare[p*p],
            # if p is prime.
            primesquare[p * p] = True;
            j+=1;

# Function to count divisors
def countDivisors(n):

    # If number is 1, then it
    # will have only 1 as a
    # factor. So, total factors
    # will be 1.
    if (n == 1):
        return 1;

    prime = [False]*(n + 2);
    primesquare = [False]*(n *n + 3);

    # for storing primes upto n
    a = [0]*n;

    # Calling SieveOfEratosthenes
    # to store prime factors of
    # n and to store square of
    # prime factors of n
    SieveOfEratosthenes(n, prime,primesquare, a);

    # ans will contain
    # total number of
    # distinct divisors
    ans = 1;

    # Loop for counting
    # factors of n
    for i in range(0,True):

        # a[i] is not less
        # than cube root n
        if (a[i] * a[i] * a[i] > n):
            break;

        # Calculating power of
        # a[i] in n. cnt is power
        # of prime a[i] in n.
        cnt = 1;

        # if a[i] is a factor of n
        while (n % a[i] == 0):
            n //= a[i];

            # incrementing power
            cnt = cnt + 1;

        # Calculating number of
        # divisors. If n = a^p * b^q
        # then total divisors
        # of n are (p+1)*(q+1)
        ans = ans * cnt;

    # if a[i] is greater
    # than cube root of n

    # First case
    if (prime[n]):
        ans = ans * 2;

    # Second case
    elif (primesquare[n]):
        ans = ans * 3;

    # Third case
    elif (n != 1):
        ans = ans * 4;

    return ans; # Total divisors

# Returns sum of
# all factors of n.
def sumofFactors(n):

    # Traversing through
    # all prime factors.
    res = 1;
    for i in range(2,int(math.sqrt(n))+1):
        count = 0;
        curr_sum = 1;
        curr_term = 1;
        while (n % i == 0):
            count+=1;
            n //= i;

            curr_term *= i;
            curr_sum += curr_term;

        res *= curr_sum;

    # This condition is to handle
    # the case when n is a prime
    # number greater than 2.
    if (n >= 2):
        res *= (1 + n);

    return res;

# Check if number is
# Arithmetic Number or not.
def checkArithmetic(n):

    count = countDivisors(n);
    sum = sumofFactors(n);

    return (sum % count == 0);

# Driver code
n = 6;
if(checkArithmetic(n)):
    print("Yes");
else:
    print("No");

# This code is contributed
# by mits
```

## C#

```
// C# program to check if a number
// is arithmetic number or not
using System;

class GFG
{

// Sieve Of Eratosthenes
static void SieveOfEratosthenes(int n, bool []prime,
                        bool []primesquare, int []a)
{
    for (int i = 2; i <= n; i++)
        prime[i] = true;

    for (int i = 0; i <= (n * n ); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for (int p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    int j = 0;
    for (int p = 2; p <= n; p++)
    {
        if (prime[p])
        {
            // Storing primes in an array
            a[j] = p;

            // Update value in primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
static int countDivisors(int n)
{
    // If number is 1, then it will have only 1
    // as a factor. So, total factors will be 1.
    if (n == 1)
        return 1;

    bool []prime = new bool[n + 1];
    bool []primesquare = new bool[n * n + 1];

    int []a = new int[n]; // for storing primes upto n

    // Calling SieveOfEratosthenes to store prime
    // factors of n and to store square of prime
    // factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number of
    // distinct divisors
    int ans = 1;

    // Loop for counting factors of n
    for (int i = 0;; i++)
    {

        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        // cnt is power of prime a[i] in n.
        int cnt = 1;

        // if a[i] is a factor of n
        while (n % a[i] == 0)
        {
            n = n / a[i];
            cnt = cnt + 1; // incrementing power
        }

        // Calculating number of divisors
        // If n = a^p * b^q then total
        // divisors of n
        // are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // if a[i] is greater than cube root of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    return ans; // Total divisors
}

// Returns sum of all factors of n.
static int sumofFactors(int n)
{
    // Traversing through all prime factors.
    int res = 1;
    for (int i = 2; i <= Math.Sqrt(n); i++)
    {

        int count = 0, curr_sum = 1;
        int curr_term = 1;
        while (n % i == 0)
        {
            count++;
            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Check if number is Arithmetic Number
// or not.
static bool checkArithmetic(int n)
{
    int count = countDivisors(n);
    int sum = sumofFactors(n);

    return (sum % count == 0);
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    if(checkArithmetic(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is Arithmetic
// number or not

// Sieve Of Eratosthenes
function SieveOfEratosthenes($n, &$prime,
                             &$primesquare, &$a)
{
    for ($i = 2; $i <= $n; $i++)
        $prime[$i] = true;

    for ($i = 0;
         $i <= ($n * $n + 1); $i++)
        $primesquare[$i] = false;

    // 1 is not a
    // prime number
    $prime[1] = false;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is
        // not changed, then
        // it is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p * 2;  
                 $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    $j = 0;
    for ($p = 2; $p <= $n; $p++)
    {
        if ($prime[$p])
        {
            // Storing primes in an array
            $a[$j] = $p;

            // Update value in
            // primesquare[p*p],
            // if p is prime.
            $primesquare[$p * $p] = true;
            $j++;
        }
    }
}

// Function to count divisors
function countDivisors($n)
{
    // If number is 1, then it
    // will have only 1 as a
    // factor. So, total factors
    // will be 1.
    if ($n == 1)
        return 1;

    $prime = array_fill(0, ($n + 1), false);
    $primesquare = array_fill(0, ($n *
                              $n + 1), false);

    // for storing primes upto n
    $a = array_fill(0, $n, 0);

    // Calling SieveOfEratosthenes
    // to store prime factors of
    // n and to store square of
    // prime factors of n
    SieveOfEratosthenes($n, $prime,
                        $primesquare, $a);

    // ans will contain
    // total number of
    // distinct divisors
    $ans = 1;

    // Loop for counting
    // factors of n
    for ($i = 0;; $i++)
    {

        // a[i] is not less
        // than cube root n
        if ($a[$i] * $a[$i] * $a[$i] > $n)
            break;

        // Calculating power of
        // a[i] in n. cnt is power
        // of prime a[i] in n.
        $cnt = 1;

        // if a[i] is a factor of n
        while ($n % $a[$i] == 0)
        {
            $n = (int)($n / $a[$i]);

            // incrementing power
            $cnt = $cnt + 1;
        }

        // Calculating number of
        // divisors. If n = a^p * b^q
        // then total divisors
        // of n are (p+1)*(q+1)
        $ans = $ans * $cnt;
    }

    // if a[i] is greater
    // than cube root of n

    // First case
    if ($prime[$n])
        $ans = $ans * 2;

    // Second case
    else if ($primesquare[$n])
        $ans = $ans * 3;

    // Third case
    else if ($n != 1)
        $ans = $ans * 4;

    return $ans; // Total divisors
}

// Returns sum of
// all factors of n.
function sumofFactors($n)
{
    // Traversing through
    // all prime factors.
    $res = 1;
    for ($i = 2;
         $i <= sqrt($n); $i++)
    {
        $count = 0;
        $curr_sum = 1;
        $curr_term = 1;
        while ($n % $i == 0)
        {
            $count++;
            $n = (int)($n / $i);

            $curr_term *= $i;
            $curr_sum += $curr_term;
        }

        $res *= $curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if ($n >= 2)
        $res *= (1 + $n);

    return $res;
}

// Check if number is
// Arithmetic Number or not.
function checkArithmetic($n)
{
    $count = countDivisors($n);
    $sum = sumofFactors($n);

    return ($sum % $count == 0);
}

// Driver code
$n = 6;
echo (checkArithmetic($n)) ?
                     "Yes" : "No";

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number is Arithmetic
// number or not

// Sieve Of Eratosthenes
function SieveOfEratosthenes(n, prime, primesquare, a)
{
    for (var i = 2; i <= n; i++)
        prime[i] = true;

    for (var i = 0; i <= (n * n + 1); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for (var p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (var i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    var j = 0;
    for (var p = 2; p <= n; p++) {
        if (prime[p]) {
            // Storing primes in an array
            a[j] = p;

            // Update value in primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
function countDivisors(n)
{
    // If number is 1, then it will have only 1
    // as a factor. So, total factors will be 1.
    if (n == 1)
        return 1;

    var prime = Array(n+1).fill(false);

    var primesquare = Array(n * n + 1).fill(0);

    var a = Array(n).fill(0); // for storing primes upto n

    // Calling SieveOfEratosthenes to store prime
    // factors of n and to store square of prime
    // factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number of
    // distinct divisors
    var ans = 1;

    // Loop for counting factors of n
    for (var i = 0;; i++) {

        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        // cnt is power of prime a[i] in n.
        var cnt = 1;

        // if a[i] is a factor of n
        while (n % a[i] == 0)
        {
            n = parseInt(n / a[i]);
            cnt = cnt + 1; // incrementing power
        }

        // Calculating number of divisors
        // If n = a^p * b^q then total
        // divisors of n
        // are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // if a[i] is greater than cube root of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    return ans; // Total divisors
}

// Returns sum of all factors of n.
function sumofFactors(n)
{
    // Traversing through all prime factors.
    var res = 1;
    for (var i = 2; i <= Math.sqrt(n); i++) {

        var count = 0, curr_sum = 1;
        var curr_term = 1;
        while (n % i == 0) {
            count++;
            n = parseInt(n / i);

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Check if number is Arithmetic Number
// or not.
function checkArithmetic(n)
{
    var count = countDivisors(n);
    var sum = sumofFactors(n);

    return (sum  % count == 0);
}

// Driven Program
var n = 6;
(checkArithmetic(n)) ? (document.write( "Yes")) :
                       (document.write( "No"));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```