# 位数总和等于其所有质因数位数总和的数字

> 原文:[https://www . geesforgeks . org/数字总和等于其所有质因数的数字总和/](https://www.geeksforgeeks.org/numbers-with-sum-of-digits-equal-to-the-sum-of-digits-of-its-all-prime-factor/)

给定一个范围，任务是找出给定范围内数字的计数，使其位数之和等于其所有质因数位数之和。
**例:**

```
Input: l = 2, r = 10
Output: 5
2, 3, 4, 5 and 7 are such numbers

Input: l = 15, r = 22
Output: 3
17, 19 and 22 are such numbers
As, 17 and 19 are already prime.
Prime Factors of 22 = 2 * 11 i.e 
For 22, Sum of digits is 2+2 = 4
For 2 * 11, Sum of digits is 2 + 1 + 1 = 4
```

**方法:**一个有效的解决方案是修改厄拉多塞的[筛，使得对于每个非质数，它存储最小的质因数(前因子)。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

1.  预处理，为 2 到 MAXN 之间的所有数字找到最小的质因数。这可以通过在恒定时间内把数分解成它的质因数来实现，因为对于每个数，如果它是质数，它就没有前置因子。
2.  否则，我们可以把它分解成一个质因数和数的另一部分，它可能是质因数，也可能不是质因数。
3.  重复这个提取因子的过程，直到它变成质数。
4.  然后通过将最小质因数的第个数字相加，即

    > ，检查该数字的位数是否等于质因数的位数位数 _ SPF 之和[n] +位数 _ SPF 之和(不适用)

5.  现在制作前缀和数组，计算一个数字 n 的有效数字。对于每个查询，打印:

    > **年[r]—年【L-1】**

以下是上述方法的实现:

## C++

```
// C++ program to Find the count of the numbers
// in the given range such that the sum of its
// digit is equal to the sum of all its prime
// factors digits sum.
#include <bits/stdc++.h>
using namespace std;

// maximum size of number
#define MAXN 100005

// array to store smallest prime factor of number
int spf[MAXN] = { 0 };

// array to store sum of digits of a number
int sum_digits[MAXN] = { 0 };

// boolean array to check given number is countable
// for required answer or not.
bool isValid[MAXN] = { 0 };

// prefix array to store answer
int ans[MAXN] = { 0 };

// Calculating SPF (Smallest Prime Factor) for every
// number till MAXN.
void Smallest_prime_factor()
{
    // marking smallest prime factor for every
    // number to be itself.
    for (int i = 1; i < MAXN; i++)
        spf[i] = i;

    // separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i <= MAXN; i += 2)

        // checking if i is prime
        if (spf[i] == i)

            // marking SPF for all numbers divisible by i
            for (int j = i * i; j < MAXN; j += i)

                // marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
}

// Function to find sum of digits in a number
int Digit_Sum(int copy)
{
    int d = 0;
    while (copy) {
        d += copy % 10;
        copy /= 10;
    }

    return d;
}

// find sum of digits of all numbers up to MAXN
void Sum_Of_All_Digits()
{
    for (int n = 2; n < MAXN; n++) {
        // add sum of digits of least 
        // prime factor and n/spf[n]
        sum_digits[n] = sum_digits[n / spf[n]] 
                           + Digit_Sum(spf[n]);

        // if it is valid make isValid true
        if (Digit_Sum(n) == sum_digits[n])
            isValid[n] = true;
    }

    // prefix sum to compute answer
    for (int n = 2; n < MAXN; n++) {
        if (isValid[n])
            ans[n] = 1;
        ans[n] += ans[n - 1];
    }
}

// Driver code
int main()
{
    Smallest_prime_factor();
    Sum_Of_All_Digits();

    // decleartion
    int l, r;

    // print answer for required range
    l = 2, r = 3;
    cout << "Valid numbers in the range " << l << " " 
         << r << " are " << ans[r] - ans[l - 1] << endl;

    // print answer for required range
    l = 2, r = 10;
    cout << "Valid numbers in the range " << l << " " 
         << r << " are " << ans[r] - ans[l - 1] << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the count 
// of the numbers in the given 
// range such that the sum of its
// digit is equal to the sum of 
// all its prime factors digits sum.
import java.io.*;

class GFG 
{

// maximum size of number
static int MAXN = 100005;

// array to store smallest 
// prime factor of number
static int spf[] = new int[MAXN];

// array to store sum 
// of digits of a number
static int sum_digits[] = new int[MAXN];

// boolean array to check
// given number is countable
// for required answer or not.
static boolean isValid[] = new boolean[MAXN];

// prefix array to store answer
static int ans[] = new int[MAXN];

// Calculating SPF (Smallest
// Prime Factor) for every
// number till MAXN.
static void Smallest_prime_factor()
{
    // marking smallest prime factor 
    // for every number to be itself.
    for (int i = 1; i < MAXN; i++)
        spf[i] = i;

    // separately marking spf 
    // for every even number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; 
             i * i <= MAXN; i += 2)

        // checking if i is prime
        if (spf[i] == i)

            // marking SPF for all
            // numbers divisible by i
            for (int j = i * i; 
                     j < MAXN; j += i)

                // marking spf[j] if it
                // is not previously marked
                if (spf[j] == j)
                    spf[j] = i;
}

// Function to find sum 
// of digits in a number
static int Digit_Sum(int copy)
{
    int d = 0;
    while (copy > 0) 
    {
        d += copy % 10;
        copy /= 10;
    }

    return d;
}

// find sum of digits of 
// all numbers up to MAXN
static void Sum_Of_All_Digits()
{
    for (int n = 2; n < MAXN; n++)
    {
        // add sum of digits of least 
        // prime factor and n/spf[n]
        sum_digits[n] = sum_digits[n / spf[n]] 
                          + Digit_Sum(spf[n]);

        // if it is valid make isValid true
        if (Digit_Sum(n) == sum_digits[n])
            isValid[n] = true;
    }

    // prefix sum to compute answer
    for (int n = 2; n < MAXN; n++) 
    {
        if (isValid[n])
            ans[n] = 1;
        ans[n] += ans[n - 1];
    }
}

// Driver code
public static void main (String[] args) 
{
    Smallest_prime_factor();
    Sum_Of_All_Digits();

    // declaration
    int l, r;

    // print answer for required range
    l = 2; r = 3;
    System.out.println("Valid numbers in the range " + 
                               l + " " + r + " are " + 
                              (ans[r] - ans[l - 1] ));

    // print answer for required range
    l = 2; r = 10;
    System.out.println("Valid numbers in the range " + 
                               l + " " + r + " are " + 
                               (ans[r] - ans[l - 1]));
}
}

// This code is contributed
// by Inder
```

## 蟒蛇 3

```
# Python 3 program to Find the count of 
# the numbers in the given range such
# that the sum of its digit is equal to
# the sum of all its prime factors digits sum.

# maximum size of number
MAXN = 100005

# array to store smallest prime
# factor of number
spf = [0] * MAXN

# array to store sum of digits of a number
sum_digits = [0] * MAXN

# boolean array to check given number 
# is countable for required answer or not.
isValid = [0] * MAXN

# prefix array to store answer
ans = [0]*MAXN

# Calculating SPF (Smallest Prime Factor) 
# for every number till MAXN.
def Smallest_prime_factor():

    # marking smallest prime factor
    # for every number to be itself.
    for i in range(1, MAXN):
        spf[i] = i

    # separately marking spf for 
    # every even number as 2
    for i in range(4, MAXN, 2):
        spf[i] = 2

    i = 3
    while i * i <= MAXN: 

        # checking if i is prime
        if (spf[i] == i):

            # marking SPF for all numbers
            # divisible by i
            for j in range(i * i, MAXN, i):

                # marking spf[j] if it is not
                # previously marked
                if (spf[j] == j):
                    spf[j] = i

        i += 2

# Function to find sum of digits 
# in a number
def Digit_Sum(copy):

    d = 0
    while (copy) :
        d += copy % 10
        copy //= 10

    return d

# find sum of digits of all
# numbers up to MAXN
def Sum_Of_All_Digits():

    for n in range(2, MAXN) :

        # add sum of digits of least 
        # prime factor and n/spf[n]
        sum_digits[n] = (sum_digits[n // spf[n]] +
                         Digit_Sum(spf[n]))

        # if it is valid make isValid true
        if (Digit_Sum(n) == sum_digits[n]):
            isValid[n] = True

    # prefix sum to compute answer
    for n in range(2, MAXN) :
        if (isValid[n]):
            ans[n] = 1
        ans[n] += ans[n - 1]

# Driver code
if __name__ == "__main__":

    Smallest_prime_factor()
    Sum_Of_All_Digits()

    # print answer for required range
    l = 2
    r = 3
    print("Valid numbers in the range", l, r,
                  "are", ans[r] - ans[l - 1])

    # print answer for required range
    l = 2
    r = 10
    print("Valid numbers in the range", l, r, 
                  "are", ans[r] - ans[l - 1])

# This code is contributed by ita_c
```

## C#

```
// C# program to Find the count 
// of the numbers in the given 
// range such that the sum of its
// digit is equal to the sum of 
// all its prime factors digits sum.
using System;

class GFG 
{

// maximum size of number
static int MAXN = 100005;

// array to store smallest 
// prime factor of number
static int []spf = new int[MAXN];

// array to store sum 
// of digits of a number
static int []sum_digits = new int[MAXN];

// boolean array to check
// given number is countable
// for required answer or not.
static bool []isValid = new bool[MAXN];

// prefix array to store answer
static int []ans = new int[MAXN];

// Calculating SPF (Smallest
// Prime Factor) for every
// number till MAXN.
static void Smallest_prime_factor()
{
    // marking smallest prime factor 
    // for every number to be itself.
    for (int i = 1; i < MAXN; i++)
        spf[i] = i;

    // separately marking spf 
    // for every even number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; 
             i * i <= MAXN; i += 2)

        // checking if i is prime
        if (spf[i] == i)

            // marking SPF for all
            // numbers divisible by i
            for (int j = i * i; 
                     j < MAXN; j += i)

                // marking spf[j] if it
                // is not previously marked
                if (spf[j] == j)
                    spf[j] = i;
}

// Function to find sum 
// of digits in a number
static int Digit_Sum(int copy)
{
    int d = 0;
    while (copy > 0) 
    {
        d += copy % 10;
        copy /= 10;
    }

    return d;
}

// find sum of digits of 
// all numbers up to MAXN
static void Sum_Of_All_Digits()
{
    for (int n = 2; n < MAXN; n++)
    {
        // add sum of digits of least 
        // prime factor and n/spf[n]
        sum_digits[n] = sum_digits[n / spf[n]] +
                              Digit_Sum(spf[n]);

        // if it is valid make 
        // isValid true
        if (Digit_Sum(n) == sum_digits[n])
            isValid[n] = true;
    }

    // prefix sum to compute answer
    for (int n = 2; n < MAXN; n++) 
    {
        if (isValid[n])
            ans[n] = 1;
        ans[n] += ans[n - 1];
    }
}

// Driver code
public static void Main () 
{
    Smallest_prime_factor();
    Sum_Of_All_Digits();

    // declaration
    int l, r;

    // print answer for required range
    l = 2; r = 3;
    Console.WriteLine("Valid numbers in the range " + 
                              l + " " + r + " are " + 
                             (ans[r] - ans[l - 1] ));

    // print answer for required range
    l = 2; r = 10;
    Console.WriteLine("Valid numbers in the range " + 
                              l + " " + r + " are " + 
                              (ans[r] - ans[l - 1]));
}
}

// This code is contributed
// by Subhadeep
```

## java 描述语言

```
<script>

// Javascript program to Find the count 
// of the numbers in the given 
// range such that the sum of its
// digit is equal to the sum of 
// all its prime factors digits sum.

// maximum size of number
var MAXN = 100005;

// array to store smallest 
// prime factor of number
var spf = Array.from({length: MAXN}, (_, i) => 0);

// array to store sum 
// of digits of a number
var sum_digits = Array.from({length: MAXN}, (_, i) => 0);

// boolean array to check
// given number is countable
// for required answer or not.
var isValid = Array.from({length: MAXN}, (_, i) => false);

// prefix array to store answer
var ans = Array.from({length: MAXN}, (_, i) => 0);

// Calculating SPF (Smallest
// Prime Factor) for every
// number till MAXN.
function Smallest_prime_factor()
{
    // marking smallest prime factor 
    // for every number to be itself.
    for (i = 1; i < MAXN; i++)
        spf[i] = i;

    // separately marking spf 
    // for every even number as 2
    for (i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (i = 3; 
             i * i <= MAXN; i += 2)

        // checking if i is prime
        if (spf[i] == i)

            // marking SPF for all
            // numbers divisible by i
            for (j = i * i; 
                     j < MAXN; j += i)

                // marking spf[j] if it
                // is not previously marked
                if (spf[j] == j)
                    spf[j] = i;
}

// Function to find sum 
// of digits in a number
function Digit_Sum(copy)
{
    var d = 0;
    while (copy > 0) 
    {
        d += copy % 10;
        copy = parseInt(copy/10);
    }

    return d;
}

// find sum of digits of 
// all numbers up to MAXN
function Sum_Of_All_Digits()
{
    for (n = 2; n < MAXN; n++)
    {
        // add sum of digits of least 
        // prime factor and n/spf[n]
        sum_digits[n] = sum_digits[parseInt(n / spf[n])] 
                          + Digit_Sum(spf[n]);

        // if it is valid make isValid true
        if (Digit_Sum(n) == sum_digits[n])
            isValid[n] = true;
    }

    // prefix sum to compute answer
    for (n = 2; n < MAXN; n++) 
    {
        if (isValid[n])
            ans[n] = 1;
        ans[n] += ans[n - 1];
    }
}

// Driver code
Smallest_prime_factor();
Sum_Of_All_Digits();

// declaration
var l, r;

// print answer for required range
l = 2; r = 3;
document.write("Valid numbers in the range " + 
                           l + " " + r + " are " + 
                          (ans[r] - ans[l - 1] ));

// print answer for required range
l = 2; r = 10;
document.write("<br>Valid numbers in the range " + 
                           l + " " + r + " are " + 
                           (ans[r] - ans[l - 1]));

// This code contributed by shikhasingrajput 

</script>
```

**Output:** 

```
Valid numbers in the range 2 3 are 2
Valid numbers in the range 2 10 are 5
```