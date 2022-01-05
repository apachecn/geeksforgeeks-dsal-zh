# 求一个数与其最大质因数之和

> 原文:[https://www . geeksforgeeks . org/find-一个数的和及其最大质因数/](https://www.geeksforgeeks.org/find-sum-of-a-number-and-its-maximum-prime-factor/)

给定一个整数 **N** ，任务是求 **N** 的和及其最大质因数。
**例:**

> **输入:**19
> T3】输出:38
> 19 的最大质因数为 19。
> 因此，19 + 19 = 38
> **输入:** 8
> **输出:** 10
> 8 + 2 = 10

**逼近:**找到该数的[最大质因数](https://www.geeksforgeeks.org/find-largest-prime-factor-number/)存入 **maxPrimeFact** 然后打印 **N + maxPrimeFact** 的值。
以下是上述方法的实施:

## C++

```
// C++ program to find sum of n and
// it's largest prime factor
#include <cmath>
#include <iostream>
using namespace std;

// Function to return the sum of n and
// it's largest prime factor
int maxPrimeFactors(int n)
{
    int num = n;

    // Initialise maxPrime to -1.
    int maxPrime = -1;

    while (n % 2 == 0) {
        maxPrime = 2;
        n /= 2;
    }

    // n must be odd at this point, thus skip
    // the even numbers and iterate only odd numbers
    for (int i = 3; i <= sqrt(n); i += 2) {
        while (n % i == 0) {
            maxPrime = i;
            n = n / i;
        }
    }

    // This condition is to handle the case
    // when n is a prime number greater  than 2
    if (n > 2)
        maxPrime = n;

    // finally return the sum.
    int sum = maxPrime + num;
    return sum;
}

// Driver Program to check the above function.
int main()
{
    int n = 19;

    cout << maxPrimeFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of n and
// it's largest prime factor
import java.io.*;

class GFG
{

// Function to return the sum of n
// and it's largest prime factor
static int maxPrimeFactors(int n)
{
int num = n;

// Initialise maxPrime to -1.
int maxPrime = -1;

while (n % 2 == 0)
{
maxPrime = 2;
n /= 2;
}

// n must be odd at this point,
// thus skip the even numbers and
// iterate only odd numbers
for (int i = 3; i <= Math.sqrt(n); i += 2) {

    while (n % i == 0) {
        maxPrime = i; n = n / i;
        }

}
        // This condition is to handle the case
        // when n is a prime number greater than 2
        if (n > 2) {
            maxPrime = n;
        }
// finally return the sum.
int sum = maxPrime + num;
return sum;
}

// Driver Code
public static void main (String[] args)
{
int n = 19;

System.out.println(maxPrimeFactors(n));
}
}
// This code is contributed by anuj_67
```

## 蟒蛇 3

```
# Python 3 program to find sum of n and
# it's largest prime factor
from math import sqrt

# Function to return the sum of n and
# it's largest prime factor
def maxPrimeFactors(n):
    num = n

    # Initialise maxPrime to -1.
    maxPrime = -1;

    while (n % 2 == 0):
        maxPrime = 2
        n = n / 2

    # n must be odd at this point, thus skip
    # the even numbers and iterate only odd numbers
    p = int(sqrt(n) + 1)
    for i in range(3, p, 2):
        while (n % i == 0):
            maxPrime = i
            n = n / i

    # This condition is to handle the case
    # when n is a prime number greater than 2
    if (n > 2):
        maxPrime = n

    # finally return the sum.
    sum = maxPrime + num
    return sum

# Driver Code
if __name__ == '__main__':
    n = 19

    print(maxPrimeFactors(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum of n and
// it's largest prime factor
using System;

class GFG
{
// Function to return the sum of n
// and it's largest prime factor
static int maxPrimeFactors(int n)
{
int num = n;

// Initialise maxPrime to -1.
int maxPrime = -1;

while (n % 2 == 0)
{
    maxPrime = 2;
    n /= 2;
}

// n must be odd at this point,
// thus skip the even numbers and
// iterate only odd numbers
for (int i = 3;
         i <= Math.Sqrt(n); i += 2)
{

    while (n % i == 0)
    {
        maxPrime = i; n = n / i;
    }

}

// This condition is to handle the case
// when n is a prime number greater than 2
if (n > 2)
{
    maxPrime = n;
}

// finally return the sum.
int sum = maxPrime + num;
return sum;
}

// Driver Code
static void Main ()
{
    int n = 19;

    Console.WriteLine(maxPrimeFactors(n));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of n and
// it's largest prime factor

// Function to return the sum of n
// and it's largest prime factor
function maxPrimeFactors($n)
{
    $num = $n;

    // Initialise maxPrime to -1.
    $maxPrime = -1;

    while ($n % 2 == 0)
    {
        $maxPrime = 2;
        $n /= 2;
    }

    // n must be odd at this point,
    // thus skip the even numbers
    // and iterate only odd numbers
    for ($i = 3; $i <= sqrt($n); $i += 2)
    {
        while ($n % $i == 0)
        {
            $maxPrime = $i;
            $n = $n / $i;
        }
    }

    // This condition is to handle the case
    // when n is a prime number greater than 2
    if ($n > 2)
        $maxPrime = $n;

    // finally return the sum.
    $sum = $maxPrime + $num;
    return $sum;
}

// Driver Code
$n = 19;

echo maxPrimeFactors($n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of n and
// it's largest prime factor

// Function to return the sum of n
// and it's largest prime factor
function maxPrimeFactors(n)
{
    var num = n;

    // Initialise maxPrime to -1.
    var maxPrime = -1;

    while (n % 2 == 0)
    {
        maxPrime = 2;
        n = parseInt(n/2);
    }

    // n must be odd at this point,
    // thus skip the even numbers and
    // iterate only odd numbers
    for (var i = 3; i <= parseInt(Math.sqrt(n)); i += 2)
    {

        while (n % i == 0) {
            maxPrime = i;
            n = parseInt(n / i);
        }

    }
            // This condition is to handle the case
            // when n is a prime number greater than 2
            if (n > 2) {
                maxPrime = n;
            }
    // finally return the sum.
    var sum = maxPrime + num;
    return sum;
}

// Driver Code

var n = 19;

document.write(maxPrimeFactors(n));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
38
```