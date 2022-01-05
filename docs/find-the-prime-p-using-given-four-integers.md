# 用给定的四个整数求素数 P

> 原文:[https://www . geesforgeks . org/find-the-prime-p-using-found-integer/](https://www.geeksforgeeks.org/find-the-prime-p-using-given-four-integers/)

给定四个整数 X，Y，X <sup>2</sup> %P，Y <sup>2</sup> %P，其中 P 为素数。任务是找到质数 P.
**注:**答案永远存在。
**示例:**

> **输入:** X = 3，XsqmodP = 0，Y = 5，YsqmodP = 1
> **输出:** 3
> 当 X = 3，x <sup>2</sup> = 9，9 模 P 为 0。所以 P 的可能值是 3
> 当 x = 5，x <sup>2</sup> = 25，25 模 P 为 1。所以 p 的可能值是 3
> **输入:** X = 4，XsqmodP = 1，Y = 5，YsqmodP = 0
> **输出:** 5

**方法:**
从上面的数字我们得到，

> x
> 2–xsqmodp = 0 mod p
> y<sup>2</sup>–ysqmodp = 0 mod p

现在从这两个方程中找出所有常见的质因数，并检查它是否满足原始方程，如果满足(其中一个将一直存在)，那么这就是答案。
以下是上述方法的实现:

## C++

```
// CPP program to possible prime number
#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool Prime(int n)
{
    for (int j = 2; j <= sqrt(n); j++)
        if (n % j == 0)
            return false;

    return true;
}

// Function to find possible prime number
int find_prime(int x, int xsqmodp , int y, int ysqmodp)
{

    int n = x*x - xsqmodp;
    int n1 = y*y - ysqmodp;

    // Find a possible prime number
    for (int j = 2; j <= max(sqrt(n), sqrt(n1)); j++)
    {
        if (n % j == 0 && (x * x) % j == xsqmodp &&
                  n1 % j == 0 && (y * y) % j == ysqmodp)
            if (Prime(j))
                return j;

        int j1 = n / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp
             && n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;

        j1 = n1 / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
                n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;
    }

    // Last condition
    if (n == n1)
        return n;
}

// Driver code
int main()
{
    int x = 3, xsqmodp = 0, y = 5, ysqmodp = 1;

    // Function call
    cout << find_prime(x, xsqmodp, y, ysqmodp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to possible prime number
import java.util.*;
class GFG
{

// Function to check if a
// number is prime or not
static boolean Prime(int n)
{
    for (int j = 2;
             j <= Math.sqrt(n); j++)
        if (n % j == 0)
            return false;

    return true;
}

// Function to find possible prime number
static int find_prime(int x, int xsqmodp ,
                      int y, int ysqmodp)
{
    int n = x * x - xsqmodp;
    int n1 = y * y - ysqmodp;

    // Find a possible prime number
    for (int j = 2;
             j <= Math.max(Math.sqrt(n),
                           Math.sqrt(n1)); j++)
    {
        if (n % j == 0 && (x * x) % j == xsqmodp &&
            n1 % j == 0 && (y * y) % j == ysqmodp)
            if (Prime(j))
                return j;

        int j1 = n / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
            n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;

        j1 = n1 / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
            n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;
    }

    // Last condition
    if (n == n1)
        return n;
    return Integer.MIN_VALUE;
}

// Driver code
public static void main(String[] args)
{
    int x = 3, xsqmodp = 0,
        y = 5, ysqmodp = 1;

    // Function call
    System.out.println(find_prime(x, xsqmodp,
                                  y, ysqmodp));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to possible prime number
from math import sqrt

# Function to check if a
# number is prime or not
def Prime(n):
    for j in range(2, int(sqrt(n)) + 1, 1):
        if (n % j == 0):
            return False

    return True

# Function to find possible prime number
def find_prime(x, xsqmodp, y, ysqmodp):
    n = x * x - xsqmodp
    n1 = y * y - ysqmodp

    # Find a possible prime number
    for j in range(2, max(int(sqrt(n)),
                          int(sqrt(n1))), 1):
        if (n % j == 0 and (x * x) % j == xsqmodp and
            n1 % j == 0 and (y * y) % j == ysqmodp):
            if (Prime(j)):
                return j

        j1 = n // j
        if (n % j1 == 0 and (x * x) % j1 == xsqmodp and
            n1 % j1 == 0 and (y * y) % j1 == ysqmodp):
            if (Prime(j1)):
                return j1

        j1 = n1 // j
        if (n % j1 == 0 and (x * x) % j1 == xsqmodp and
            n1 % j1 == 0 and (y * y) % j1 == ysqmodp):
            if (Prime(j1)):
                return j1

    # Last condition
    if (n == n1):
        return n

# Driver code
if __name__ == '__main__':
    x = 3
    xsqmodp = 0
    y = 5
    ysqmodp = 1

    # Function call
    print(find_prime(x, xsqmodp, y, ysqmodp))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to possible prime number
using System;

class GFG
{

// Function to check if a
// number is prime or not
static bool Prime(int n)
{
    for (int j = 2;
             j <= Math.Sqrt(n); j++)
        if (n % j == 0)
            return false;

    return true;
}

// Function to find possible prime number
static int find_prime(int x, int xsqmodp ,
                      int y, int ysqmodp)
{
    int n = x * x - xsqmodp;
    int n1 = y * y - ysqmodp;

    // Find a possible prime number
    for (int j = 2;
            j <= Math.Max(Math.Sqrt(n),
                          Math.Sqrt(n1)); j++)
    {
        if (n % j == 0 && (x * x) % j == xsqmodp &&
            n1 % j == 0 && (y * y) % j == ysqmodp)
            if (Prime(j))
                return j;

        int j1 = n / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
            n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;

        j1 = n1 / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
            n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;
    }

    // Last condition
    if (n == n1)
        return n;
    return int.MinValue;
}

// Driver code
public static void Main()
{
    int x = 3, xsqmodp = 0,
        y = 5, ysqmodp = 1;

    // Function call
    Console.WriteLine(find_prime(x, xsqmodp,
                                 y, ysqmodp));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// Javascript program to possible prime number

// Function to check if a
// number is prime or not
function Prime(n)
{
    for (let j = 2; j <= Math.sqrt(n); j++)
        if (n % j == 0)
            return false;

    return true;
}

// Function to find possible prime number
function find_prime(x, xsqmodp , y, ysqmodp)
{

    let n = x*x - xsqmodp;
    let n1 = y*y - ysqmodp;

    // Find a possible prime number
    for (let j = 2; j <= Math.max(Math.sqrt(n), Math.sqrt(n1)); j++)
    {
        if (n % j == 0 && (x * x) % j == xsqmodp &&
                  n1 % j == 0 && (y * y) % j == ysqmodp)
            if (Prime(j))
                return j;

        let j1 = parseInt(n / j);
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp
             && n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;

        j1 = n1 / j;
        if (n % j1 == 0 && (x * x) % j1 == xsqmodp &&
                n1 % j1 == 0 && (y * y) % j1 == ysqmodp)
            if (Prime(j1))
                return j1;
    }

    // Last condition
    if (n == n1)
        return n;
}

// Driver code
    let x = 3, xsqmodp = 0, y = 5, ysqmodp = 1;

    // Function call
    document.write(find_prime(x, xsqmodp, y, ysqmodp));

</script>
```

**Output:** 

```
3
```