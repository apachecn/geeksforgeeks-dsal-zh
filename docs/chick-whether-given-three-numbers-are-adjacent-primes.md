# 检查给定的三个数是否为相邻素数

> 原文:[https://www . geesforgeks . org/chick-不管给定的三个数字是否是相邻的素数/](https://www.geeksforgeeks.org/chick-whether-given-three-numbers-are-adjacent-primes/)

给定三个数字，检查它们是否相邻，素数不是。如果三个素数之间没有素数，则称它们为相邻素数。
**例:**

```
Input : 2, 3, 5
Output : Yes
Explanation: 2, 3, 5 are adjacent primes.

Input : 11, 13, 19
Output : No
Explanation: 11, 13, 19 are not adjacent primes. 
Because there exits 17 between 13 and 19 which 
is prime.  
```

**方法:**
我们已经知道什么是[素数](https://www.geeksforgeeks.org/prime-numbers/)。在这里，我们需要检查三个数字是否是相邻的素数。首先，我们检查给定的三个数字是否为质数。之后我们会找到第一个数和第二个数的下一个素数。如果满足相邻素数的条件，那么很明显，给定的三个数是相邻素数，否则不是。

## C++

```
// CPP program to check given three numbers are
// primes are not.

#include <bits/stdc++.h>
using namespace std;

// checks weather given number is prime or not.
bool isPrime(int n)
{
    // check if n is a multiple of 2
    if (n % 2 == 0)
        return false;

    // if not, then just check the odds
    for (int i = 3; i * i <= n; i += 2)
        if (n % i == 0)
            return false;   
    return true;
}

// return next prime number
int nextPrime(int start)
{
    // start with next number.
    int next = start + 1;

    // breaks after finding next prime number
    while (!isPrime(next))
        next++;

    return next;
}

// check given three numbers are adjacent primes are not.
bool areAdjacentPrimes(int a, int b, int c)
{
    // check given three numbers are primes are not.
    if (!isPrime(a) || !isPrime(b) || !isPrime(c))
        return false;

    // find next prime of a
    int next = nextPrime(a);

    // If next is not same as 'a'
    if (next != b)
        return false;

    // If next next is not same as 'c'
    if (nextPrime(b) != c)
        return false;

    return true;
}

// Driver code for above functions
int main()
{
    if (areAdjacentPrimes(11, 13, 19))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check given three numbers are
// primes are not.

import java.io.*;
import java.util.*;

class GFG
{
    public static boolean isPrime(int n)
    {
        // check if n is a multiple of 2
        if (n % 2 == 0)
            return false;

        // if not, then just check the odds
        for (int i = 3; i * i <= n; i += 2)
            if (n % i == 0)
                return false;
        return true;
    }

    // return next prime number
    public static int nextPrime(int start)
    {
        // start with next number.
        int next = start + 1;

        // breaks after finding next prime number
        while (!isPrime(next))
            next++;

        return next;
    }

    // check given three numbers are adjacent primes are not.
    public static boolean areAdjacentPrimes(int a, int b, int c)
    {
        // check given three numbers are primes are not.
        if (!isPrime(a) || !isPrime(b) || !isPrime(c))
            return false;

        // find next prime of a
        int next = nextPrime(a);

        // If next is not same as 'a'
        if (next != b)
            return false;

        // If next next is not same as 'c'
        if (nextPrime(b) != c)
            return false;

        return true;
    }

    // Driver code for above functions
    public static void main (String[] args)
    {
        if (areAdjacentPrimes(11, 13, 19))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
// Mohit Gupta_OMG <(o_0)>
```

## 计算机编程语言

```
# Python3 program to check given 
# three numbers are primes are not.

# Function checks whether given number is prime or not.
def isPrime(n) :
    # Check if n is a multiple of 2
    if (n % 2 == 0) :
        return False

    # If not, then just check the odds
    i = 3
    while( i*i <= n) :
        if (n % i == 0) :
            return False
        i = i + 2
    return True

# Return next prime number
def nextPrime(start) :
    # Start with next number
    nxt = start + 1

    # Breaks after finding next prime number
    while (isPrime(nxt) == False) :
        nxt = nxt + 1

    return nxt

# Check given three numbers
# are adjacent primes are not
def areAdjacentPrimes(a, b, c) :
    # Check given three numbers are primes are not
    if (isPrime(a) == False or isPrime(b) == False
                            or isPrime(c) == False) :
        return False

    # Find next prime of a
    nxt = nextPrime(a)

    # If next is not same as 'a'
    if (nxt != b) :
        return False

    # If next next is not same as 'c'
    if (nextPrime(b) != c) :
        return False

    return True

# Driver code for above functions
if (areAdjacentPrimes(11, 13, 19)) :
    print( "Yes"),
else :
    print( "No")

#This code is contributed by NIKITA TIWARI.
```

## C#

```
// Java program to check given three numbers are
// primes are not.
using System;

class GFG
{
    public static bool isPrime(int n)
    {
        // check if n is a multiple of 2
        if (n % 2 == 0)
            return false;

        // if not, then just check the odds
        for (int i = 3; i * i <= n; i += 2)
            if (n % i == 0)
                return false;
        return true;
    }

    // return next prime number
    public static int nextPrime(int start)
    {
        // start with next number.
        int next = start + 1;

        // breaks after finding next prime number
        while (!isPrime(next))
            next++;

        return next;
    }

    // check given three numbers are adjacent primes are not.
    public static bool areAdjacentPrimes(int a, int b, int c)
    {
        // check given three numbers are primes are not.
        if (!isPrime(a) || !isPrime(b) || !isPrime(c))
            return false;

        // find next prime of a
        int next = nextPrime(a);

        // If next is not same as 'a'
        if (next != b)
            return false;

        // If next next is not same as 'c'
        if (nextPrime(b) != c)
            return false;

        return true;
    }

    // Driver code
    public static void Main ()
    {
        if (areAdjacentPrimes(11, 13, 19))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check given
// three numbers are primes or not.

// checks weather given
// number is prime or not.
function isPrime($n)
{
    // check if n is
    // a multiple of 2
    if ($n % 2 == 0)
        return false;

    // if not, then just
    // check the odds
    for ($i = 3; $i * $i <= $n; $i += 2)
        if ($n % $i == 0)
            return false;
    return true;
}

// return next prime number
function nextPrime($start)
{
    // start with next number.
    $next = $start + 1;

    // breaks after finding
    // next prime number
    while (!isPrime($next))
        $next++;

    return $next;
}

// check given three numbers
// are adjacent primes are not.
function areAdjacentPrimes($a, $b, $c)
{
    // check given three numbers
    // are primes are not.
    if (!isPrime($a) || !isPrime($b) ||
                        !isPrime($c))
        return false;

    // find next prime of a
    $next = nextPrime($a);

    // If next is not same as 'a'
    if ($next != $b)
        return false;

    // If next next is
    // not same as 'c'
    if (nextPrime($b) != $c)
        return false;

    return true;
}

// Driver code
if (areAdjacentPrimes(11, 13, 19))
    echo "Yes";
else
    echo "No";

// This article is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check given
// three numbers are
// primes are not.

    function isPrime(n)
    {
        // check if n is a multiple of 2
        if (n % 2 == 0)
            return false;

        // if not, then just check the odds
        for (let i = 3; i * i <= n; i += 2)
            if (n % i == 0)
                return false;
        return true;
    }

    // return next prime number
    function nextPrime(start)
    {
        // start with next number.
        let next = start + 1;

        // breaks after finding next prime number
        while (!isPrime(next))
            next++;

        return next;
    }

    // check given three numbers are
    // adjacent primes are not.
    function areAdjacentPrimes(a, b, c)
    {
        // check given three numbers are primes are not.
        if (!isPrime(a) || !isPrime(b) || !isPrime(c))
            return false;

        // find next prime of a
        let next = nextPrime(a);

        // If next is not same as 'a'
        if (next != b)
            return false;

        // If next next is not same as 'c'
        if (nextPrime(b) != c)
            return false;

        return true;
    }

// Driver code

        if (areAdjacentPrimes(11, 13, 19))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
No
```