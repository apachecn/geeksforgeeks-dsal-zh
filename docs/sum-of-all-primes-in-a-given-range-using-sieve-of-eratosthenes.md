# 使用厄拉多塞筛对给定范围内的所有素数求和

> 原文:[https://www . geeksforgeeks . org/给定范围内所有素数之和-使用埃拉托斯特尼筛/](https://www.geeksforgeeks.org/sum-of-all-primes-in-a-given-range-using-sieve-of-eratosthenes/)

给定一个范围[L，R]。任务是找出从 L 到 R(包括 L 和 R)给定范围内所有素数的和。
**例** :

```
Input : L = 10, R = 20
Output : Sum = 60
Prime numbers between [10, 20] are:
11, 13, 17, 19
Therefore, sum = 11 + 13 + 17 + 19 = 60

Input : L = 15, R = 25
Output : Sum = 59
```

A **简单解**是从 L 遍历到 R，检查当前数是否为质数。如果是，将其添加到![sum  ](img/3427faae84c28d40393dda8ea75359f3.png "Rendered by QuickLaTeX.com")。最后，打印总和。
一个**高效的解决方案**是使用厄拉多塞的[筛来查找给定限制内的所有素数。然后，计算一个前缀和数组来存储和，直到每个值都在极限之前。一旦我们有了前缀数组，我们只需要返回前缀[R]–前缀[L-1]。
**注**:前缀【I】将存储从 1 到![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")的所有素数之和。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find sum of primes
// in range L to R
#include <bits/stdc++.h>
using namespace std;

const int MAX = 10000;

// prefix[i] is going to store sum of primes
// till i (including i).
int prefix[MAX + 1];

// Function to build the prefix sum array
void buildPrefix()
{
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool prime[MAX + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // Build prefix array
    prefix[0] = prefix[1] = 0;
    for (int p = 2; p <= MAX; p++) {
        prefix[p] = prefix[p - 1];
        if (prime[p])
            prefix[p] += p;
    }
}

// Function to return sum of prime in range
int sumPrimeRange(int L, int R)
{
    buildPrefix();

    return prefix[R] - prefix[L - 1];
}

// Driver code
int main()
{
    int L = 10, R = 20;

    cout << sumPrimeRange(L, R) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of primes
// in range L to R

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static final int MAX = 10000;

// prefix[i] is going to store sum of primes
// till i (including i).
static int prefix[]=new int[MAX + 1];

// Function to build the prefix sum array
static void buildPrefix()
{
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[] = new boolean[MAX + 1];

    for(int i = 0; i < MAX+1; i++)
    prime[i] = true;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // Build prefix array
    prefix[0] = prefix[1] = 0;
    for (int p = 2; p <= MAX; p++) {
        prefix[p] = prefix[p - 1];
        if (prime[p] == true)
            prefix[p] += p;
    }
}

// Function to return sum of prime in range
static int sumPrimeRange(int L, int R)
{
    buildPrefix();

    return prefix[R] - prefix[L - 1];
}

// Driver code
public static void main(String args[])
{
    int L = 10, R = 20;

    System.out.println (sumPrimeRange(L, R));

}
}
```

## 蟒蛇 3

```
# Python 3 program to find sum of primes
# in range L to R
from math import sqrt

MAX = 10000

# prefix[i] is going to store sum of primes
# till i (including i).
prefix = [0 for i in range(MAX + 1)]

# Function to build the prefix sum array
def buildPrefix():

    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(MAX + 1)]

    for p in range(2,int(sqrt(MAX)) + 1, 1):

        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, MAX + 1, p):
                prime[i] = False

    # Build prefix array
    prefix[0] = 0
    prefix[1] = 0
    for p in range(2, MAX + 1, 1):
        prefix[p] = prefix[p - 1]
        if (prime[p]):
            prefix[p] += p

# Function to return sum of prime in range
def sumPrimeRange(L, R):
    buildPrefix()

    return prefix[R] - prefix[L - 1]

# Driver code
if __name__ == '__main__':
    L = 10
    R = 20
    print(sumPrimeRange(L, R))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum of
// primes in range L to R
using System;
class GFG
{

static int MAX = 10000;

// prefix[i] is going to
// store sum of primes
// till i (including i).
static int []prefix = new int[MAX + 1];

// Function to build the
// prefix sum array
static void buildPrefix()
{
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally
    // be false if i is Not a prime,
    // else true.
    bool []prime = new bool[MAX + 1];

    for(int i = 0; i < MAX+1; i++)
    prime[i] = true;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // Build prefix array
    prefix[0] = prefix[1] = 0;
    for (int p = 2; p <= MAX; p++)
    {
        prefix[p] = prefix[p - 1];
        if (prime[p] == true)
            prefix[p] += p;
    }
}

// Function to return sum
// of prime in range
static int sumPrimeRange(int L, int R)
{
    buildPrefix();

    return prefix[R] - prefix[L - 1];
}

// Driver code
public static void Main()
{
    int L = 10, R = 20;

    Console.WriteLine(sumPrimeRange(L, R));
}
}

// This code is contributed
// by anuj_67
```

## java 描述语言

```
<script>
// Jacascript program to find sum of primes

MAX = 10000;

// prefix[i] is going to store sum of primes
// till i (including i).
prefix = new Array(MAX + 1);

// Function to build the prefix sum array
function buildPrefix()
{
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    prime = new Array(MAX + 1);
    prime.fill(true);

    for (var p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // Build prefix array
    prefix[0] = prefix[1] = 0;
    for (var p = 2; p <= MAX; p++) {
        prefix[p] = prefix[p - 1];
        if (prime[p])
            prefix[p] += p;
    }
}

// Function to return sum of prime in range
function sumPrimeRange(L, R)
{
    buildPrefix();
    return prefix[R] - prefix[L - 1];
}

var L = 10, R = 20;
document.write( sumPrimeRange(L, R) + "<br>");

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
60
```