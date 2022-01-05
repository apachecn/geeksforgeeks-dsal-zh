# A 和 B 的倍数之和小于 N

> 原文:[https://www . geesforgeks . org/a 和 b 的倍数之和小于 n/](https://www.geeksforgeeks.org/sum-of-multiples-of-a-and-b-less-than-n/)

给定一个数 N，任务是求 N 以下所有 A 和 B 的倍数之和
**例:**

```
Input:N = 11, A= 8, B= 2
Output: Sum = 30
Multiples of 8 less than 11 is 8 only.
Multiples of 2 less than 11 is 2, 4, 6, 8, 10 and their sum is 30.
As 8 is common in both so it is counted only once.

Input: N = 100, A= 5, B= 10
Output: Sum = 950
```

**一种天真的方法**是通过 1 到进行迭代，找到 A 和 B 的倍数，并将其相加求和。循环结束时显示总和。
**高效进场:**由于 A 的倍数会形成 AP 系列 A、2a、3a……。
和 B 形成 AP 系列 B，2b，3b……
将这两个系列的和相加，我们将得到这两个数字的倍数之和，但可能有一些共同的倍数，因此通过减去 lcm(A，B)的倍数，从这两个系列的和中去除重复项。所以，减去 lcm(A，B)的级数。
所以 A 和 B 小于 N 的倍数之和为**和(A)+和(B)-和(lcm(A，B))** 。
以下是上述方法的实施:

## C++

```
// CPP program to find the sum of all
// multiples of A and B below N
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to find sum of AP series
ll sumAP(ll n, ll d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of A and B below N
ll sumMultiples(ll A, ll B, ll n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    // common factors of A and B
    ll common = (A * B) / __gcd(A, B);

    return sumAP(n, A) + sumAP(n, B) - sumAP(n, common);
}

// Driver code
int main()
{
    ll n = 100, A = 5, B = 10;

    cout << "Sum = " << sumMultiples(A, B, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// multiples of A and B below N

class GFG{

static int __gcd(int a, int b)
    {
      if (b == 0)
        return a;
      return __gcd(b, a % b); 
    }

// Function to find sum of AP series
static int sumAP(int n, int d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of A and B below N
static int sumMultiples(int A, int B, int n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    // common factors of A and B
    int common = (A * B) / __gcd(A,B);

    return sumAP(n, A) + sumAP(n, B) - sumAP(n, common);
}

// Driver code
public static void main(String[] args)
{
    int n = 100, A = 5, B = 10;

    System.out.println("Sum = "+sumMultiples(A, B, n));
}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find the sum of
# all multiples of A and B below N
from math import gcd,sqrt

# Function to find sum of AP series
def sumAP(n, d):

    # Number of terms
    n = int(n / d)

    return (n) * (1 + n) * d / 2

# Function to find the sum of all
# multiples of A and B below N
def sumMultiples(A, B, n):

    # Since, we need the sum of
    # multiples less than N
    n -= 1

    # common factors of A and B
    common = int((A * B) / gcd(A, B))

    return (sumAP(n, A) + sumAP(n, B) -
            sumAP(n, common))

# Driver code
if __name__ == '__main__':
    n = 100
    A = 5
    B = 10

    print("Sum =", int(sumMultiples(A, B, n)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the sum of all
// multiples of A and B below N

class GFG{

static int __gcd(int a, int b)
    {
    if (b == 0)
        return a;
    return __gcd(b, a % b);
    }

// Function to find sum of AP series
static int sumAP(int n, int d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of A and B below N
static int sumMultiples(int A, int B, int n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    // common factors of A and B
    int common = (A * B) / __gcd(A,B);

    return sumAP(n, A) + sumAP(n, B) - sumAP(n, common);
}

// Driver code
public static void Main()
{
    int n = 100, A = 5, B = 10;

    System.Console.WriteLine("Sum = "+sumMultiples(A, B, n));
}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// multiples of A and B below N
function __gcd($a,$b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// Function to find sum of AP series
function sumAP($n, $d)
{
    // Number of terms
    $n = (int)($n / $d);

    return ($n) * (1 + $n) * $d / 2;
}

// Function to find the sum of all
// multiples of A and B below N
function sumMultiples($A, $B, $n)
{
    // Since, we need the sum of
    // multiples less than N
    $n--;

    // common factors of A and B
    $common = (int)(($A * $B) /
               __gcd($A, $B));

    return sumAP($n, $A) +
           sumAP($n, $B) -
           sumAP($n, $common);
}

// Driver code
$n = 100;
$A = 5;
$B = 10;

echo "Sum = " . sumMultiples($A, $B, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript  program to find the sum of all
// multiples of A and B below N
function __gcd(a,b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to find sum of AP series
function sumAP(n, d)
{
    // Number of terms
    n = parseInt(n / d);

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of A and B below N
function sumMultiples(A, B, n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    // common factors of A and B
    common = parseInt((A * B) /
               __gcd(A, B));

    return sumAP(n, A) +
           sumAP(n, B) -
           sumAP(n, common);
}

// Driver code
let n = 100;
let A = 5;
let B = 10;

document.write( "Sum = " + sumMultiples(A, B, n));

// This code is contributed by bobby

</script>
```

**Output:** 

```
Sum = 950
```