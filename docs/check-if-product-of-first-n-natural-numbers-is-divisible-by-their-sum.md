# 检查前 N 个自然数的乘积是否能被它们的和整除

> 原文:[https://www . geesforgeks . org/check-first-n-自然数的乘积是否可被其和除尽/](https://www.geeksforgeeks.org/check-if-product-of-first-n-natural-numbers-is-divisible-by-their-sum/)

给定一个整数 **N** ，任务是检查第一个 **N** 自然数的乘积是否能被第一个 **N** 自然数的和整除。
**举例:**

> **输入:** N = 3
> **输出:**是
> 积= 1 * 2 * 3 = 6
> 和= 1 + 2 + 3 = 6
> **输入:** N = 6
> **输出:**否

**天真法:**求第一个 **N 个**自然数的和与积，检查积是否能被和整除。
**高效进场:**我们知道第一个 **N 个**自然的和与积是**和=(N *(N+1))/2****积= N！**分别为。现在为了检查乘积是否能被和整除，我们需要检查下面等式的余数是否为 0。

> **N！/(N *(N+1)/2)**
> **2 *(N–1)！/ N + 1**
> 即 **(N + 1)** 的每个因子都应该在**(2 *(N–1)！)**。所以，如果 **(N + 1)** 是一个素数，那么我们可以肯定乘积不能被和整除。
> 所以最终只要检查 **(N + 1)** 是否为质数即可。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n is prime
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

// Function that return true if the product
// of the first n natural numbers is divisible
// by the sum of first n natural numbers
bool isDivisible(int n)
{
    if (isPrime(n + 1))
        return false;
    return true;
}

// Driver code
int main()
{
    int n = 6;
    if (isDivisible(n))
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

// Function that returns true if n is prime
static boolean isPrime(int n)
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

// Function that return true if the product
// of the first n natural numbers is divisible
// by the sum of first n natural numbers
static boolean isDivisible(int n)
{
    if (isPrime(n + 1))
        return false;
    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    if (isDivisible(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function that returns true if n is prime
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5, int(sqrt(n)) + 1, 6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function that return true if the product
# of the first n natural numbers is divisible
# by the sum of first n natural numbers
def isDivisible(n):
    if (isPrime(n + 1)):
        return False
    return True

# Driver code
if __name__ == '__main__':
    n = 6
    if (isDivisible(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if n is prime
static bool isPrime(int n)
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

// Function that return true if the product
// of the first n natural numbers is divisible
// by the sum of first n natural numbers
static bool isDivisible(int n)
{
    if (isPrime(n + 1))
        return false;
    return true;
}

// Driver code
static void Main()
{
    int n = 6;
    if (isDivisible(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if n is prime
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

// Function that return true if the product
// of the first n natural numbers is divisible
// by the sum of first n natural numbers
function isDivisible($n)
{
    if (isPrime($n + 1))
        return false;
    return true;
}

// Driver code
$n = 6;
if (isDivisible($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function that returns true if n is prime
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

    for (i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function that return true if the product
// of the first n natural numbers is divisible
// by the sum of first n natural numbers
function isDivisible(n)
{
    if (isPrime(n + 1))
        return false;
    return true;
}

// Driver code
var n = 6;
if (isDivisible(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
No
```