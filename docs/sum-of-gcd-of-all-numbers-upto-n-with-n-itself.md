# 直到 N 与 N 本身的所有数字的 GCD 之和

> 原文:[https://www . geesforgeks . org/sum-of-gcd-of-all-numbers-up-n-with-n-nature/](https://www.geeksforgeeks.org/sum-of-gcd-of-all-numbers-upto-n-with-n-itself/)

给定一个整数 **N** ，任务是用 **N** 本身求到 **N** 为止所有数字的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)之和。
**示例:**

> **输入:** N = 12
> **输出:** 40
> **解释:**
> GCD 的[1，12] = 1、[2，12] = 2、[3，12] = 3、[4，12] = 4、[5，12] = 1、[6，12] = 6、[7，12] = 1、[8，12] = 4、[9，12] = 3、[10，12] = 2、[11，11]总和是(1 + 2 + 3 + 4 + 1 + 6 + 1 + 4 + 3 + 2 + 1 + 12) = 40。
> **输入:** N = 2
> **输出:** 3
> **解释:**
> GCD 的[1，2] = 1，[2，2] = 2，它们的和为 3。

**天真的方法:**一个简单的解决方法是迭代从 1 到 N 的所有数字，用 N 本身找到它们的 gcd，并继续添加它们。
**时间复杂度:** *O(N * log N)*
**高效途径:**
为了优化上述途径，我们需要观察到 **GCD(i，N)给出了 N 的除数之一**。因此，我们可以检查 N 的每个除数，有多少个数字的 GCD(i，N)与该除数相同，而不是从 1 到 N 循环。

> **图解:**
> 例如 N = 12，它的除数是 1，2，3，4，6，12。
> 范围内的数字**【1，12】**，其 GCD 为 12 的数字为:
> 
> *   1 是{1，5，7，11}
> *   2 是{2，10}
> *   3 是{3，9}
> *   4 是{4，8}
> *   6 是{6}
> *   12 是{12}
> 
> 所以答案是；1*4 + 2*2 + 3*2 + 4*2 + 6*1 + 12*1 = 40.

*   所以我们要用 GCD *d* 求从 1 到 **N** 的整数个数，其中 **d** 是 **N** 的除数。让我们考虑 x <sub>1</sub> ，x <sub>2</sub> ，x <sub>3</sub> ，…。x <sub>n</sub> 作为从 1 到 N 的不同整数，使得它们与 N 的 GCD 为 d
*   此后， **GCD(x <sub>i</sub> ，N) = d** 然后 **GCD(x <sub>i</sub> /d，N/d) = 1**
*   所以，从 1 到 **N** 的整数计数，其与 **N** 的 GCD 是 **d** 是 **(N/d)** 的[欧拉全图函数](https://www.geeksforgeeks.org/eulers-totient-function/)。

下面是上述方法的实现:

## C++

```
// C++ Program to find the Sum
// of GCD of all integers up to N
// with N itself

#include <bits/stdc++.h>
using namespace std;

// Function to Find Sum of
// GCD of each numbers
int getCount(int d, int n)
{

    int no = n / d;

    int result = no;

    // Consider all prime factors
    // of no. and subtract their
    // multiples from result
    for (int p = 2; p * p <= no; ++p) {

        // Check if p is a prime factor
        if (no % p == 0) {

            // If yes, then update no
            // and result
            while (no % p == 0)
                no /= p;
            result -= result / p;
        }
    }

    // If no has a prime factor greater
    // than sqrt(n) then at-most one such
    // prime factor exists
    if (no > 1)
        result -= result / no;

    // Return the result
    return result;
}

// Finding GCD of pairs
int sumOfGCDofPairs(int n)
{
    int res = 0;

    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            // Calculate the divisors
            int d1 = i;
            int d2 = n / i;

            // Return count of numbers
            // from 1 to N with GCD d with N
            res += d1 * getCount(d1, n);

            // Check if d1 and d2 are
            // equal then skip this
            if (d1 != d2)
                res += d2 * getCount(d2, n);
        }
    }

    return res;
}

// Driver code
int main()
{
    int n = 12;

    cout << sumOfGCDofPairs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Sum
// of GCD of all integers up to N
// with N itself
class GFG{

// Function to Find Sum of
// GCD of each numbers
static int getCount(int d, int n)
{
    int no = n / d;
    int result = no;

    // Consider all prime factors
    // of no. and subtract their
    // multiples from result
    for(int p = 2; p * p <= no; ++p)
    {

        // Check if p is a prime factor
        if (no % p == 0)
        {

            // If yes, then update no
            // and result
            while (no % p == 0)
                no /= p;
            result -= result / p;
        }
    }

    // If no has a prime factor greater
    // than Math.sqrt(n) then at-most one such
    // prime factor exists
    if (no > 1)
        result -= result / no;

    // Return the result
    return result;
}

// Finding GCD of pairs
static int sumOfGCDofPairs(int n)
{
    int res = 0;

    for(int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {

            // Calculate the divisors
            int d1 = i;
            int d2 = n / i;

            // Return count of numbers
            // from 1 to N with GCD d with N
            res += d1 * getCount(d1, n);

            // Check if d1 and d2 are
            // equal then skip this
            if (d1 != d2)
                res += d2 * getCount(d2, n);
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int n = 12;

    System.out.print(sumOfGCDofPairs(n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of GCD of all integers up to N
# with N itself

# Function to Find Sum of
# GCD of each numbers
def getCount(d, n):

    no = n // d;
    result = no;

    # Consider all prime factors
    # of no. and subtract their
    # multiples from result
    for p in range(2, int(pow(no, 1 / 2)) + 1):

        # Check if p is a prime factor
        if (no % p == 0):

            # If yes, then update no
            # and result
            while (no % p == 0):
                no //= p;

            result -= result // p;

    # If no has a prime factor greater
    # than Math.sqrt(n) then at-most one such
    # prime factor exists
    if (no > 1):
        result -= result // no;

    # Return the result
    return result;

# Finding GCD of pairs
def sumOfGCDofPairs(n):

    res = 0;

    for i in range(1, int(pow(n, 1 / 2)) + 1):
        if (n % i == 0):

            # Calculate the divisors
            d1 = i;
            d2 = n // i;

            # Return count of numbers
            # from 1 to N with GCD d with N
            res += d1 * getCount(d1, n);

            # Check if d1 and d2 are
            # equal then skip this
            if (d1 != d2):
                res += d2 * getCount(d2, n);

    return res;

# Driver code
if __name__ == '__main__':

    n = 12;

    print(sumOfGCDofPairs(n));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to find the sum
// of GCD of all integers up to N
// with N itself
using System;

class GFG{

// Function to find sum of
// GCD of each numbers
static int getCount(int d, int n)
{
    int no = n / d;
    int result = no;

    // Consider all prime factors
    // of no. and subtract their
    // multiples from result
    for(int p = 2; p * p <= no; ++p)
    {

        // Check if p is a prime factor
        if (no % p == 0)
        {

            // If yes, then update no
            // and result
            while (no % p == 0)
                no /= p;

            result -= result / p;
        }
    }

    // If no has a prime factor greater
    // than Math.Sqrt(n) then at-most
    // one such prime factor exists
    if (no > 1)
        result -= result / no;

    // Return the result
    return result;
}

// Finding GCD of pairs
static int sumOfGCDofPairs(int n)
{
    int res = 0;

    for(int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {

            // Calculate the divisors
            int d1 = i;
            int d2 = n / i;

            // Return count of numbers
            // from 1 to N with GCD d with N
            res += d1 * getCount(d1, n);

            // Check if d1 and d2 are
            // equal then skip this
            if (d1 != d2)
                res += d2 * getCount(d2, n);
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int n = 12;

    Console.Write(sumOfGCDofPairs(n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript Program to find the Sum
// of GCD of all integers up to N
// with N itself

// Function to Find Sum of
// GCD of each numbers
function getCount(d, n)
{

    let no = Math.floor(n / d);

    let result = no;

    // Consider all prime factors
    // of no. and subtract their
    // multiples from result
    for (let p = 2; p * p <= no; ++p) {

        // Check if p is a prime factor
        if (no % p == 0) {

            // If yes, then update no
            // and result
            while (no % p == 0)
                no = Math.floor(no / p);
            result = Math.floor(result - result / p);
        }
    }

    // If no has a prime factor greater
    // than sqrt(n) then at-most one such
    // prime factor exists
    if (no > 1)
        result = Math.floor(result - result / no);

    // Return the result
    return result;
}

// Finding GCD of pairs
function sumOfGCDofPairs(n)
{
    let res = 0;

    for (let i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            // Calculate the divisors
            let d1 = i;
            let d2 = Math.floor(n / i);

            // Return count of numbers
            // from 1 to N with GCD d with N
            res += d1 * getCount(d1, n);

            // Check if d1 and d2 are
            // equal then skip this
            if (d1 != d2)
                res += d2 * getCount(d2, n);
        }
    }

    return res;
}

// Driver code

    let n = 12;

    document.write(sumOfGCDofPairs(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
40
```

**时间复杂度:**T2【O(N)T4】