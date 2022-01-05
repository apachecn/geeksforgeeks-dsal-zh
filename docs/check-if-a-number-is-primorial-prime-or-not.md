# 检查一个数字是否是 Primorial Prime

> 原文:[https://www . geesforgeks . org/check-a-number-if-primorial-prime-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-primorial-prime-or-not/)

给定一个正数，任务是检查 N 是否是素数。如果 N 是素数，则打印“是”，否则打印“否”
[**【素数:**](https://en.wikipedia.org/wiki/Primorial_prime) 在数学中，素数是形式为 **p <sub>n</sub> # + 1** 或**p<sub>N</sub>#–1**的素数，其中 **p <sub>n</sub> #** 是**p**的素数
**示例** :**** 

```
Input : N = 5
Output : YES
5 is Primorial prime of the form p<sub>n - 1</sub>  
for n=2, Primorial is 2*3 = 6
and 6-1 =5.

Input : N = 31
Output : YES
31 is Primorial prime of the form p<sub>n + 1</sub>  
for n=3, Primorial is 2*3*5 = 30
and 30+1 = 31.
```

前几个原始素数是:

> 2、3、5、7、29、31、211、2309、2311、30029

**先决条件:**

*   [原始](https://www.geeksforgeeks.org/primorial-of-a-number/)
*   [厄拉多塞筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

**进场:**

1.  使用厄拉多塞筛生成该范围内的所有素数。
2.  检查 n 是否为质数，如果 n 不是质数，则打印否
3.  否则，从第一个质数(即 2)开始乘以下一个质数，并继续检查*乘积+ 1 = n* 或乘积–1 = n
4.  如果*积+1=n* 或*积-1=n* ，则 n 是 Primorial Prime，否则不是。

以下是上述方法的实现:

## C++

```
// CPP program to check Primorial Prime

#include <bits/stdc++.h>
using namespace std;

#define MAX 10000

vector<int> arr;

bool prime[MAX];

// Function to generate prime numbers
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // make all entries of boolean array 'prime'
    // as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.

    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p < MAX; p++) {
        // If prime[p] is not changed, then it is a prime

        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }

    // store all prime numbers
    // to vector 'arr'
    for (int p = 2; p < MAX; p++)
        if (prime[p])
            arr.push_back(p);
}

// Function to check the number for Primorial prime
bool isPrimorialPrime(long n)
{
    // If n is not prime Number
    // return false
    if (!prime[n])
        return false;

    long long product = 1;
    int i = 0;

    while (product < n) {

        // Multiply next prime number
        // and check if product + 1 = n or Product-1 =n
        // holds or not
        product = product * arr[i];

        if (product + 1 == n || product - 1 == n)
            return true;

        i++;
    }

    return false;
}

// Driver code
int main()
{
    SieveOfEratosthenes();

    long n = 31;

    // Check if n is Primorial Prime
    if (isPrimorialPrime(n))
        cout << "YES\n";
    else
        cout << "NO\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check Primorial prime

import java.util.*;

class GFG {

    static final int MAX = 1000000;
    static Vector<Integer> arr = new Vector<Integer>();
    static boolean[] prime = new boolean[MAX];

    // Function to get the prime numbers
    static void SieveOfEratosthenes()
    {

        // make all entries of boolean array 'prime'
        // as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.

        for (int i = 0; i < MAX; i++)
            prime[i] = true;

        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p)
                    prime[i] = false;
            }
        }

        // store all prime numbers
        // to vector 'arr'
        for (int p = 2; p < MAX; p++)
            if (prime[p])
                arr.add(p);
    }

    // Function to check the number for Primorial prime
    static boolean isPrimorialPrime(int n)
    {
        // If n is not prime
        // Then return false
        if (!prime[n])
            return false;

        long product = 1;
        int i = 0;
        while (product < n) {

            // Multiply next prime number
            // and check if product + 1 = n or product -1=n
            // holds or not
            product = product * arr.get(i);

            if (product + 1 == n || product - 1 == n)
                return true;

            i++;
        }

        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        SieveOfEratosthenes();

        int n = 31;

        if (isPrimorialPrime(n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 Program to check Primorial Prime

# from math lib import sqrt method
from math import sqrt

MAX = 100000

# Create a boolean array "prime[0..n]"
# and initialize make all entries of
# boolean array 'prime' as true.
# A value in prime[i] will finally be
# false if i is Not a prime, else true.
prime = [True] * MAX

arr = []

# Utility function to generate
# prime numbers
def SieveOfEratosthenes() :

    for p in range(2, int(sqrt(MAX)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True :

            # Update all multiples of p
            for i in range(p * 2 , MAX, p) :
                prime[i] = False

    # store all prime numbers
    # to list 'arr'
    for p in range(2, MAX) :

        if prime[p] :
            arr.append(p)

# Function to check the number
# for Primorial prime
def isPrimorialPrime(n) :

    # If n is not prime Number
    # return false
    if not prime[n] :
        return False

    product, i = 1, 0

    # Multiply next prime number
    # and check if product + 1 = n
    # or Product-1 = n holds or not
    while product < n :

        product *= arr[i]

        if product + 1 == n or product - 1 == n :
            return True

        i += 1

    return False

# Driver code
if __name__ == "__main__" :

    SieveOfEratosthenes()

    n = 31

    # Check if n is Primorial Prime
    if (isPrimorialPrime(n)) :
        print("YES")
    else :
        print("NO")

# This code is contributed by ANKITRAI1
```

## C#

```
// c# program to check Primorial prime
using System;
using System.Collections.Generic;

public class GFG
{

    public const int MAX = 1000000;
    public static List<int> arr = new List<int>();
    public static bool[] prime = new bool[MAX];

    // Function to get the prime numbers
    public static void SieveOfEratosthenes()
    {

        // make all entries of boolean array 'prime'
        // as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.

        for (int i = 0; i < MAX; i++)
        {
            prime[i] = true;
        }

        for (int p = 2; p * p < MAX; p++)
        {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p)
                {
                    prime[i] = false;
                }
            }
        }

        // store all prime numbers
        // to vector 'arr'
        for (int p = 2; p < MAX; p++)
        {
            if (prime[p])
            {
                arr.Add(p);
            }
        }
    }

    // Function to check the number for Primorial prime
    public static bool isPrimorialPrime(int n)
    {
        // If n is not prime
        // Then return false
        if (!prime[n])
        {
            return false;
        }

        long product = 1;
        int i = 0;
        while (product < n)
        {

            // Multiply next prime number
            // and check if product + 1 = n or product -1=n
            // holds or not
            product = product * arr[i];

            if (product + 1 == n || product - 1 == n)
            {
                return true;
            }

            i++;
        }

        return false;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        SieveOfEratosthenes();

        int n = 31;

        if (isPrimorialPrime(n))
        {
            Console.WriteLine("YES");
        }
        else
        {
            Console.WriteLine("NO");
        }
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check Primorial Prime
$MAX = 100000;

// Create a boolean array "prime[0..n]"
// and initialize make all entries of
// boolean array 'prime' as true.
// A value in prime[i] will finally be
// false if i is Not a prime, else true.
$prime = array_fill(0, $MAX, true);

$arr = array();

// Utility function to generate
// prime numbers
function SieveOfEratosthenes()
{
    global $MAX, $prime, $arr;
    for($p = 2; $p <= (int)(sqrt($MAX)); $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)

            // Update all multiples of p
            for ($i = $p * 2; $i < $MAX; $i += $p)
                $prime[$i] = false;
    }

    // store all prime numbers
    // to list 'arr'
    for ($p = 2; $p < $MAX; $p++)
        if ($prime[$p])
            array_push($arr, $p);
}

// Function to check the number
// for Primorial prime
function isPrimorialPrime($n)
{
    global $MAX, $prime, $arr;

    // If n is not prime Number
    // return false
    if(!$prime[$n])
        return false;

    $product = 1;
    $i = 0;

    // Multiply next prime number
    // and check if product + 1 = n
    // or Product-1 = n holds or not
    while ($product < $n)
    {
        $product *= $arr[$i];

        if ($product + 1 == $n ||
            $product - 1 == $n )
            return true;

        $i += 1;
    }

    return false;
}

// Driver code
SieveOfEratosthenes();

$n = 31;

// Check if n is Primorial Prime
if (isPrimorialPrime($n))
    print("YES");
else
    print("NO");

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to check Primorial Prime

var MAX = 10000;

var arr = [];

var prime = Array(MAX).fill(true);

// Function to generate prime numbers
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // make all entries of boolean array 'prime'
    // as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.

    for (var p = 2; p * p < MAX; p++) {
        // If prime[p] is not changed, then it is a prime

        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }

    // store all prime numbers
    // to vector 'arr'
    for (var p = 2; p < MAX; p++)
        if (prime[p])
            arr.push(p);
}

// Function to check the number for Primorial prime
function isPrimorialPrime(n)
{
    // If n is not prime Number
    // return false
    if (!prime[n])
        return false;

    var product = 1;
    var i = 0;

    while (product < n) {

        // Multiply next prime number
        // and check if product + 1 = n or Product-1 =n
        // holds or not
        product = product * arr[i];

        if (product + 1 == n || product - 1 == n)
            return true;

        i++;
    }

    return false;
}

// Driver code
SieveOfEratosthenes();
var n = 31;
// Check if n is Primorial Prime
if (isPrimorialPrime(n))
    document.write( "YES");
else
    document.write("NO");

</script>
```

**Output:** 

```
YES
```