# 生成满足给定条件的 N 个整数

> 原文:[https://www . geesforgeks . org/generate-n-integers-满足给定条件/](https://www.geeksforgeeks.org/generate-n-integers-satisfying-the-given-conditions/)

给定一个整数 **N** ，任务是生成一个大小为 **N** 的数组，其属性如下:

1.  没有两种元素会相互分裂。
2.  每个奇数子集都有一个奇数和，每个偶数子集都有一个偶数和。

**例:**

> **输入:** N = 3
> **输出:** 3 5 7
> 没有两个元素相互除，所有奇数子集{3}、{5}、{7}和{3，5，7}的和
> 都是奇数。
> 所有偶子集之和为偶，即{3，5}、{3，7}和{5，7}
> **输入:** N = 6
> **输出:** 3 5 7 11 13 17

**方法:**为了满足每个奇数子集有奇数和，偶数子集有偶数和的条件，每个元素必须是奇数，并且为了使任何两个元素不相互除，它们必须是素数。所以，现在的任务是找到前 N 个奇素数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 1000000

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the first
// n odd prime numbers
void solve(int n)
{
    // To store the current count
    // of prime numbers
    int count = 0;

    // Starting with 3 as 2 is
    // an even prime number
    for (int i = 3; count < n; i++) {

        // If i is prime
        if (prime[i]) {

            // Print i and increment count
            cout << i << " ";
            count++;
        }
    }
}

// Driver code
int main()
{
    // Create the sieve
    SieveOfEratosthenes();

    int n = 6;
    solve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 1000000;

// Create a boolean array "prime[0..n]" and
// initialize all entries it as true.
// A value in prime[i] will finally be false
// if i is Not a prime, else true.
static boolean []prime = new boolean[MAX + 1];
static void SieveOfEratosthenes()
{
    for (int i = 0; i <= MAX; i ++)
        prime[i] = true;

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the first
// n odd prime numbers
static void solve(int n)
{
    // To store the current count
    // of prime numbers
    int count = 0;

    // Starting with 3 as 2 is
    // an even prime number
    for (int i = 3; count < n; i++)
    {

        // If i is prime
        if (prime[i])
        {

            // Print i and increment count
            System.out.print(i + " ");
            count++;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // Create the sieve
    SieveOfEratosthenes();

    int n = 6;
    solve(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

MAX = 1000000

# Create a boolean array "prime[0..n]" and
# initialize all entries it as true.
# A value in prime[i] will finally be false
# if i is Not a prime, else true.
prime = [True] * (MAX + 1);

def SieveOfEratosthenes() :

    prime[1] = False;

    for p in range(2, int(sqrt(MAX)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Set all multiples of p to non-prime
            for i in range(p * 2, MAX + 1, p) :
                prime[i] = False;

# Function to find the first
# n odd prime numbers
def solve(n) :

    # To store the current count
    # of prime numbers
    count = 0;
    i = 3;

    # Starting with 3 as 2 is
    # an even prime number
    while count < n :

        # If i is prime
        if (prime[i]) :

            # Print i and increment count
            print(i, end = " ");
            count += 1;

        i += 1

# Driver code
if __name__ == "__main__" :

    # Create the sieve
    SieveOfEratosthenes();

    n = 6;
    solve(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int MAX = 1000000;

// Create a boolean array "prime[0..n]" and
// initialize all entries it as true.
// A value in prime[i] will finally be false
// if i is Not a prime, else true.
static bool []prime = new bool[MAX + 1];
static void SieveOfEratosthenes()
{
    for (int i = 0; i <= MAX; i ++)
        prime[i] = true;

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the first
// n odd prime numbers
static void solve(int n)
{
    // To store the current count
    // of prime numbers
    int count = 0;

    // Starting with 3 as 2 is
    // an even prime number
    for (int i = 3; count < n; i++)
    {

        // If i is prime
        if (prime[i])
        {

            // Print i and increment count
            Console.Write(i + " ");
            count++;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    // Create the sieve
    SieveOfEratosthenes();

    int n = 6;
    solve(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MAX = 1000000;

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
let prime = new Array(MAX + 1).fill(true);
function SieveOfEratosthenes()
{

    prime[1] = false;

    for (let p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (let i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the first
// n odd prime numbers
function solve(n)
{
    // To store the current count
    // of prime numbers
    let count = 0;

    // Starting with 3 as 2 is
    // an even prime number
    for (let i = 3; count < n; i++) {

        // If i is prime
        if (prime[i]) {

            // Print i and increment count
            document.write(i + " ");
            count++;
        }
    }
}

// Driver code
    // Create the sieve
    SieveOfEratosthenes();

    let n = 6;
    solve(n);

</script>
```

**Output:** 

```
3 5 7 11 13 17
```