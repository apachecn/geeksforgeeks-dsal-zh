# 一个数除以另一个数的最高幂

> 原文:[https://www . geesforgeks . org/除以其他数的最高幂数/](https://www.geeksforgeeks.org/highest-power-of-a-number-that-divides-other-number/)

给定两个数 **N** 和 **M** ，任务是找出 M 除 N 的最高幂
**注** : M > 1
**例:**

> **输入:** N = 48，M = 4
> **输出:** 2
> 48 % (4^2) = 0
> **输入:** N = 32，M = 20
> **输出:** 0
> 32 % (20^0) = 0

**逼近**:首先对数字 **N** 和 **M** 进行质因数分解，并将 N 和 M 的质因数计数分别存储在**freq 1【】**和**freq 2【】**中，对于 M 的每个质因数，检查其**freq 2【num】**是否大于**freq 1【num】**。如果是 M 的任意质因数，则最大功率为 **0** 。否则，对于 **M** 的每个质因数，最大功率将是所有 **freq1[num] / freq2[num]** 的最小值。
对于一个数 **N = 24，**质因数将 *2^3 * 3^1* 。因此 freq1[2] = 3，freq1[3] = 1。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the prime factors
// and its count of times it divides
void primeFactors(int n, int freq[])
{

    int cnt = 0;

    // Count the number of 2s that divide n
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    freq[2] = cnt;

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i + 2) {
        cnt = 0;

        // While i divides n, count i and divide n
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        freq[i] = cnt;
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        freq[n] = 1;
}

// Function to return the highest power
int getMaximumPower(int n, int m)
{

    // Initialize two arrays
    int freq1[n + 1], freq2[m + 1];

    memset(freq1, 0, sizeof freq1);
    memset(freq2, 0, sizeof freq2);

    // Get the prime factors of n and m
    primeFactors(n, freq1);
    primeFactors(m, freq2);

    int maxi = 0;

    // Iterate and find the maximum power
    for (int i = 2; i <= m; i++) {

        // If i not a prime factor of n and m
        if (freq1[i] == 0 && freq2[i] == 0)
            continue;

        // If i is a prime factor of n and m
        // If count of i dividing m is more
        // than i dividing n, then power will be 0
        if (freq2[i] > freq1[i])
            return 0;

        // If i is a prime factor of M
        if (freq2[i]) {

            // get the maximum power
            maxi = max(maxi, freq1[i] / freq2[i]);
        }
    }

    return maxi;
}

// Drivers code
int main()
{
    int n = 48, m = 4;
    cout << getMaximumPower(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG
{

// Function to get the prime factors
// and its count of times it divides
static void primeFactors(int n, int freq[])
{

    int cnt = 0;

    // Count the number of 2s that divide n
    while (n % 2 == 0)
    {
        cnt++;
        n = n / 2;
    }

    freq[2] = cnt;

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= Math.sqrt(n); i = i + 2)
    {
        cnt = 0;

        // While i divides n, count i and divide n
        while (n % i == 0)
        {
            cnt++;
            n = n / i;
        }

        freq[i] = cnt;
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        freq[n] = 1;
}

// Function to return the highest power
static int getMaximumPower(int n, int m)
{

    // Initialize two arrays
    int freq1[] = new int[n + 1], freq2[] = new int[m + 1];

    // Get the prime factors of n and m
    primeFactors(n, freq1);
    primeFactors(m, freq2);

    int maxi = 0;

    // Iterate and find the maximum power
    for (int i = 2; i <= m; i++)
    {

        // If i not a prime factor of n and m
        if (freq1[i] == 0 && freq2[i] == 0)
            continue;

        // If i is a prime factor of n and m
        // If count of i dividing m is more
        // than i dividing n, then power will be 0
        if (freq2[i] > freq1[i])
            return 0;

        // If i is a prime factor of M
        if (freq2[i] != 0)
        {

            // get the maximum power
            maxi = Math.max(maxi, freq1[i] / freq2[i]);
        }
    }

    return maxi;
}

// Drivers code
public static void main(String[] args)
{
    int n = 48, m = 4;
    System.out.println(getMaximumPower(n, m));

}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
import math

# Python program to implement
# the above approach

# Function to get the prime factors
# and its count of times it divides
def primeFactors(n, freq):
    cnt = 0

    # Count the number of 2s that divide n
    while n % 2 == 0:
        cnt = cnt + 1
        n = int(n // 2)

    freq[2] = cnt

    # n must be odd at this point. So we can skip
    # one element (Note i = i+2)
    i=3
    while i<=math.sqrt(n):
        cnt = 0

        # While i divides n, count i and divide n
        while (n % i == 0):
            cnt = cnt+1
            n = int(n // i)

        freq[int(i)] = cnt
        i=i + 2

    # This condition is to handle the case when n
    # is a prime number greater than 2
    if (n > 2):
        freq[int(n)] = 1

# Function to return the highest power
def getMaximumPower(n, m):

    # Initialize two arrays
    freq1 = [0] * (n + 1)
    freq2 = [0] * (m + 1)

    # Get the prime factors of n and m
    primeFactors(n, freq1)
    primeFactors(m, freq2)

    maxi = 0

    # Iterate and find the maximum power
    i = 2
    while i <= m:

        # If i not a prime factor of n and m
        if (freq1[i] == 0 and freq2[i] == 0):
            i = i + 1
            continue

        # If i is a prime factor of n and m
        # If count of i dividing m is more
        # than i dividing n, then power will be 0
        if (freq2[i] > freq1[i]):
            return 0

        # If i is a prime factor of M
        if (freq2[i]):

            # get the maximum power
            maxi = max(maxi, int(freq1[i] // freq2[i]))

        i = i + 1

    return maxi

# Drivers code
n = 48
m = 4
print(getMaximumPower(n, m))

# This code is contributed by Shashank_Sharma
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to get the prime factors
// and its count of times it divides
static void primeFactors(int n, int []freq)
{

    int cnt = 0;

    // Count the number of 2s that divide n
    while (n % 2 == 0)
    {
        cnt++;
        n = n / 2;
    }

    freq[2] = cnt;

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= Math.Sqrt(n); i = i + 2)
    {
        cnt = 0;

        // While i divides n, count i and divide n
        while (n % i == 0)
        {
            cnt++;
            n = n / i;
        }

        freq[i] = cnt;
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        freq[n] = 1;
}

// Function to return the highest power
static int getMaximumPower(int n, int m)
{

    // Initialize two arrays
    int []freq1 = new int[n + 1];int []freq2 = new int[m + 1];

    // Get the prime factors of n and m
    primeFactors(n, freq1);
    primeFactors(m, freq2);

    int maxi = 0;

    // Iterate and find the maximum power
    for (int i = 2; i <= m; i++)
    {

        // If i not a prime factor of n and m
        if (freq1[i] == 0 && freq2[i] == 0)
            continue;

        // If i is a prime factor of n and m
        // If count of i dividing m is more
        // than i dividing n, then power will be 0
        if (freq2[i] > freq1[i])
            return 0;

        // If i is a prime factor of M
        if (freq2[i] != 0)
        {

            // get the maximum power
            maxi = Math.Max(maxi, freq1[i] / freq2[i]);
        }
    }

    return maxi;
}

// Drivers code
public static void Main(String[] args)
{
    int n = 48, m = 4;
    Console.WriteLine(getMaximumPower(n, m));

}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function to get the prime factors
// and its count of times it divides
function primeFactors($n, $freq)
{

    $cnt = 0;

    // Count the number of 2s that divide n
    while ($n % 2 == 0)
    {
        $cnt++;
        $n = floor($n / 2);
    }

    $freq[2] = $cnt;

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for ($i = 3; $i <= sqrt($n); $i = $i + 2)
    {
        $cnt = 0;

        // While i divides n, count i and divide n
        while ($n % $i == 0)
        {
            $cnt++;
            $n = floor($n / $i);
        }

        $freq[$i] = $cnt;
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if ($n > 2)
        $freq[$n] = 1;

    return $freq ;
}

// Function to return the highest power
function getMaximumPower($n, $m)
{

    $freq1 = array_fill(0,$n + 1,0);
    $freq2 = array_fill(0,$m + 1,0);

    // Get the prime factors of n and m
    $freq1 = primeFactors($n, $freq1);
    $freq2 = primeFactors($m, $freq2);

    $maxi = 0;

    // Iterate and find the maximum power
    for ($i = 2; $i <= $m; $i++)
    {

        // If i not a prime factor of n and m
        if ($freq1[$i] == 0 && $freq2[$i] == 0)
            continue;

        // If i is a prime factor of n and m
        // If count of i dividing m is more
        // than i dividing n, then power will be 0
        if ($freq2[$i] > $freq1[$i])
            return 0;

        // If i is a prime factor of M
        if ($freq2[$i])
        {

            // get the maximum power
            $maxi = max($maxi, floor($freq1[$i] / $freq2[$i]));
        }
    }

    return $maxi;
}

    // Drivers code
    $n = 48; $m = 4;
    echo getMaximumPower($n, $m);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get the prime factors
// and its count of times it divides
function primeFactors(n, freq)
{

    var cnt = 0;

    // Count the number of 2s that divide n
    while (n % 2 == 0) {
        cnt++;
        n = n / 2;
    }

    freq[2] = cnt;
    var i;
    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (i = 3; i <= Math.sqrt(n); i = i + 2) {
        cnt = 0;

        // While i divides n, count i and divide n
        while (n % i == 0) {
            cnt++;
            n = n / i;
        }

        freq[i] = cnt;
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        freq[n] = 1;
}

// Function to return the highest power
function getMaximumPower(n, m)
{

    // Initialize two arrays
    var freq1 = new Array(n+1);
    var freq2 = new Array(m+1);

    // Get the prime factors of n and m
    primeFactors(n, freq1);
    primeFactors(m, freq2);

    var maxi = 0;

    // Iterate and find the maximum power
    for(i = 2; i <= m; i++) {

        // If i not a prime factor of n and m
        if (freq1[i] == 0 && freq2[i] == 0)
            continue;

        // If i is a prime factor of n and m
        // If count of i dividing m is more
        // than i dividing n, then power will be 0
        if (freq2[i] > freq1[i])
            return 0;

        // If i is a prime factor of M
        if (freq2[i]) {

            // get the maximum power
            maxi = Math.max(maxi, freq1[i]/freq2[i]);
        }
    }

    return maxi;
}

// Drivers code
    var n = 48, m = 4;
    document.write(getMaximumPower(n, m));

</script>
```

**Output**

```
2
```

**时间复杂度:** O(n log log n)

**辅助空间:** O(最大值(m，n))