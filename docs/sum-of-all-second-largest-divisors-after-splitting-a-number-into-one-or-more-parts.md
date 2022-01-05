# 将一个数分成一个或多个部分后所有第二大除数的和

> 原文:[https://www . geeksforgeeks . org/将一个数拆分成一个或多个部分后的所有第二大除数之和/](https://www.geeksforgeeks.org/sum-of-all-second-largest-divisors-after-splitting-a-number-into-one-or-more-parts/)

给定一个整数 **N** ( 2 < = N < = 10^9)，将数字分成一个或多个部分(可能没有)，其中每个部分必须大于 1。任务是找到所有分裂数的第二大除数的最小可能和。
**例:**

```
Input : N = 27 
Output : 3
Explanation : Split the given number into 19, 5, 3\. Second largest 
divisor of each number is 1\. So, sum is 3.

Input : N = 19
Output : 1
Explanation : Don't make any splits. Second largest divisor of 19 
is 1\. So, sum is 1 
```

**方法:**
这个想法基于[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)。

1.  当数是质数时，那么答案将是 1。
2.  当一个数为偶数时，它总是可以表示为两个素数之和。所以，答案会是 2。
3.  当数字是奇数时，
    *   当 N-2 是素数时，那么这个数可以表示为 2 个素数之和，即 2 和 N-2，那么答案就是 2。
    *   否则，答案永远是 3。

以下是上述方法的实现:

## C++

```
// CPP program to find sum of all second largest divisor
// after splitting a number into one or more parts
#include <bits/stdc++.h>
using namespace std;

// Function to find a number is prime or not
bool prime(int n)
{
    if (n == 1)
        return false;

    // If there is any divisor
    for (int i = 2; i * i <= n; ++i)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find the sum of all second largest divisor
// after splitting a number into one or more parts
int Min_Sum(int n)
{
    // If number is prime
    if (prime(n))
        return 1;

    // If n is even
    if (n % 2 == 0)
        return 2;

    // If the number is odd
    else {

        // If N-2 is prime
        if (prime(n - 2))
            return 2;

        // There exists 3 primes x1, x2, x3
        // such that x1 + x2 + x3 = n
        else
            return 3;
    }
}

// Driver code
int main()
{
    int n = 27;

    // Function call
    cout << Min_Sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Sum of all second largest
// divisors after splitting a number into one or more parts
import java.io.*;

class GFG {

// Function to find a number is prime or not
static boolean prime(int n)
{
    if (n == 1)
        return false;

    // If there is any divisor
    for (int i = 2; i * i <= n; ++i)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find the sum of all second largest divisor
// after splitting a number into one or more parts
static int Min_Sum(int n)
{
    // If number is prime
    if (prime(n))
        return 1;

    // If n is even
    if (n % 2 == 0)
        return 2;

    // If the number is odd
    else {

        // If N-2 is prime
        if (prime(n - 2))
            return 2;

        // There exists 3 primes x1, x2, x3
        // such that x1 + x2 + x3 = n
        else
            return 3;
    }
}

// Driver code

    public static void main (String[] args) {
    int n = 27;

    // Function call
    System.out.println( Min_Sum(n));
    }
}

// This code is contributed by anuj_6
```

## 蟒蛇 3

```
# Python 3 program to find sum of all second largest divisor
# after splitting a number into one or more parts

from math import sqrt
# Function to find a number is prime or not
def prime(n):
    if (n == 1):
        return False

    # If there is any divisor
    for i in range(2,int(sqrt(n))+1,1):
        if (n % i == 0):
            return False

    return True

# Function to find the sum of all second largest divisor
# after splitting a number into one or more parts
def Min_Sum(n):
    # If number is prime
    if (prime(n)):
        return 1

    # If n is even
    if (n % 2 == 0):
        return 2

    # If the number is odd
    else:
        # If N-2 is prime
        if (prime(n - 2)):
            return 2

        # There exists 3 primes x1, x2, x3
        # such that x1 + x2 + x3 = n
        else:
            return 3

# Driver code
if __name__ == '__main__':
    n = 27

    # Function call
    print(Min_Sum(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to Sum of all second largest
// divisors after splitting a number into one or more parts
using System;

class GFG
{

// Function to find a number is prime or not
static bool prime(int n)
{
    if (n == 1)
        return false;

    // If there is any divisor
    for (int i = 2; i * i <= n; ++i)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find the sum of all second largest divisor
// after splitting a number into one or more parts
static int Min_Sum(int n)
{
    // If number is prime
    if (prime(n))
        return 1;

    // If n is even
    if (n % 2 == 0)
        return 2;

    // If the number is odd
    else {

        // If N-2 is prime
        if (prime(n - 2))
            return 2;

        // There exists 3 primes x1, x2, x3
        // such that x1 + x2 + x3 = n
        else
            return 3;
    }
}

// Driver code
public static void Main ()
{
    int n = 27;

    // Function call
    Console.WriteLine( Min_Sum(n));
}
}

// This code is contributed by anuj_6
```

## java 描述语言

```
<script>
// Javascript program to find sum of all second largest divisor
// after splitting a number into one or more parts

// Function to find a number is prime or not
function prime(n)
{
    if (n == 1)
        return false;

    // If there is any divisor
    for (let i = 2; i * i <= n; ++i)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find the sum of all second largest divisor
// after splitting a number into one or more parts
function Min_Sum(n)
{
    // If number is prime
    if (prime(n))
        return 1;

    // If n is even
    if (n % 2 == 0)
        return 2;

    // If the number is odd
    else {

        // If N-2 is prime
        if (prime(n - 2))
            return 2;

        // There exists 3 primes x1, x2, x3
        // such that x1 + x2 + x3 = n
        else
            return 3;
    }
}

// Driver code
    let n = 27;

    // Function call
    document.write(Min_Sum(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(sqrt(N))