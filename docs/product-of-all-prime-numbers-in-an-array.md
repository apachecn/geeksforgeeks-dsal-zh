# 数组中所有素数的乘积

> 原文:[https://www . geeksforgeeks . org/全素数积数组/](https://www.geeksforgeeks.org/product-of-all-prime-numbers-in-an-array/)

给定一个由 N 个正整数组成的数组 arr[]。任务是编写一个程序来寻找给定数组的所有素数的乘积。
**例** :

> **输入** : arr[] = {1，3，4，5，7}
> **输出** : 105
> 有三个素数，3，5，7 的乘积= 105。
> **输入** : arr[] = {1，2，3，4，5，6，7}
> **输出** : 210

**天真方法:**一个简单的解决方法是遍历数组，不断检查每个元素是否是素数，同时计算素数元素的乘积。
**高效方法:**使用厄拉多塞的[筛生成数组中最大元素的所有素数，并将它们存储在哈希中。现在遍历数组，用筛子找出那些质数的乘积。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find product of
// primes in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find the product of prime numbers
// in the given array
int primeProduct(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Product all primes in arr[]
    int prod = 1;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            prod *= arr[i];

    return prod;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << primeProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of
// primes in given array.
import java.util.*;

class GFG
{

// Function to find the product of prime numbers
// in the given array
static int primeProduct(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = Arrays.stream(arr).max().getAsInt();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    Vector<Boolean> prime = new Vector<Boolean>(max_val + 1);
    for(int i = 0; i < max_val + 1; i++)
        prime.add(i, Boolean.TRUE);

    // Remaining part of SIEVE
    prime.add(0, Boolean.FALSE);
    prime.add(1, Boolean.FALSE);
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime.get(p) == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime.add(i, Boolean.FALSE);
        }
    }

    // Product all primes in arr[]
    int prod = 1;
    for (int i = 0; i < n; i++)
        if (prime.get(arr[i]))
            prod *= arr[i];

    return prod;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;

    System.out.print(primeProduct(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find product of
# primes in given array
import math as mt

# function to find the product of prime
# numbers in the given array
def primeProduct(arr, n):

    # find the maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # remaining part of SIEVE
    prime[0] = False
    prime[1] = False

    for p in range(mt.ceil(mt.sqrt(max_val))):

        # Remaining part of SIEVE

        # if prime[p] is not changed,
        # than it is prime
        if prime[p]:

            # update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i] = False

    # product all primes in arr[]
    prod = 1

    for i in range(n):
        if prime[arr[i]]:
            prod *= arr[i]

    return prod

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7]

n = len(arr)

print(primeProduct(arr, n))

# This code is contributed
# by Mohit kumar 29

```

## C#

```
// C# program to find product of
// primes in given array.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to find the product of prime numbers
// in the given array
static int primeProduct(int []arr, int n)
{
    // Find maximum value in the array
    int max_val = arr.Max();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    List<bool> prime = new List<bool>(max_val + 1);
    for(int i = 0; i < max_val + 1; i++)
        prime.Insert(i, true);

    // Remaining part of SIEVE
    prime.Insert(0, false);
    prime.Insert(1, false);
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime.Insert(i, false);
        }
    }

    // Product all primes in arr[]
    int prod = 1;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            prod *= arr[i];

    return prod;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;

    Console.Write(primeProduct(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product of
// primes in given array.

// Function to find the product of
// prime numbers in the given array
function primeProduct($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, True);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $max_val; $i += $p)
                $prime[$i]= false;
        }
    }

    // Product all primes in arr[]
    $prod = 1;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$arr[$i]])
            $prod *= $arr[$i];

    return $prod;
}

// Driver code
$arr = array(1, 2, 3, 4, 5, 6, 7);
$n = sizeof($arr);

echo(primeProduct($arr, $n));

// This code contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
// Javascript program to find product of
// primes in given array.

// Function to find the product of
// prime numbers in the given array
function primeProduct(arr, n)
{
    // Find maximum value in the array
    let max_val = arr.sort((a, b) => b - a)[0];

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (let p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (let i = p * 2;
                i <= max_val; i += p)
                prime[i]= false;
        }
    }

    // Product all primes in arr[]
    let prod = 1;
    for (let i = 0; i < n; i++)
        if (prime[arr[i]])
            prod *= arr[i];

    return prod;
}

// Driver code
let arr = new Array(1, 2, 3, 4, 5, 6, 7);
let n = arr.length;

document.write(primeProduct(arr, n));

// This code contributed by _Saurabh_Jaiswal.
</script>
```

**Output:** 

```
210
```