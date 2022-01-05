# 检查给定的数字是否是堂兄素数

> 原文:[https://www . geesforgeks . org/check-给定的数字是否是表亲质数/](https://www.geeksforgeeks.org/check-whether-the-given-numbers-are-cousin-prime-or-not/)

给定两个正整数 n1 和 n2，任务是检查两者是否都是表哥素数。如果两个数字都是表亲素数，则打印“是”，否则打印“否”。
[**表亲素数:**](https://en.wikipedia.org/wiki/Cousin_prime) 在数学中，表亲素数是相差 4 的素数。假设“p”是一个质数，如果(p + 4)也是一个质数，那么这两个质数将被称为表亲质数。
100 以下的表亲素数为:

> (3, 7), (7, 11), (13, 17), (19, 23), (37, 41), (43, 47), (67, 71), (79, 83), (97, 101)

**示例:**

```
Input: n1 = 7, n2 = 11
Output: YES
    Both are prime numbers and they differ by 4.

Input: n1 = 5, n2 = 11
Output: NO
    Both are prime numbers but they differ by 6.
```

**方法:**一个**简单的解决方法**是检查两个数是否都是素数并且相差 4。如果它们是素数，相差 4，那么它们将是表亲素数，否则不是。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check Cousin prime

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Returns true if n1 and n2 are Cousin primes
bool isCousinPrime(int n1, int n2)
{
    // Check if they differ by 4 or not
    if (abs(n1 - n2) != 4)
        return false;

    // Check if both are prime number or not
    else
        return (isPrime(n1) && isPrime(n2));
}

// Driver code
int main()
{

    // Get the 2 numbers
    int n1 = 7, n2 = 11;

    // Check the numbers for cousin prime
    if (isCousinPrime(n1, n2))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// JAVA program to check Cousin prime

import java.util.*;

class GFG {

    // Function to check if a number is prime or not
    static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6) {
            if (n % i == 0 || n % (i + 2) == 0) {
                return false;
            }
        }

        return true;
    }

    // Returns true if n1 and n2 are Cousin primes
    static boolean isCousinPrime(int n1, int n2)
    {
        // Check if they differ by 4 or not
        if (Math.abs(n1 - n2) != 4)
            return false;

        // Check if both are prime number or not
        else
            return (isPrime(n1) && isPrime(n2));
    }

    // Driver code
    public static void main(String[] args)
    {

        // Get the 2 numbers
        int n1 = 7, n2 = 11;

        // Check the numbers for cousin prime
        if (isCousinPrime(n1, n2))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 计算机编程语言

```
# Python program to check Cousin prime

import math

# Function to check whether a  
# number is prime or not
def isPrime( n ):

    # Corner cases
    if n <= 1:
        return False
    if n <= 3:
        return True

    # This is checked so that we 
    # can skip middle five numbers
    # in below loop
    if n % 2 == 0 or n % 3 == 0:
        return False

    for i in range(5, int(math.sqrt(n)+1), 6):
        if n % i == 0 or n %(i + 2) == 0:
            return False

    return True

# Returns true if n1 and n2 are Cousin primes
def isCousinPrime( n1,  n2) :

    # Check if they differ by 4 or not
    if(not (abs(n1-n2)== 4)):
        return False

    # Check if both are prime number or not
    else:
        return (isPrime(n1) and isPrime(n2))

# Driver code

# Get the 2 numbers
n1 = 7
n2 = 11

# Check the numbers for cousin prime
if (isCousinPrime(n1, n2)):
    print("YES")
else:
    print("NO")

```

## C#

```
// C# Code for Cousin Prime Numbers

using System;

class GFG {

    // Function to check if the given
    // number is prime or not
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Returns true if n1 and n2 are Cousin primes
    static bool isCousinPrime(int n1, int n2)
    {
        // Check if the numbers differ by 4 or not
        if (Math.Abs(n1 - n2) != 4) {
            return false;
        }
        else {
            return (isPrime(n1) && isPrime(n2));
        }
    }

    // Driver program
    public static void Main()
    {

        // Get the 2 numbers
        int n1 = 7, n2 = 11;

        // Check the numbers for cousin prime
        if (isCousinPrime(n1, n2))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PhP program to check Cousin prime

// Function to check if the given
// Number is prime or not
function isPrime($n)
{

    // Corner cases
    if ($n <= 1) return false;
    if ($n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
            return false;

    return true;
}

// Returns true if n1 and n2 are Cousin primes
function isCousinPrime($n1, $n2)
{
    // Check if the given number differ by 4 or not
    if(abs($n1-$n2)!=4)
        return false;

    // Check if both numbers are prime or not
    else
        return (isPrime($n1) && isPrime($n2));
}

// Driver code

// Get the 2 numbers
$n1 = 7;
$n2 = 11;

    // Check the numbers for cousin prime
if (isCousinPrime($n1, $n2))
    echo "YES";
else
    echo "NO";

?>
```

## java 描述语言

```
<script>

// Javascript program to check Cousin prime

// Function to check if a number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (var i = 5; i * i <= n; i = i + 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Returns true if n1 and n2 are Cousin primes
function isCousinPrime(n1, n2)
{
    // Check if they differ by 4 or not
    if(Math.abs(n1 - n2) != 4)
        return false;

    // Check if both are prime number or not
    else
        return (isPrime(n1) && isPrime(n2));
}

// Driver code
// Get the 2 numbers
var n1 = 7, n2 = 11;
// Check the numbers for cousin prime
if (isCousinPrime(n1, n2))
    document.write( "YES");
else
    document.write( "NO" );

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(n1 <sup>1/2</sup> )*

***辅助空间:** O(1)*