# 打印 N 以内的所有原素

> 原文:[https://www . geesforgeks . org/print-all-Prost-primes-up-n/](https://www.geeksforgeeks.org/print-all-proth-primes-up-to-n/)

给定一个数字 N，任务是检查给定的数字是否为**Prost Prime**。
一个**原质数**是一个[原质数](https://www.geeksforgeeks.org/program-to-check-whether-a-number-is-proth-number-or-not/)是原质数。
前几个原素是–

> 3, 5, 13, 17, 41, 97, 113, 193, 241, 257, 353, 449, 577, 641, 673, 769, 929, 1153, 1217, … ..

**例:**

```
Input: 41
Output: 41 is Proth Prime

Input: 19
Output: 19 is not a Proth Prime
```

**方法:**
想法是使用厄拉多塞的[筛子来寻找阿普顿的素数。然后检查给定的号码是否为](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[原号码](https://www.geeksforgeeks.org/program-to-check-whether-a-number-is-proth-number-or-not/)。如果数是一个[原数](https://www.geeksforgeeks.org/program-to-check-whether-a-number-is-proth-number-or-not/)并且也是一个素数，那么给定的数就是原素数。
以下是上述算法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
int prime[1000000];

// Calculate all primes upto n.
void SieveOfEratosthenes(int n)
{
    // Initialize all entries it as true.
    // A value in prime[i] will finally
    // false if i is Not a prime, else true.
    for (int i = 1; i <= n + 1; i++)
        prime[i] = true;

    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to
            // the square of it numbers
            // which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Utility function to check power of two
bool isPowerOfTwo(int n)
{
    return (n && !(n & (n - 1)));
}

// Function to check if the Given
// number is Proth number or not
bool isProthNumber(int n)
{

    int k = 1;
    while (k < (n / k)) {

        // check if k divides n or not
        if (n % k == 0) {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo(n / k))
                return true;
        }

        // update k to next odd number
        k = k + 2;
    }

    // If we reach here means there
    // exists no value of K such
    // that k is odd number and n/k
    // is a power of 2 greater than k
    return false;
}

// Function to check whether the given
// number is Proth Prime or Not.
bool isProthPrime(int n)
{
    // Check n for Proth Number
    if (isProthNumber(n - 1)) {

        // if number is prime, return true
        if (prime[n])
            return true;
        else
            return false;
    }
    else
        return false;
}

// Driver Code
int main()
{
    int n = 41;

    // if number is proth number,
    // calculate primes upto n
    SieveOfEratosthenes(n);

    for (int i = 1; i <= n; i++)
        // Check n for Proth Prime
        if (isProthPrime(i))
            cout << i << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

static boolean[] prime = new boolean[1000000];

// Calculate all primes upto n.
static void SieveOfEratosthenes(int n)
{
    // Initialize all entries it as true.
    // A value in prime[i] will finally
    // false if i is Not a prime, else true.
    for (int i = 1; i <= n + 1; i++)
        prime[i] = true;

    prime[1] = false;

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // greater than or equal to
            // the square of it numbers
            // which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Utility function to check power of two
static boolean isPowerOfTwo(int n)
{
    return (n > 0 && (n & (n - 1)) == 0);
}

// Function to check if the Given
// number is Proth number or not
static boolean isProthNumber(int n)
{

    int k = 1;
    while (k < (int)(n / k))
    {

        // check if k divides n or not
        if (n % k == 0)
        {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo((int)(n / k)))
                return true;
        }

        // update k to next odd number
        k = k + 2;
    }

    // If we reach here means there
    // exists no value of K such
    // that k is odd number and n/k
    // is a power of 2 greater than k
    return false;
}

// Function to check whether the given
// number is Proth Prime or Not.
static boolean isProthPrime(int n)
{
    // Check n for Proth Number
    if (isProthNumber(n - 1))
    {

        // if number is prime, return true
        if (prime[n])
            return true;
        else
            return false;
    }
    else
        return false;
}

// Driver Code
public static void main(String args[])
{
    int n = 41;

    // if number is proth number,
    // calculate primes upto n
    SieveOfEratosthenes(n);

    for (int i = 1; i <= n; i++)
        // Check n for Proth Prime
        if (isProthPrime(i))
            System.out.println(i);
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
import math as mt

prime = [0 for i in range(1000000)]

# Calculate all primes upto n.
def SieveOfEratosthenes(n):

    # Initialize all entries it as true.
    # A value in prime[i] will finally
    # false if i is Not a prime, else true.
    for i in range(1, n + 2):
        prime[i] = True

    prime[1] = False

    for p in range(2, mt.ceil(n**(0.5))):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # greater than or equal to
            # the square of it numbers
            # which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, n + 1, p):
                prime[i] = False

# Utility function to check power of two
def isPowerOfTwo(n):
    return (n and (n & (n - 1)) == False)

# Function to check if the Given
# number is Proth number or not
def isProthNumber(n):

    k = 1
    while (k < (n // k)):

        # check if k divides n or not
        if (n % k == 0):

            # Check if n/k is power of 2 or not
            if (isPowerOfTwo(n // k)):
                return True

        # update k to next odd number
        k = k + 2

    # If we reach here means there
    # exists no value of K such
    # that k is odd number and n/k
    # is a power of 2 greater than k
    return False

# Function to check whether the given
# number is Proth Prime or Not.
def isProthPrime(n):

    # Check n for Proth Number
    if (isProthNumber(n - 1)):

        # if number is prime, return true
        if (prime[n]):
            return True
        else:
            return False

    else:
        return False

# Driver Code
n = 41

# if number is proth number,
# calculate primes upto n
SieveOfEratosthenes(n)

for i in range(1, n + 1):

    # Check n for Proth Prime
    if isProthPrime(i) == True:
        print(i)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static Boolean[] prime = new Boolean[1000000];

// Calculate all primes upto n.
static void SieveOfEratosthenes(int n)
{
    // Initialize all entries it as true.
    // A value in prime[i] will finally
    // false if i is Not a prime, else true.
    for (int i = 1; i <= n + 1; i++)
        prime[i] = true;

    prime[1] = false;

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // greater than or equal to
            // the square of it numbers
            // which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Utility function to check power of two
static Boolean isPowerOfTwo(int n)
{
    return (n > 0 && (n & (n - 1)) == 0);
}

// Function to check if the Given
// number is Proth number or not
static Boolean isProthNumber(int n)
{

    int k = 1;
    while (k < (int)(n / k))
    {

        // check if k divides n or not
        if (n % k == 0)
        {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo((int)(n / k)))
                return true;
        }

        // update k to next odd number
        k = k + 2;
    }

    // If we reach here means there
    // exists no value of K such
    // that k is odd number and n/k
    // is a power of 2 greater than k
    return false;
}

// Function to check whether the given
// number is Proth Prime or Not.
static Boolean isProthPrime(int n)
{
    // Check n for Proth Number
    if (isProthNumber(n - 1))
    {

        // if number is prime, return true
        if (prime[n])
            return true;
        else
            return false;
    }
    else
        return false;
}

// Driver Code
static public void Main(String []args)
{
    int n = 41;

    // if number is proth number,
    // calculate primes upto n
    SieveOfEratosthenes(n);

    for (int i = 1; i <= n; i++)

        // Check n for Proth Prime
        if (isProthPrime(i))
            Console.WriteLine(i);
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$GLOBALS['prime'] = array();

// Calculate all primes upto n.
function SieveOfEratosthenes($n)
{
    // Initialize all entries it as true.
    // A value in prime[i] will finally
    // false if i is Not a prime, else true.
    for ($i = 1; $i <= $n + 1; $i++)
        $GLOBALS['prime'][$i] = true;

    $GLOBALS['prime'][1] = false;

    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($GLOBALS['prime'][$p] == true)
        {

            // Update all multiples of p greater 
            // than or equal to the square of it 
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for ($i = $p * $p; $i <= $n; $i += $p)
                $GLOBALS['prime'][$i] = false;
        }
    }
}

// Utility function to check power of two
function isPowerOfTwo($n)
{
    return ($n && !($n & ($n - 1)));
}

// Function to check if the Given
// number is Proth number or not
function isProthNumber($n)
{
    $k = 1;
    while ($k < ($n / $k))
    {

        // check if k divides n or not
        if ($n % $k == 0)
        {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo($n / $k))
                return true;
        }

        // update k to next odd number
        $k = $k + 2;
    }

    // If we reach here means there
    // exists no value of K such
    // that k is odd number and n/k
    // is a power of 2 greater than k
    return false;
}

// Function to check whether the given
// number is Proth Prime or Not.
function isProthPrime($n)
{
    // Check n for Proth Number
    if (isProthNumber($n - 1))
    {

        // if number is prime, return true
        if ($GLOBALS['prime'][$n])
            return true;
        else
            return false;
    }
    else
        return false;
}

// Driver Code
$n = 41;

// if number is proth number,
// calculate primes upto n
SieveOfEratosthenes($n);

for ($i = 1; $i <= $n; $i++)

    // Check n for Proth Prime
    if (isProthPrime($i) == true)
        echo $i, "\n";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach
let prime = new Array();

// Calculate all primes upto n.
function SieveOfEratosthenes(n)
{
    // Initialize all entries it as true.
    // A value in prime[i] will finally
    // false if i is Not a prime, else true.
    for (let i = 1; i <= n + 1; i++)
        prime[i] = true;

    prime[1] = false;

    for (let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Utility function to check power of two
function isPowerOfTwo(n)
{
    return (n && !(n & (n - 1)));
}

// Function to check if the Given
// number is Proth number or not
function isProthNumber(n)
{
    let k = 1;
    while (k < (n / k))
    {

        // check if k divides n or not
        if (n % k == 0)
        {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo(n / k))
                return true;
        }

        // update k to next odd number
        k = k + 2;
    }

    // If we reach here means there
    // exists no value of K such
    // that k is odd number and n/k
    // is a power of 2 greater than k
    return false;
}

// Function to check whether the given
// number is Proth Prime or Not.
function isProthPrime(n)
{
    // Check n for Proth Number
    if (isProthNumber(n - 1))
    {

        // if number is prime, return true
        if (prime[n])
            return true;
        else
            return false;
    }
    else
        return false;
}

// Driver Code
let n = 41;

// if number is proth number,
// calculate primes upto n
SieveOfEratosthenes(n);

for (let i = 1; i <= n; i++)

    // Check n for Proth Prime
    if (isProthPrime(i) == true)
        document.write(i + "<br>");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
3
5
13
17
41
```

**时间复杂度:** O(n*log(log(n)))
**参考文献:**

*   https://en . Wikipedia . org/wiki/proth _ number # proth _ primes
*   [https://www . geesforgeks . org/program-to-check-a-number-is-pret-number-or-not/](https://www.geeksforgeeks.org/program-to-check-whether-a-number-is-proth-number-or-not/)