# 检查一个数是否是欧拉伪素数

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-Euler-伪素数/](https://www.geeksforgeeks.org/check-if-a-number-is-euler-pseudoprime/)

给定一个整数 **N** 和一个基数 **A** ，任务是检查 **N** 是否是给定基数 **A** 的[欧拉伪素数](https://en.wikipedia.org/wiki/Euler_pseudoprime)。
一个整数 **N** 被称为欧拉伪素数到基数 **A** ，如果

1.  **A > 0** 和 **N** 为奇数复合数。
2.  **A** 和 **N** 为同素，即 **GCD(A，N) = 1** 。
3.  **A<sup>(N–1)/2</sup>% N**不是 **1** 就是**N–1**。

**例:**

> **输入:** N = 121，A = 3
> **输出:**是
> **输入:** N = 343，A = 2
> **输出:**否

**方法:**检查欧拉伪素数的所有给定条件。如果任一条件不成立，则打印否，否则打印是。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n is composite
bool isComposite(int n)
{
    // Check if there is any divisor of n.
    // we only need check divisor till sqrt(n)
    // because if there is divisor which is greater
    // than sqrt(n) then there must be a divisor
    // which is less than sqrt(n)
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return true;
    }
    return false;
}

// Iterative Function to calculate
// (x^y) % p in O(log y)
int Power(int x, int y, int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is greater
    // than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1) {
            res = (res * x) % p;
        }

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function that returns true if N is
// Euler Pseudoprime to the base A
bool isEulerPseudoprime(int N, int A)
{

    // Invalid base
    if (A <= 0)
        return false;

    // N is not a composite odd number
    if (N % 2 == 0 || !isComposite(N))
        return false;

    // If A and N are not coprime
    if (__gcd(A, N) != 1)
        return false;

    int mod = Power(A, (N - 1) / 2, N);
    if (mod != 1 && mod != N - 1)
        return false;

    // All the conditions for Euler
    // Pseudoprime are satisfied
    return true;
}

// Driver code
int main()
{

    int N = 121, A = 3;

    if (isEulerPseudoprime(N, A))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if n is composite
static boolean isComposite(int n)
{
    // Check if there is any divisor of n.
    // we only need check divisor till sqrt(n)
    // because if there is divisor which is greater
    // than sqrt(n) then there must be a divisor
    // which is less than sqrt(n)
    for (int i = 2; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
            return true;
    }
    return false;
}

// Iterative Function to calculate
// (x^y) % p in O(log y)
static int Power(int x, int y, int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is greater
    // than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y % 2 == 1)
        {
            res = (res * x) % p;
        }

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function that returns true if N is
// Euler Pseudoprime to the base A
static boolean isEulerPseudoprime(int N, int A)
{

    // Invalid base
    if (A <= 0)
        return false;

    // N is not a composite odd number
    if (N % 2 == 0 || !isComposite(N))
        return false;

    // If A and N are not coprime
    if (__gcd(A, N) != 1)
        return false;

    int mod = Power(A, (N - 1) / 2, N);
    if (mod != 1 && mod != N - 1)
        return false;

    // All the conditions for Euler
    // Pseudoprime are satisfied
    return true;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver code
public static void main(String []args)
{
    int N = 121, A = 3;

    if (isEulerPseudoprime(N, A))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for nth Fuss–Catalan Number
from math import gcd, sqrt

# Function that returns true if n is composite
def isComposite(n) :

    # Check if there is any divisor of n.
    # we only need check divisor till sqrt(n)
    # because if there is divisor which is greater
    # than sqrt(n) then there must be a divisor
    # which is less than sqrt(n)
    for i in range(2, int(sqrt(n)) + 1) :
        if (n % i == 0) :
            return True;

    return False;

# Iterative Function to calculate
# (x^y) % p in O(log y)
def Power(x, y, p) :

    # Initialize result
    res = 1;

    # Update x if it is greater
    # than or equal to p
    x = x % p;

    while (y > 0) :

        # If y is odd, multiply x with result
        if (y & 1) :
            res = (res * x) % p;

        # y must be even now
        y = y >> 1; # y = y/2
        x = (x * x) % p;

    return res;

# Function that returns true if N is
# Euler Pseudoprime to the base A
def isEulerPseudoprime(N, A) :

    # Invalid base
    if (A <= 0) :
        return False;

    # N is not a composite odd number
    if (N % 2 == 0 or not isComposite(N)) :
        return False;

    # If A and N are not coprime
    if (gcd(A, N) != 1) :
        return false;

    mod = Power(A, (N - 1) // 2, N);
    if (mod != 1 and mod != N - 1) :
        return False;

    # All the conditions for Euler
    # Pseudoprime are satisfied
    return True;

# Driver code
if __name__ == "__main__" :

    N = 121; A = 3;

    if (isEulerPseudoprime(N, A)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if n is composite
static bool isComposite(int n)
{
    // Check if there is any divisor of n.
    // we only need check divisor till sqrt(n)
    // because if there is divisor which is greater
    // than sqrt(n) then there must be a divisor
    // which is less than sqrt(n)
    for (int i = 2; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
            return true;
    }
    return false;
}

// Iterative Function to calculate
// (x^y) % p in O(log y)
static int Power(int x, int y, int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is greater
    // than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y % 2 == 1)
        {
            res = (res * x) % p;
        }

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function that returns true if N is
// Euler Pseudoprime to the base A
static bool isEulerPseudoprime(int N, int A)
{

    // Invalid base
    if (A <= 0)
        return false;

    // N is not a composite odd number
    if (N % 2 == 0 || !isComposite(N))
        return false;

    // If A and N are not coprime
    if (__gcd(A, N) != 1)
        return false;

    int mod = Power(A, (N - 1) / 2, N);
    if (mod != 1 && mod != N - 1)
        return false;

    // All the conditions for Euler
    // Pseudoprime are satisfied
    return true;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver code
public static void Main(String []args)
{
    int N = 121, A = 3;

    if (isEulerPseudoprime(N, A))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if n is composite
function isComposite(n)
{
    // Check if there is any divisor of n.
    // we only need check divisor till sqrt(n)
    // because if there is divisor which is greater
    // than sqrt(n) then there must be a divisor
    // which is less than sqrt(n)
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0)
            return true;
    }
    return false;
}

// Iterative Function to calculate
// (x^y) % p in O(log y)
function Power(x, y, p) {

    // Initialize result
    let res = 1;

    // Update x if it is greater
    // than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1) {
            res = (res * x) % p;
        }

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

function __gcd(a, b) {
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function that returns true if N is
// Euler Pseudoprime to the base A
function isEulerPseudoprime(N, A) {

    // Invalid base
    if (A <= 0)
        return false;

    // N is not a composite odd number
    if (N % 2 == 0 || !isComposite(N))
        return false;

    // If A and N are not coprime
    if (__gcd(A, N) != 1)
        return false;

    let mod = Power(A, (N - 1) / 2, N);
    if (mod != 1 && mod != N - 1)
        return false;

    // All the conditions for Euler
    // Pseudoprime are satisfied
    return true;
}

// Driver code

let N = 121, A = 3;

if (isEulerPseudoprime(N, A))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(sqrt(N))