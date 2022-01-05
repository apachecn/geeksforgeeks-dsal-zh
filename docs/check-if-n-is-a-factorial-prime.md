# 检查 N 是否是阶乘素数

> 原文:[https://www . geesforgeks . org/check-if-n-is-factorial-prime/](https://www.geeksforgeeks.org/check-if-n-is-a-factorial-prime/)

给定一个正整数 **N** ，任务是检查 **N** 是否为[阶乘素数](https://en.wikipedia.org/wiki/Factorial_prime)。如果是阶乘素数，则打印**是**否则打印**否**。
**注:**在数学中，阶乘素数是一个比任意数的[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)少一或多一的[素数](https://www.geeksforgeeks.org/prime-numbers/)。前几个阶乘素数是 **2，3，5，7，23，719，5039，…** 。
**例:**

> **输入:** N = 23
> **输出:** YES
> 23 是一个质数，比 4 (4！= 24).
> **输入:** 11
> **输出:** NO
> 11 是素数但也不能表示为 n！+ 1 或 n！– 1.

**方法:**为了使 **N** 成为阶乘数， **N** 必须是素数，并且**N–1**或 **N + 1** 应该是任意数的阶乘值。

*   如果 **N** 不是质数，则打印 **No** 。
*   否则设置**事实= 1** 并从 **i = 1** 开始更新**事实=事实* i** ，如果**事实= N–1**或**事实= N + 1** 则打印**是**。
*   重复上述步骤，直到**事实≤ N + 1** ，如果条件不满足，则最终打印**否**。

以下是上述方法的实现:

## C++

```
// C++ program to check if given
// number is a factorial prime

#include <bits/stdc++.h>
using namespace std;

// Utility function to check
// if a number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function that returns true if n is a factorial prime
bool isFactorialPrime(long n)
{

    // If n is not prime then return false
    if (!isPrime(n))
        return false;

    long fact = 1;
    int i = 1;
    while (fact <= n + 1) {

        // Calculate factorial
        fact = fact * i;

        // If n is a factorial prime
        if (n + 1 == fact || n - 1 == fact)
            return true;

        i++;
    }

    // n is not a factorial prime
    return false;
}

// Driver code
int main()
{

    int n = 23;

    if (isFactorialPrime(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given
// number is a factorial prime
class GFG {

    // Utility function to check
    // if a number is prime or not
    static boolean isPrime(long n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function that returns true if n is a factorial prime
    static boolean isFactorialPrime(long n)
    {

        // If n is not prime then return false
        if (!isPrime(n))
            return false;

        long fact = 1;
        int i = 1;
        while (fact <= n + 1) {

            // Calculate factorial
            fact = fact * i;

            // If n is a factorial prime
            if (n + 1 == fact || n - 1 == fact)
                return true;

            i++;
        }

        // n is not a factorial prime
        return false;
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 23;

        if (isFactorialPrime(n))
            System.out.println("Yes");

        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if given
# number is a factorial prime

# from math lib import sqrt function
from math import sqrt

# Utility function to check
# if a number is prime or not
def isPrime(n) :

    # Corner cases
    if (n <= 1) :
        return False

    if (n <= 3) :
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0) :
        return False

    for i in range(5, int(sqrt(n)) + 1, 6) :
        if (n % i == 0 or n % (i + 2) == 0) :
            return False

    return True

# Function that returns true if n
# is a factorial prime
def isFactorialPrime(n) :

    # If n is not prime then return false
    if (not isPrime(n)) :
        return False

    fact = 1
    i = 1
    while (fact <= n + 1) :

        # Calculate factorial
        fact = fact * i

        # If n is a factorial prime
        if (n + 1 == fact or n - 1 == fact) :
            return True

        i += 1

    # n is not a factorial prime
    return False

# Driver code
if __name__ == "__main__" :

    n = 23

    if (isFactorialPrime(n)) :
        print("Yes")
    else :
        print("No")

# This code is contributed by Ryuga
```

## C#

```
// C# program to check if given
// number is a factorial prime
using System;
class GFG {

    // Utility function to check
    // if a number is prime or not
    static bool isPrime(long n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function that returns true if n is a factorial prime
    static bool isFactorialPrime(long n)
    {

        // If n is not prime then return false
        if (!isPrime(n))
            return false;

        long fact = 1;
        int i = 1;
        while (fact <= n + 1) {

            // Calculate factorial
            fact = fact * i;

            // If n is a factorial prime
            if (n + 1 == fact || n - 1 == fact)
                return true;

            i++;
        }

        // n is not a factorial prime
        return false;
    }

    // Driver code
    public static void Main()
    {

        int n = 23;

        if (isFactorialPrime(n))
            Console.WriteLine("Yes");

        else
            Console.WriteLine("No");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if given number
// is a factorial prime

// Utility function to check if a
// number is prime or not
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

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
            return false;

    return true;
}

// Function that returns true if
// n is a factorial prime
function isFactorialPrime($n)
{

    // If n is not prime then return false
    if (!isPrime($n))
        return false;

    $fact = 1;
    $i = 1;
    while ($fact <= $n + 1)
    {

        // Calculate factorial
        $fact = $fact * $i;

        // If n is a factorial prime
        if ($n + 1 == $fact || $n - 1 == $fact)
            return true;

        $i++;
    }

    // n is not a factorial prime
    return false;
}

// Driver code
$n = 23;

if (isFactorialPrime($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
// Javascript program to check if given number
// is a factorial prime

// Utility function to check if a
// number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function that returns true if
// n is a factorial prime
function isFactorialPrime(n)
{

    // If n is not prime then return false
    if (!isPrime(n))
        return false;

    let fact = 1;
    let i = 1;
    while (fact <= n + 1)
    {

        // Calculate factorial
        fact = fact * i;

        // If n is a factorial prime
        if (n + 1 == fact || n - 1 == fact)
            return true;

        i++;
    }

    // n is not a factorial prime
    return false;
}

// Driver code
let n = 23;

if (isFactorialPrime(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by gfgking
```

**Output:** 

```
Yes
```