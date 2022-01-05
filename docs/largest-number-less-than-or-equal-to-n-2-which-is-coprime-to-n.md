# 小于或等于 N/2 的最大数值，与 N 互质

> 原文:[https://www . geesforgeks . org/最大数字小于或等于 n-2-哪是互素到 n/](https://www.geeksforgeeks.org/largest-number-less-than-or-equal-to-n-2-which-is-coprime-to-n/)

给定一个数 N，任务是找到小于或等于 N/2 的最大正整数，它是与 N 的互素。
**注:**如果 gcd(A，B) = 1，则两个数 A 和 B 被认为是互素的。也给出了 2 < N < 10^18.
**示例:**

```
Input: N = 50
Output: 23
GCD(50, 23) = 1 

Input: N = 100
Output: 49
```

**天真法:**从 N/2 开始，找出小于或等于 N/2 的数，这就是互素到 N.
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approacdh
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to calculate gcd of two number
ll gcd(ll a, ll b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to check if two numbers are coprime or not
bool coPrime(ll n1, ll n2)
{
    // two numbers are coprime if their gcd is 1
    if (gcd(n1, n2) == 1)
        return true;
    else
        return false;
}

// Function to find largest integer less
// than or equal to N/2 and coprime with N
ll largestCoprime(ll N)
{
    ll half = floor(N / 2);

    // Check one by one all numbers
    // less than or equal to N/2
    while (coPrime(N, half) == false)
        half--;

    return half;
}

// Driver code
int main()
{

    ll n = 50;
    cout << largestCoprime(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approacdh
import java.util.*;

class GFG
{

// Function to calculate gcd of two number
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to check if two
// numbers are coprime or not
static boolean coPrime(int n1, int n2)
{
    // two numbers are coprime
    // if their gcd is 1
    if (gcd(n1, n2) == 1)
        return true;
    else
        return false;
}

// Function to find largest integer less
// than or equal to N/2 and coprime with N
static int largestCoprime(int N)
{
    int half = (int)(N / 2);

    // Check one by one all numbers
    // less than or equal to N/2
    while (coPrime(N, half) == false)
        half--;

    return half;
}

// Driver code
public static void main(String args[])
{
    int n = 50;
    System.out.println(largestCoprime(n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the above approacdh
import math as mt

# Function to calculate gcd of two number
def gcd( a, b):

    if (b == 0):
        return a
    else:
        return gcd(b, a % b)

# Function to check if two numbers are coprime or not
def coPrime( n1, n2):

    # two numbers are coprime if their gcd is 1
    if (gcd(n1, n2) == 1):
        return True
    else:
        return False

# Function to find largest integer less
# than or equal to N/2 and coprime with N
def largestCoprime( N):

    half = mt.floor(N / 2)

    # Check one by one a numbers
    # less than or equal to N/2
    while (coPrime(N, half) == False):
        half -= 1

    return half

# Driver code

n = 50
print( largestCoprime(n))

#This code is contributed by Mohit kumar 29
```

## C#

```
// C# implementation of the above approacdh
using System;

class GFG
{

// Function to calculate gcd of two number
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to check if two
// numbers are coprime or not
static bool coPrime(int n1, int n2)
{
    // two numbers are coprime
    // if their gcd is 1
    if (gcd(n1, n2) == 1)
        return true;
    else
        return false;
}

// Function to find largest integer less
// than or equal to N/2 and coprime with N
static int largestCoprime(int N)
{
    int half = (int)(N / 2);

    // Check one by one all numbers
    // less than or equal to N/2
    while (coPrime(N, half) == false)
        half--;

    return half;
}

// Driver code
static void Main()
{
    int n = 50;
    Console.WriteLine(largestCoprime(n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to calculate gcd of two number
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    else
        return gcd($b, $a % $b);
}

// Function to check if two numbers
// are coprime or not
function coPrime($n1, $n2)
{
    // two numbers are coprime if
    // their gcd is 1
    if (gcd($n1, $n2) == 1)
        return true;
    else
        return false;
}

// Function to find largest integer less
// than or equal to N/2 and coprime with N
function largestCoprime($N)
{
    $half = floor($N / 2);

    // Check one by one all numbers
    // less than or equal to N/2
    while (coPrime($N, $half) == false)
        $half--;

    return $half;
}

// Driver code
$n = 50;
echo largestCoprime($n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
// Javascript implementation of the above approach

// Function to calculate gcd of two number
function gcd(a, b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to check if two numbers
// are coprime or not
function coPrime(n1, n2)
{
    // two numbers are coprime if
    // their gcd is 1
    if (gcd(n1, n2) == 1)
        return true;
    else
        return false;
}

// Function to find largest integer less
// than or equal to N/2 and coprime with N
function largestCoprime(N)
{
    let half = Math.floor(N / 2);

    // Check one by one all numbers
    // less than or equal to N/2
    while (coPrime(N, half) == false)
        half--;

    return half;
}

// Driver code
let n = 50;
document.write(largestCoprime(n));

// This code is contributed
// by gfgking
```

**Output:** 

```
23
```