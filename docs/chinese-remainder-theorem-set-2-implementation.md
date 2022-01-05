# 中国剩余定理|集合 2(基于逆模的实现)

> 原文:[https://www . geesforgeks . org/Chinese-余数-定理-集合-2-实现/](https://www.geeksforgeeks.org/chinese-remainder-theorem-set-2-implementation/)

给我们两个数组 num[0..k-1]和 rem[0..k-1]。在 num[0..k-1]，每对都是互质的(每对的 gcd 为 1)。我们需要找到最小正数 x，这样:

```
     x % num[0]    =  rem[0], 
     x % num[1]    =  rem[1], 
     .......................
     x % num[k-1]  =  rem[k-1]
```

**示例:**

```
Input:  num[] = {3, 4, 5}, rem[] = {2, 3, 1}
Output: 11
Explanation: 
11 is the smallest number such that:
  (1) When we divide it by 3, we get remainder 2\. 
  (2) When we divide it by 4, we get remainder 3.
  (3) When we divide it by 5, we get remainder 1.
```

我们强烈建议将以下帖子作为先决条件。

[中国剩余定理|集合 1(引言)](https://www.geeksforgeeks.org/chinese-remainder-theorem-set-1-introduction/)
我们讨论了一个求最小 x 的朴素解法，本文讨论了一个求 x 的有效解法。
解决方案基于以下公式。

```
x =  ( ∑ (rem[i]*pp[i]*inv[i]) ) % prod
   Where 0 <= i <= n-1

rem[i] is given array of remainders

prod is product of all given numbers
prod = num[0] * num[1] * ... * num[k-1]

pp[i] is product of all divided by num[i]
pp[i] = prod / num[i]

inv[i] = Modular Multiplicative Inverse of 
         pp[i] with respect to num[i]
```

**示例:**

```
Let us take below example to understand the solution
   num[] = {3, 4, 5}, rem[] = {2, 3, 1}
   prod  = 60 
   pp[]  = {20, 15, 12}
   inv[] = {2,  3,  3}  // (20*2)%3 = 1, (15*3)%4 = 1
                        // (12*3)%5 = 1

   x = (rem[0]*pp[0]*inv[0] + rem[1]*pp[1]*inv[1] + 
        rem[2]*pp[2]*inv[2]) % prod
     = (2*20*2 + 3*15*3 + 1*12*3) % 60
     = (80 + 135 + 36) % 60
     = 11
```

参考[这个](https://www.youtube.com/watch?v=ru7mWZJlRQg)可以很好的直观的解释上面的公式。

下面是上面公式的实现。我们可以使用这里讨论的基于扩展欧几里德的方法来求逆模。

## C++

```
// A C++ program to demonstrate
// working of Chinise remainder
// Theorem
#include <bits/stdc++.h>
using namespace std;

// Returns modulo inverse of a
// with respect to m using
// extended Euclid Algorithm.
// Refer below post for details:
// https://www.geeksforgeeks.org/
// multiplicative-inverse-under-modulo-m/
int inv(int a, int m)
{
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;

    if (m == 1)
        return 0;

    // Apply extended Euclid Algorithm
    while (a > 1) {
        // q is quotient
        q = a / m;

        t = m;

        // m is remainder now, process same as
        // euclid's algo
        m = a % m, a = t;

        t = x0;

        x0 = x1 - q * x0;

        x1 = t;
    }

    // Make x1 positive
    if (x1 < 0)
        x1 += m0;

    return x1;
}

// k is size of num[] and rem[]. Returns the smallest
// number x such that:
// x % num[0] = rem[0],
// x % num[1] = rem[1],
// ..................
// x % num[k-2] = rem[k-1]
// Assumption: Numbers in num[] are pairwise coprime
// (gcd for every pair is 1)
int findMinX(int num[], int rem[], int k)
{
    // Compute product of all numbers
    int prod = 1;
    for (int i = 0; i < k; i++)
        prod *= num[i];

    // Initialize result
    int result = 0;

    // Apply above formula
    for (int i = 0; i < k; i++) {
        int pp = prod / num[i];
        result += rem[i] * inv(pp, num[i]) * pp;
    }

    return result % prod;
}

// Driver method
int main(void)
{
    int num[] = { 3, 4, 5 };
    int rem[] = { 2, 3, 1 };
    int k = sizeof(num) / sizeof(num[0]);
    cout << "x is " << findMinX(num, rem, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to demonstrate
// working of Chinise remainder
// Theorem
import java.io.*;

class GFG {

    // Returns modulo inverse of a
    // with respect to m using extended
    // Euclid Algorithm. Refer below post for details:
    // https://www.geeksforgeeks.org/
    // multiplicative-inverse-under-modulo-m/
    static int inv(int a, int m)
    {
        int m0 = m, t, q;
        int x0 = 0, x1 = 1;

        if (m == 1)
            return 0;

        // Apply extended Euclid Algorithm
        while (a > 1) {
            // q is quotient
            q = a / m;

            t = m;

            // m is remainder now, process
            // same as euclid's algo
            m = a % m;
            a = t;

            t = x0;

            x0 = x1 - q * x0;

            x1 = t;
        }

        // Make x1 positive
        if (x1 < 0)
            x1 += m0;

        return x1;
    }

    // k is size of num[] and rem[].
    // Returns the smallest number
    // x such that:
    // x % num[0] = rem[0],
    // x % num[1] = rem[1],
    // ..................
    // x % num[k-2] = rem[k-1]
    // Assumption: Numbers in num[] are pairwise
    // coprime (gcd for every pair is 1)
    static int findMinX(int num[], int rem[], int k)
    {
        // Compute product of all numbers
        int prod = 1;
        for (int i = 0; i < k; i++)
            prod *= num[i];

        // Initialize result
        int result = 0;

        // Apply above formula
        for (int i = 0; i < k; i++) {
            int pp = prod / num[i];
            result += rem[i] * inv(pp, num[i]) * pp;
        }

        return result % prod;
    }

    // Driver method
    public static void main(String args[])
    {
        int num[] = { 3, 4, 5 };
        int rem[] = { 2, 3, 1 };
        int k = num.length;
        System.out.println("x is " + findMinX(num, rem, k));
    }
}

// This code is contributed by nikita Tiwari.
```

## 蟒蛇 3

```
# A Python3 program to demonstrate
# working of Chinise remainder
# Theorem

# Returns modulo inverse of a with
# respect to m using extended
# Euclid Algorithm. Refer below
# post for details:
# https://www.geeksforgeeks.org/
# multiplicative-inverse-under-modulo-m/
def inv(a, m) :

    m0 = m
    x0 = 0
    x1 = 1

    if (m == 1) :
        return 0

    # Apply extended Euclid Algorithm
    while (a > 1) :
        # q is quotient
        q = a // m

        t = m

        # m is remainder now, process
        # same as euclid's algo
        m = a % m
        a = t

        t = x0

        x0 = x1 - q * x0

        x1 = t

    # Make x1 positive
    if (x1 < 0) :
        x1 = x1 + m0

    return x1

# k is size of num[] and rem[].
# Returns the smallest
# number x such that:
# x % num[0] = rem[0],
# x % num[1] = rem[1],
# ..................
# x % num[k-2] = rem[k-1]
# Assumption: Numbers in num[]
# are pairwise coprime
# (gcd for every pair is 1)
def findMinX(num, rem, k) :

    # Compute product of all numbers
    prod = 1
    for i in range(0, k) :
        prod = prod * num[i]

    # Initialize result
    result = 0

    # Apply above formula
    for i in range(0,k):
        pp = prod // num[i]
        result = result + rem[i] * inv(pp, num[i]) * pp

    return result % prod

# Driver method
num = [3, 4, 5]
rem = [2, 3, 1]
k = len(num)
print( "x is " , findMinX(num, rem, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A C# program to demonstrate
// working of Chinese remainder
// Theorem
using System;

class GFG
{
    // Returns modulo inverse of
    // 'a' with respect to 'm'
    // using extended Euclid Algorithm.
    // Refer below post for details:
    // https://www.geeksforgeeks.org/
    // multiplicative-inverse-under-modulo-m/
    static int inv(int a, int m)
    {
        int m0 = m, t, q;
        int x0 = 0, x1 = 1;

        if (m == 1)
        return 0;

        // Apply extended
        // Euclid Algorithm
        while (a > 1)
        {
            // q is quotient
            q = a / m;

            t = m;

            // m is remainder now,
            // process same as
            // euclid's algo
            m = a % m; a = t;

            t = x0;

            x0 = x1 - q * x0;

            x1 = t;
        }

        // Make x1 positive
        if (x1 < 0)
        x1 += m0;

        return x1;
    }

    // k is size of num[] and rem[].
    // Returns the smallest number
    // x such that:
    // x % num[0] = rem[0],
    // x % num[1] = rem[1],
    // ..................
    // x % num[k-2] = rem[k-1]
    // Assumption: Numbers in num[]
    // are pairwise coprime (gcd
    // for every pair is 1)
    static int findMinX(int []num,
                        int []rem,
                        int k)
    {
        // Compute product
        // of all numbers
        int prod = 1;
        for (int i = 0; i < k; i++)
            prod *= num[i];

        // Initialize result
        int result = 0;

        // Apply above formula
        for (int i = 0; i < k; i++)
        {
            int pp = prod / num[i];
            result += rem[i] *
                    inv(pp, num[i]) * pp;
        }

        return result % prod;
    }

    // Driver Code
    static public void Main ()
    {
        int []num = {3, 4, 5};
        int []rem = {2, 3, 1};
        int k = num.Length;
        Console.WriteLine("x is " +
                        findMinX(num, rem, k));
    }
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate working
// of Chinise remainder Theorem

// Returns modulo inverse of a with
// respect to m using extended Euclid
// Algorithm. Refer below post for details:
// https://www.geeksforgeeks.org/
// multiplicative-inverse-under-modulo-m/
function inv($a, $m)
{
    $m0 = $m;
    $x0 = 0;
    $x1 = 1;

    if ($m == 1)
    return 0;

    // Apply extended Euclid Algorithm
    while ($a > 1)
    {
        // q is quotient
        $q = (int)($a / $m);

        $t = $m;

        // m is remainder now, process
        // same as euclid's algo
        $m = $a % $m;
        $a = $t;

        $t = $x0;

        $x0 = $x1 - $q * $x0;

        $x1 = $t;
    }

    // Make x1 positive
    if ($x1 < 0)
    $x1 += $m0;

    return $x1;
}

// k is size of num[] and rem[].
// Returns the smallest
// number x such that:
// x % num[0] = rem[0],
// x % num[1] = rem[1],
// ..................
// x % num[k-2] = rem[k-1]
// Assumption: Numbers in num[]
// are pairwise coprime (gcd for
// every pair is 1)
function findMinX($num, $rem, $k)
{
    // Compute product of all numbers
    $prod = 1;
    for ($i = 0; $i < $k; $i++)
        $prod *= $num[$i];

    // Initialize result
    $result = 0;

    // Apply above formula
    for ($i = 0; $i < $k; $i++)
    {
        $pp = (int)$prod / $num[$i];
        $result += $rem[$i] * inv($pp,
                    $num[$i]) * $pp;
    }

    return $result % $prod;
}

// Driver Code
$num = array(3, 4, 5);
$rem = array(2, 3, 1);
$k = sizeof($num);
echo "x is ". findMinX($num, $rem, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to demonstrate working
// of Chinise remainder Theorem

// Returns modulo inverse of a with
// respect to m using extended Euclid
// Algorithm. Refer below post for details:
// https://www.geeksforgeeks.org/
// multiplicative-inverse-under-modulo-m/
function inv(a, m)
{
    let m0 = m;
    let x0 = 0;
    let x1 = 1;

    if (m == 1)
    return 0;

    // Apply extended Euclid Algorithm
    while (a > 1)
    {
        // q is quotient
        let q = parseInt(a / m);

        let t = m;

        // m is remainder now, process
        // same as euclid's algo
        m = a % m;
        a = t;

        t = x0;

        x0 = x1 - q * x0;

        x1 = t;
    }

    // Make x1 positive
    if (x1 < 0)
    x1 += m0;

    return x1;
}

// k is size of num[] and rem[].
// Returns the smallest
// number x such that:
// x % num[0] = rem[0],
// x % num[1] = rem[1],
// ..................
// x % num[k-2] = rem[k-1]
// Assumption: Numbers in num[]
// are pairwise coprime (gcd for
// every pair is 1)
function findMinX(num, rem, k)
{
    // Compute product of all numbers
    let prod = 1;
    for (let i = 0; i < k; i++)
        prod *= num[i];

    // Initialize result
    let result = 0;

    // Apply above formula
    for (let i = 0; i < k; i++)
    {
        pp = parseInt(prod / num[i]);
        result += rem[i] * inv(pp,
                    num[i]) * pp;
    }

    return result % prod;
}

// Driver Code
let num = new Array(3, 4, 5);
let rem = new Array(2, 3, 1);
let k = num.length;
document.write("x is " + findMinX(num, rem, k));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
x is 11
```

**时间复杂度:** O(N*LogN)

**辅助空间:** O(1)

本文由 **Ruchir Garg** 供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论