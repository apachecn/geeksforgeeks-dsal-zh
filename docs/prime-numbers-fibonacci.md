# 素数和斐波那契数

> 原文:[https://www.geeksforgeeks.org/prime-numbers-fibonacci/](https://www.geeksforgeeks.org/prime-numbers-fibonacci/)

给定一个数，找出同时是斐波那契数和素数的数(小于或等于 n)。

**例:**

```
Input : n = 40
Output: 2 3 5 13
Explanation :
Here, range(upper limit) = 40
Fibonacci series upto n is, 1, 
1, 2, 3, 5, 8, 13, 21, 34.
Prime numbers in above series = 2, 3, 5, 13.

Input : n = 100
Output: 2 3 5 13 89
Explanation :
Here, range(upper limit) = 40
Fibonacci series upto n are 1, 1, 2, 
3, 5, 8, 13, 21, 34, 55, 89.
Prime numbers in Fibonacci upto n : 2, 3, 
5, 13, 89.
```

一个**简单的解决方案**是迭代生成所有小于或等于 n 的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，对于每个斐波那契数，[检查它是否是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果是质数，那就打印出来。

一个**有效的解决方案**是使用[筛来生成 n](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 以内的所有素数。在我们生成素数之后，如果一个数的形式是 5i <sup>2</sup> + 4 或者形式是 5i<sup>2</sup>–4，我们可以通过使用一个数是斐波那契数的属性来快速检查这个数是否是斐波那契数。详见[本](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。

下面是以上步骤的实现

## c++

```
// CPP program to print prime numbers present
// in Fibonacci series.
#include <bits/stdc++.h>
using namespace std;

// Function to check perfect square
bool isSquare(int n)
{
    int sr = sqrt(n);
    return (sr * sr == n);
}

// Prints all numbers less than or equal to n that
// are both Prime and Fibonacci.
void printPrimeAndFib(int n)
{
    // Using Sieve to generate all primes
    // less than or equal to n.
    bool prime[n + 1];   
    memset(prime, true, sizeof(prime));
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Now traverse through the range and print numbers
    // that are both prime and Fibonacci.
    for (int i=2; i<=n; i++)   
       if (prime[i] && (isSquare(5 * i * i + 4) > 0 ||
                        isSquare(5 * i * i - 4) > 0))
                cout << i << " ";
}

// Driver function
int main()
{
    int n = 30;
    printPrimeAndFib(n);
    return 0;
}
```

## Java

```
// Java program to print prime numbers
// present in Fibonacci series.
class PrimeAndFib
{
// Function to check perfect square
Boolean isSquare(int n)
{
    int sr = (int)Math.sqrt(n);
    return (sr * sr == n);
}

// Prints all numbers less than or equal
// to n that are both Prime and Fibonacci.
static void printPrimeAndFib(int n)
{
    // Using Sieve to generate all
    // primes less than or equal to n.
    Boolean[] prime = new Boolean[n + 1];

    // memset(prime, true, sizeof(prime));
    for (int p = 0; p <= n; p++)
    prime[p] = true;
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Now traverse through the range and
    // print numbers that are both prime
    // and Fibonacci.
    for (int i=2; i<=n; i++) {
        double sqrt = Math.sqrt(5 * i * i + 4);
        double sqrt1 = Math.sqrt(5 * i * i - 4);

        int x = (int) sqrt;
        int y = (int) sqrt1;

    if (prime[i]==true && (Math.pow(sqrt,2) ==
        Math.pow(x,2) || Math.pow(sqrt1,2) ==
        Math.pow(y,2)))
        System.out.print(i+" ");
    }
}

// driver program
public static void main(String s[])
{
    int n = 30;
    printPrimeAndFib(n);
}
}

// This code is contributed by Prerna Saini
```

## python 3

```
# Python 3 program to print
# prime numbers present in
# Fibonacci series.
import math

# Function to check perfect square
def isSquare(n) :
    sr = (int)(math.sqrt(n))
    return (sr * sr == n)

# Prints all numbers less than
# or equal to n that  are
# both Prime and Fibonacci.
def printPrimeAndFib(n) :

    # Using Sieve to generate all
    # primes less than or equal to n.
    prime =[True] * (n + 1)
    p = 2
    while(p * p <= n ):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range(p * 2, n + 1, p) :
                prime[i] = False

        p = p + 1

    # Now traverse through the range
    # and print numbers that are
    # both prime and Fibonacci.
    for i in range(2, n + 1) :
        if (prime[i] and (isSquare(5 * i * i + 4) > 0 or
             isSquare(5 * i * i - 4) > 0)) :
            print(i , " ",end="")

# Driver function
n = 30
printPrimeAndFib(n);

# This code is contributed
# by Nikita Tiwari.
```

T19【c#

```
// C# program to print prime numbers
// present in Fibonacci series.
using System;

class GFG {

    // Function to check perfect square
    static bool isSquare(int n)
    {
        int sr = (int)Math.Sqrt(n);

        return (sr * sr == n);
    }

    // Prints all numbers less than or equal
    // to n that are both Prime and Fibonacci.
    static void printPrimeAndFib(int n)
    {

        // Using Sieve to generate all
        // primes less than or equal to n.
        bool[] prime = new bool[n + 1];

        // memset(prime, true, sizeof(prime));
        for (int p = 0; p <= n; p++)
            prime[p] = true;

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Now traverse through the range and
        // print numbers that are both prime
        // and Fibonacci.
        for (int i = 2; i <= n; i++) {

            double sqrt = Math.Sqrt(5 * i * i + 4);
            double sqrt1 = Math.Sqrt(5 * i * i - 4);

            int x = (int) sqrt;
            int y = (int) sqrt1;

        if (prime[i] == true && (Math.Pow(sqrt, 2) ==
             Math.Pow(x, 2) || Math.Pow(sqrt1, 2) ==
                                    Math.Pow(y, 2)))
            Console.Write(i + " ");
        }
    }

    // driver program
    public static void Main()
    {
        int n = 30;

        printPrimeAndFib(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## PHP

```
<?php
// PHP program to print prime numbers
// present in Fibonacci series.

// Function to check perfect square
function isSquare($n)
{
    $sr = (int)sqrt($n);
    return ($sr * $sr == $n);
}

// Prints all numbers less than or equal
// to n that are both Prime and Fibonacci.
function printPrimeAndFib($n)
{
    // Using Sieve to generate all primes
    // less than or equal to n.
    $prime = array_fill(0, $n + 1, true);
    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    // Now traverse through the range
    // and print numbers that are both
    // prime and Fibonacci.
    for ($i = 2; $i <= $n; $i++)
    if ($prime[$i] && (isSquare(5 * $i * $i + 4) > 0 ||
                       isSquare(5 * $i * $i - 4) > 0))
        echo $i . " ";
}

// Driver Code
$n = 30;
printPrimeAndFib($n);

// This code is contributed by mits
?>
```

## Javascript

```
<script>

// Javascript program to print prime numbers
// present in Fibonacci series.

// Function to check perfect square
function isSquare(n)
{
    let sr = Math.sqrt(n);
    return (sr * sr == n);
}

// Prints all numbers less than or equal
// to n that are both Prime and Fibonacci.
function prletPrimeAndFib(n)
{
    // Using Sieve to generate all
    // primes less than or equal to n.
    let prime = [];

    // memset(prime, true, sizeof(prime));
    for (let p = 0; p <= n; p++)
    prime[p] = true;
    for (let p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Now traverse through the range and
    // print numbers that are both prime
    // and Fibonacci.
    for (let i=2; i<=n; i++) {
        let sqrt = Math.sqrt(5 * i * i + 4);
        let sqrt1 = Math.sqrt(5 * i * i - 4);

        let x = Math.floor(sqrt);
        let y = Math.floor(sqrt1);

    if (prime[i]==true && (Math.pow(sqrt,2) ==
        Math.pow(x,2) || Math.pow(sqrt1,2) ==
        Math.pow(y,2)))
        document.write(i+" ");
    }
}

// Driver code

    let n = 30;
    printPrimeAndFib(n);

</script>
```

**输出:**

```
2 3 5 13
```