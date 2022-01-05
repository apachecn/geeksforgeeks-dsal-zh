# 辉煌的数字

> 原文:[https://www.geeksforgeeks.org/brilliant-numbers/](https://www.geeksforgeeks.org/brilliant-numbers/)

**灿烂数**是一个数 **N** 是两个相同位数的素数的乘积。
少数辉煌的数字是:

> 4, 6, 9, 10, 14, 15, 21, 25, 35, 49….

### 检查 N 是否是一个聪明的数字

给定一个数字 **N** ，任务是检查 **N** 是否为**辉煌号**。如果 **N** 是辉煌号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 1711
> **输出:**是
> **说明:**
> 1711 = 29*59，29 和 59 都是两位数。
> **输入:** N = 16
> **输出:**否

**方法:**思路是利用厄拉多塞的[筛找出所有小于等于给定数 N 的素数。一旦我们有了一个告诉所有素数的数组，我们就可以遍历这个数组来找到一个给定乘积的对。我们将使用厄拉多塞的筛子找到给定产品](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的[两个质数，并检查这对质数是否具有相同的位数。
以下是上述方法的实现:](https://www.geeksforgeeks.org/find-two-distinct-prime-numbers-with-given-product/) 

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate all prime
// numbers less than n
bool SieveOfEratosthenes(int n,
                bool isPrime[])
{
    // Initialize all entries of
    // boolean array as true.
    // A value in isPrime[i]
    // will finally be false
    // if i is Not a prime
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= n; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to return the number
// of digits in a number
int countDigit(long long n)
{
    return floor(log10(n) + 1);
}

// Function to check if N is a
// Brilliant number
bool isBrilliant(int n)
{
    int flag = 0;

    // Generating primes using Sieve
    bool isPrime[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers
    // to find first pair
    for (int i = 2; i < n; i++) {
        int x = n / i;

        if (isPrime[i] &&
          isPrime[x] and x * i == n) {
            if (countDigit(i) == countDigit(x))
                return true;
        }
    }

    return false;
}

// Driver Code
int main()
{
    // Given Number
    int n = 1711;

    // Function Call
    if (isBrilliant(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
import java.util.*;
class GFG{

// Function to generate all prime
// numbers less than n
static void SieveOfEratosthenes(int n,
                    boolean isPrime[])
{
    // Initialize all entries of
    // boolean array as true.
    // A value in isPrime[i]
    // will finally be false
    // if i is Not a prime
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to return the number
// of digits in a number
static int countDigit(int n)
{
    int count = 0;
        while (n != 0)
        {
            n = n / 10;
            ++count;
        }
        return count;
}

// Function to check if N is a
// Brilliant number
static boolean isBrilliant(int n)
{
    int flag = 0;

    // Generating primes using Sieve
    boolean isPrime[] = new boolean[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers
    // to find first pair
    for (int i = 2; i < n; i++)
    {
        int x = n / i;

        if (isPrime[i] &&
        isPrime[x] && (x * i) == n)
        {
            if (countDigit(i) == countDigit(x))
                return true;
        }
    }
    return false;
}

// Driver Code
public static void main (String[] args)
{
    // Given Number
    int n = 1711;

    // Function Call
    if (isBrilliant(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import math

# Function to generate all prime
# numbers less than n
def SieveOfEratosthenes(n, isPrime):

    # Initialize all entries of 
    # boolean array as true. 
    # A value in isPrime[i] 
    # will finally be false 
    # if i is Not a prime
    isPrime[0] = isPrime[1] = False

    for i in range(2, n + 1, 1):
        isPrime[i] = True

    p = 2
    while(p * p <= n ):

        # If isPrime[p] is not changed, 
        # then it is a prime
        if (isPrime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                isPrime[i] = False

        p += 1

# Function to return the number
# of digits in a number
def countDigit(n):

    return math.floor(math.log10(n) + 1)

# Function to check if N is a
# Brilliant number
def isBrilliant(n):

    flag = 0

    # Generating primes using Sieve
    isPrime = [0] * (n + 1)
    SieveOfEratosthenes(n, isPrime)

    # Traversing all numbers
    # to find first pair
    for i in range(2, n, 1):
        x = n // i

        if (isPrime[i] and 
            isPrime[x] and x * i == n):
            if (countDigit(i) == countDigit(x)):
                return True   

    return False 

# Driver Code

# Given Number
n = 1711

# Function Call
if (isBrilliant(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to generate all prime
// numbers less than n
static void SieveOfEratosthenes(int n,
                       bool []isPrime)
{

    // Initialize all entries of
    // boolean array as true.
    // A value in isPrime[i]
    // will finally be false
    // if i is Not a prime
    isPrime[0] = isPrime[1] = false;
    for(int i = 2; i <= n; i++)
       isPrime[i] = true;

    for(int p = 2; p * p <= n; p++)
    {

       // If isPrime[p] is not changed,
       // then it is a prime
       if (isPrime[p] == true)
       {

           // Update all multiples of p
           for(int i = p * 2; i <= n; i += p)
              isPrime[i] = false;
       }
    }
}

// Function to return the number
// of digits in a number
static int countDigit(int n)
{
    int count = 0;
    while (n != 0)
    {
        n = n / 10;
        ++count;
    }
    return count;
}

// Function to check if N is a
// Brilliant number
static bool isBrilliant(int n)
{
    //int flag = 0;

    // Generating primes using Sieve
    bool []isPrime = new bool[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers
    // to find first pair
    for(int i = 2; i < n; i++)
    {
       int x = n / i;

       if (isPrime[i] &&
           isPrime[x] && (x * i) == n)
       {
           if (countDigit(i) == countDigit(x))
               return true;
       }
    }
    return false;
}

// Driver Code
public static void Main()
{
    // Given Number
    int n = 1711;

    // Function Call
    if (isBrilliant(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation for the
// above approach

    // Function to generate all prime
    // numbers less than n
    function SieveOfEratosthenes( n, isPrime) {
        // Initialize all entries of
        // let array as true.
        // A value in isPrime[i]
        // will finally be false
        // if i is Not a prime
        isPrime[0] = isPrime[1] = false;
        for ( let i = 2; i <= n; i++)
            isPrime[i] = true;

        for (let  p = 2; p * p <= n; p++) {

            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true) {

                // Update all multiples of p
                for (let  i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Function to return the number
    // of digits in a number
    function countDigit( n) {
        let count = 0;
        while (n != 0) {
            n = parseInt(n / 10);
            ++count;
        }
        return count;
    }

    // Function to check if N is a
    // Brilliant number
    function isBrilliant( n) {
        let flag = 0;

        // Generating primes using Sieve
        let isPrime = Array(n + 1).fill(true);
        SieveOfEratosthenes(n, isPrime);

        // Traversing all numbers
        // to find first pair
        for ( let i = 2; i < n; i++) {
            let x = n / i;

            if (isPrime[i] && isPrime[x] && (x * i) == n) {
                if (countDigit(i) == countDigit(x))
                    return true;
            }
        }
        return false;
    }

    // Driver Code

        // Given Number
        let n = 1711;

        // Function Call
        if (isBrilliant(n))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(n)*

***辅助空间:** O(n)*

**参考:**T2http://oeis.org/A078972