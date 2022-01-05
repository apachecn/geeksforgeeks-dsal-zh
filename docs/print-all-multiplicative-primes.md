# 打印所有乘法素数< = N

> 原文:[https://www . geesforgeks . org/print-all-乘法-primes/](https://www.geeksforgeeks.org/print-all-multiplicative-primes/)

给定一个整数 **N** ，任务是打印所有乘法素数 **≤ N** 。

> **乘法素数**是这样的素数，它们的位数的乘积也是素数。比如；2、3、7、13、17、……

**例:**

> **输入:**N = 10
> T3】输出:2 3 5 7
> T6】输入:N = 3
> T9】输出: 2 3

**方法:**使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)检查所有素数 **≤ N** 是否为乘法素数，即其位数的乘积也是素数。如果是，那么打印那些乘法素数。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the digit product of n
int digitProduct(int n)
{
    int prod = 1;
    while (n) {
        prod = prod * (n % 10);
        n = n / 10;
    }

    return prod;
}

// Function to print all multiplicative primes <= n
void printMultiplicativePrimes(int n)
{
    // Create a boolean array "prime[0..n+1]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p]) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    for (int i = 2; i <= n; i++) {

        // If i is prime and its digit sum is also prime
        // i.e. i is a multiplicative prime
        if (prime[i] && prime[digitProduct(i)])
            cout << i << " ";
    }
}

// Driver code
int main()
{
    int n = 10;
    printMultiplicativePrimes(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the digit product of n
static int digitProduct(int n)
{
    int prod = 1;
    while (n > 0)
    {
        prod = prod * (n % 10);
        n = n / 10;
    }
    return prod;
}

// Function to print all multiplicative primes <= n
static void printMultiplicativePrimes(int n)
{
    // Create a boolean array "prime[0..n+1]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[] = new boolean[n + 1 ];
    for(int i = 0; i <= n; i++)
     prime[i] = true;

    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p])
        {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    for (int i = 2; i <= n; i++)
    {

        // If i is prime and its digit sum is also prime
        // i.e. i is a multiplicative prime
        if (prime[i] && prime[digitProduct(i)])
            System.out.print( i + " ");
    }
}

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;
        printMultiplicativePrimes(n);
    }
}

// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function to return the digit product of n
def digitProduct(n):
    prod = 1
    while (n):
        prod = prod * (n % 10)
        n = int(n / 10)

    return prod

# Function to print all multiplicative
# primes <= n
def printMultiplicativePrimes(n):

    # Create a boolean array "prime[0..n+1]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(n + 1)]

    prime[0] = prime[1] = False
    for p in range(2, int(sqrt(n)) + 1, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = False

    for i in range(2, n + 1, 1):

        # If i is prime and its digit sum
        # is also prime i.e. i is a
        # multiplicative prime
        if (prime[i] and prime[digitProduct(i)]):
            print(i, end = " ")

# Driver code
if __name__ == '__main__':
    n = 10
    printMultiplicativePrimes(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
class GFG
{

// Function to return the digit product of n
static int digitProduct(int n)
{
    int prod = 1;
    while (n > 0)
    {
        prod = prod * (n % 10);
        n = n / 10;
    }
    return prod;
}

// Function to print all multiplicative primes <= n
static void printMultiplicativePrimes(int n)
{
    // Create a boolean array "prime[0..n+1]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool[] prime = new bool[n + 1 ];

    for(int i = 0; i <= n; i++)
        prime[i] = true;

    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p])
        {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    for (int i = 2; i <= n; i++)
    {

        // If i is prime and its digit sum is also prime
        // i.e. i is a multiplicative prime
        if (prime[i] && prime[digitProduct(i)])
            System.Console.Write( i + " ");
    }
}

    // Driver code
    static void Main()
    {
        int n = 10;
        printMultiplicativePrimes(n);
    }
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the digit product of n
function digitProduct($n)
{
    $prod = 1;
    while ($n)
    {
        $prod = $prod * ($n % 10);
        $n = floor($n / 10);
    }

    return $prod;
}

// Function to print all multiplicative
// primes <= n
function printMultiplicativePrimes($n)
{
    // Create a boolean array "prime[0..n+1]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    $prime = array_fill(0, $n + 1, true);

    $prime[0] = $prime[1] = false;
    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p])
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    for ($i = 2; $i <= $n; $i++)
    {

        // If i is prime and its digit sum is also
        // prime i.e. i is a multiplicative prime
        if ($prime[$i] && $prime[digitProduct($i)])
            echo $i, " ";
    }
}

// Driver code
$n = 10;
printMultiplicativePrimes($n);

// This code is contributed by Ryuga.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function to return the digit product of n
    function digitProduct(n)
    {
        let prod = 1;
        while (n > 0)
        {
            prod = prod * (n % 10);
            n = Math.floor(n / 10);
        }
        return prod;
    }

    // Function to print all
    // multiplicative primes <= n
    function printMultiplicativePrimes(n)
    {
        // Create a boolean array "prime[0..n+1]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        let prime = new Array(n + 1);
        for(let i = 0; i <= n; i++)
            prime[i] = true;

        prime[0] = prime[1] = false;
        for (let p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p])
            {

                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        for (let i = 2; i <= n; i++)
        {

            // If i is prime and its digit sum is also prime
            // i.e. i is a multiplicative prime
            if (prime[i] && prime[digitProduct(i)])
                document.write( i + " ");
        }
    }

    // Driver code
    let n = 10;
    printMultiplicativePrimes(n);

    // This code is contributed by unknown2108

</script>
```

**Output:** 

```
2 3 5 7
```