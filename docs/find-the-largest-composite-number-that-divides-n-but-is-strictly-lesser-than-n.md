# 求除 N 但严格小于 N 的最大合成数

> 原文:[https://www . geeksforgeeks . org/find-最大复合数除以 n-但严格来说小于 n/](https://www.geeksforgeeks.org/find-the-largest-composite-number-that-divides-n-but-is-strictly-lesser-than-n/)

给定一个复合数 **N** ，任务是找到除 **N** 且严格小于 **N** 的最大复合数。如果没有这样的号码存在打印-1。
**举例:**

> **输入:** N = 16
> **输出:** 8
> **说明:**
> 所有除 16 的数都是{ 1，2，4，8，16 }
> 其中 8 是除 16 的最大合成数(小于 16)。
> **输入:** N = 100
> **输出:** -1

**逼近:**
由于 **N** 是一个复合数，因此 **N** 可以是两个数的乘积，一个是[素数](https://www.geeksforgeeks.org/prime-numbers/)，另一个是复合数，如果我们找不到 **N** 这样的一对，那么小于 **N** 的最大复合数除以 **N** 就不存在了。
求最大的合成数求最小的[质数](https://www.geeksforgeeks.org/prime-numbers/)(说一个)除 **N** 。那么除以 **N** 且小于 **N** 的最大合成数可以由 **(N/a)** 给出。
以下是步骤:

1.  找到 **N** 的最小[素数](https://www.geeksforgeeks.org/prime-numbers/)(说一个)。
2.  检查**(不适用)**是否为质数。如果是，那么我们找不到最大的合成数。
3.  否则 **(N/a)** 是除 **N** 且小于 **N** 的最大合成数。

以下是上述方法的实现:

## C++

```
// C++ program to find the largest
// composite number that divides
// N which is less than N
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// a number is prime or not
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function that find the largest
// composite number which divides
// N and less than N
int getSmallestPrimefactor(int n)
{
    // Find the prime number
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return i;
    }
}

// Driver's Code
int main()
{
    int N = 100;
    int a;

    // Get the smallest prime
    // factor
    a = getSmallestPrimefactor(N);

    // Check if (N/a) is prime
    // or not
    // If Yes print "-1"
    if (isPrime(N / a)) {
        cout << "-1";
    }

    // Else print largest composite
    // number (N/a)
    else {
        cout << N / a;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// composite number that divides
// N which is less than N
import java.util.*;

class GFG{

// Function to check whether
// a number is prime or not
static boolean isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for(int i = 2; i < n; i++)
    {
       if (n % i == 0)
           return false;
    }
    return true;
}

// Function that find the largest
// composite number which divides
// N and less than N
static int getSmallestPrimefactor(int n)
{

    // Find the prime number
    for(int i = 2; i <= Math.sqrt(n); i++)
    {
       if (n % i == 0)
           return i;
    }
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;
    int a;

    // Get the smallest prime
    // factor
    a = getSmallestPrimefactor(N);

    // Check if (N/a) is prime or
    // not. If Yes print "-1"
    if (isPrime(N / a))
    {
        System.out.print("-1");
    }

    // Else print largest composite
    // number (N/a)
    else
    {
        System.out.print(N / a);
    }
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to find the largest
# composite number that divides
# N which is less than N
import math

# Function to check whether
# a number is prime or not
def isPrime(n):

    # Corner case
    if (n <= 1):
        return False;

    # Check from 2 to n-1
    for i in range(2, n):
        if (n % i == 0):
            return False;

    return True;

# Function that find the largest
# composite number which divides
# N and less than N
def getSmallestPrimefactor(n):

    # Find the prime number
    for i in range(2, (int)(math.sqrt(n) + 1)):
        if (n % i == 0):
            return i;

    return -1

# Driver Code
N = 100;

# Get the smallest prime
# factor
a = getSmallestPrimefactor(N);

# Check if (N/a) is prime
# or not. If Yes print "-1"
if ((isPrime((int)(N / a)))):
    print(-1)

# Else print largest composite
# number (N/a)
else:
    print((int)(N / a));

# This code is contributed by grand_master   
```

## C#

```
// C# program to find the largest
// composite number that divides
// N which is less than N
using System;
class GFG{

// Function to check whether
// a number is prime or not
static bool isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for(int i = 2; i < n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function that find the largest
// composite number which divides
// N and less than N
static int getSmallestPrimefactor(int n)
{

    // Find the prime number
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
            return i;
    }
    return -1;
}

// Driver Code
public static void Main()
{
    int N = 100;
    int a;

    // Get the smallest prime
    // factor
    a = getSmallestPrimefactor(N);

    // Check if (N/a) is prime or
    // not. If Yes print "-1"
    if (isPrime(N / a))
    {
        Console.Write("-1");
    }

    // Else print largest composite
    // number (N/a)
    else
    {
        Console.Write(N / a);
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the largest
// composite number that divides
// N which is less than N

// Function to check whether
// a number is prime or not
function isPrime(n)
{
    // Corner case
    if (n <= 1)
        return false;

    var i;
    // Check from 2 to n-1
    for (i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function that find the largest
// composite number which divides
// N and less than N
function getSmallestPrimefactor(n)
{
     var i;
    // Find the prime number
    for (i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0)
            return i;
    }
}

// Driver's Code

    var N = 100;
    var a;

    // Get the smallest prime
    // factor
    a = getSmallestPrimefactor(N);

    // Check if (N/a) is prime
    // or not
    // If Yes print "-1"
    if (isPrime(N / a))
        document.write("-1");

    // Else print largest composite
    // number (N/a)
    else
        document.write(N/a);

</script>
```

**Output:** 

```
50
```

**时间复杂度:** O(sqrt(N))