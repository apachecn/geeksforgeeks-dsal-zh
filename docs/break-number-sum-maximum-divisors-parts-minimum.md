# 分解一个数，使所有部分的最大除数之和最小

> 原文:[https://www . geesforgeks . org/break-number-sum-maximum-dividers-parts-minimum/](https://www.geeksforgeeks.org/break-number-sum-maximum-divisors-parts-minimum/)

我们需要拆分一个数 n，使得所有部分的最大除数之和最小。

**示例:**

```
Input:  n = 27
Output: Minimum sum of maximum
        divisors of parts = 3
Explanation : We can split 27 as 
follows: 27 =  13 + 11 + 3,
Maximum divisor of 13 = 1,
                   11 = 1,
                   3 = 1.
Answer = 3 (1 + 1 + 1).

Input : n = 4
Output: Minimum sum of maximum
        divisors of parts = 2
Explanation : We can write 4 = 2 + 2
Maximum divisor of 2 = 1,
So answer is 1 + 1 = 2.
```

我们需要最小化最大除数。很明显，如果 N 是素数，最大除数= 1。如果该数不是质数，则该数至少应为 2。

根据[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)，每个偶数都可以表示为两个素数之和。对于我们的问题将有两种情况:

1)当数为偶数时，可以表示为两个素数之和，我们的答案将是 2，因为一个素数的最大除数是 1。
2)当数为奇数时，也可以写成素数之和，**n = 2+(n-2)；**如果(n-2)是素数(答案= 2)，则为。详见[奇数为素数之和](https://www.geeksforgeeks.org/express-odd-number-sum-prime-numbers/)。
**n = 3+(n-3)；** (n-3)是偶数，是两个素数之和(答案= 3)。

下面是这个方法的实现。

## C++

```
// CPP program to break a number such
// that sum of maximum divisors of all
// parts is minimum
#include <iostream>
using namespace std;

// Function to check if a number is
// prime or not.
bool isPrime(int n)
{
    int i = 2;
    while (i * i <= n) {
        if (n % i == 0)
            return false;
        i++;
    }
    return true;
}

int minimumSum(int n)
{
    if (isPrime(n))
        return 1;

    // If n is an even number (we can
    // write it as sum of two primes)
    if (n % 2 == 0)
        return 2;

    // If n is odd and n-2 is prime.
    if (isPrime(n - 2))
        return 2;

    // If n is odd, n-3 must be even.
    return 3;
}

// Driver code
int main()
{
    int n = 27;
    cout << minimumSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Break a number such that sum
// of maximum divisors of all parts is minimum
import java.util.*;

class GFG {

    // Function to check if a number is
    // prime or not.
    static boolean isPrime(int n)
    {
        int i = 2;

        while (i * i <= n) {
            if (n % i == 0)
                return false;
            i++;
        }
        return true;
    }

    static int minimumSum(int n)
    {
        if (isPrime(n))
            return 1;

        // If n is an even number (we can
        // write it as sum of two primes)
        if (n % 2 == 0)
            return 2;

        // If n is odd and n-2 is prime.
        if (isPrime(n - 2))
            return 2;

        // If n is odd, n-3 must be even.
        return 3;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 4;
        System.out.println(minimumSum(n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to break a number
# such that sum of maximum divisors
# of all parts is minimum

# Function to check if a number is
# prime or not.
def isPrime( n):
    i = 2

    while (i * i <= n):

        if (n % i == 0):
            return False
        i+= 1

    return True

def minimumSum( n):

    if (isPrime(n)):
        return 1

    # If n is an even number (we can
    # write it as sum of two primes)
    if (n % 2 == 0):
        return 2

    # If n is odd and n-2 is prime.
    if (isPrime(n - 2)):
        return 2

    # If n is odd, n-3 must be even.
    return 3

# Driver code
n = 27
print(minimumSum(n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# Code for Break a number
// such that sum of maximum
// divisors of all parts is minimum
using System;

class GFG {

    // Function to check if a number is
    // prime or not.
    static bool isPrime(int n)
    {
        int i = 2;

        while (i * i <= n) {
            if (n % i == 0)
                return false;
            i++;
        }
        return true;
    }

    static int minimumSum(int n)
    {
        if (isPrime(n))
            return 1;

        // If n is an even number (we can
        // write it as sum of two primes)
        if (n % 2 == 0)
            return 2;

        // If n is odd and n-2 is prime.
        if (isPrime(n - 2))
            return 2;

        // If n is odd, n-3 must be even.
        return 3;
    }

    // Driver program
    public static void Main()
    {
        int n = 27;
        Console.WriteLine(minimumSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to break a number
// such that sum of maximum
// divisors of all parts is minimum

// Function to check if a
// number is prime or not.
function isPrime($n)
{
    $i = 2;
    while ($i * $i <= $n)
    {
        if ($n % $i == 0)
            return false;
        $i++;
    }
    return true;
}

function minimumSum($n)
{
    if (isPrime($n))    
        return 1;

    // If n is an even
    // number (we can
    // write it as sum
    // of two primes)
    if ($n % 2 == 0)
        return 2;

    // If n is odd and
    // n - 2 is prime.
    if (isPrime($n - 2))
        return 2;

    // If n is odd,
    // n - 3 must be even.
    return 3;
}

// Driver code
$n = 27;
echo minimumSum($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to break a number
// such that sum of maximum divisors of
// all parts is minimum

// Function to check if a number is
// prime or not.
function isPrime(n)
{
    let i = 2;

    while (i * i <= n)
    {
        if (n % i == 0)
            return false;

        i++;
    }
    return true;
}

function minimumSum(n)
{
    if (isPrime(n))
        return 1;

    // If n is an even number (we can
    // write it as sum of two primes)
    if (n % 2 == 0)
        return 2;

    // If n is odd and n-2 is prime.
    if (isPrime(n - 2))
        return 2;

    // If n is odd, n-3 must be even.
    return 3;
}

// Driver code
let n = 27;

document.write(minimumSum(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
    3
```