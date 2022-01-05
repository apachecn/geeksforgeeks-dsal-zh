# 找出数组中的素数 K，使得(A[i] % K)最大

> 原文:[https://www . geesforgeks . org/find-质数-数组中的 k-so-ai-k-is-maximum/](https://www.geeksforgeeks.org/find-prime-number-k-in-an-array-such-that-ai-k-is-maximum/)

给定一个由 **n** 个整数组成的数组 **arr[]** 。任务是从阵列中找到一个元素 **K** 这样

1.  **K** 为**质数**。
2.  并且， **arr[i] % K** 是所有有效的 **i** 在所有可能的 **K** 值中的最大值

如果数组中没有质数，则打印 **-1** 。
**例:**

> **输入:** arr[] = {2，10，15，7，6，8，13}
> **输出:** 13
> 2，7，13 是数组中仅有的素数。
> arr[I]% 2 的最大可能值为 1，即 15 % 2 = 1。
> 为 7，为 6 % 7 = 6
> 为 13，10 % 13 = 10(最大可能)
> **输入:** arr[] = {23，13，6，2，15，18，8}
> **输出:** 23

**方法:**为了最大化 **arr[i] % K** 的值， **K** 必须是数组中的最大素数， **arr[i]** 必须是数组中小于 **K** 的最大元素。所以，现在问题简化为从数组中找到最大素数。为了做到这一点，

1.  首先，使用[筛](https://www.geeksforgeeks.org/sieve-eratosthenes-0n-time-complexity/)从数组中找出所有小于或等于最大元素的素数。
2.  然后，从数组中找到最大素数并打印出来。如果数组中没有质数，则打印-1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required
// prime number from the array
int getPrime(int arr[], int n)
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

    // To store the maximum prime number
    int maximum = -1;
    for (int i = 0; i < n; i++) {

        // If current element is prime
        // then update the maximum prime
        if (prime[arr[i]])
            maximum = max(maximum, arr[i]);
    }

    // Return the maximum prime
    // number from the array
    return maximum;
}

// Driver code
int main()
{
    int arr[] = { 2, 10, 15, 7, 6, 8, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getPrime(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the required
// prime number from the array
static int getPrime(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = Arrays.stream(arr).max().getAsInt();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    Vector<Boolean> prime = new Vector<>(max_val + 1);
    for(int i = 0; i < max_val + 1; i++)
        prime.add(i,Boolean.TRUE);

    // Remaining part of SIEVE
    prime.add(1,Boolean.FALSE);
    prime.add(2,Boolean.FALSE);
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime.get(p) == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime.add(i,Boolean.FALSE);
        }
    }

    // To store the maximum prime number
    int maximum = -1;
    for (int i = 0; i < n; i++)
    {

        // If current element is prime
        // then update the maximum prime
        if (prime.get(arr[i]))
        {
            maximum = Math.max(maximum, arr[i]);
        }

    }

    // Return the maximum prime
    // number from the array
    return maximum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 10, 15, 7, 6, 8, 13 };
    int n = arr.length;

    System.out.println(getPrime(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function to return the required
# prime number from the array
def getPrime(arr, n):

    # Find maximum value in the array
    max_val = arr[0]
    for i in range(len(arr)):

        # USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        # THAN OR EQUAL TO max_val
        # Create a boolean array "prime[0..n]". A
        # value in prime[i] will finally be false
        # if i is Not a prime, else true.
        if(arr[i] > max_val):
            max_val = arr[i]

    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, int(sqrt(max_val)) + 1, 1):

        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i] = False

    # To store the maximum prime number
    maximum = -1
    for i in range(n):

        # If current element is prime
        # then update the maximum prime
        if (prime[arr[i]]):
            maximum = max(maximum, arr[i])

    # Return the maximum prime
    # number from the array
    return maximum

# Driver code
if __name__ == '__main__':
    arr = [2, 10, 15, 7, 6, 8, 13]
    n = len(arr)

    print(getPrime(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to return the required
// prime number from the array
static int getPrime(int []arr, int n)
{
    // Find maximum value in the array
    int max_val = arr.Max();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    List<Boolean> prime = new List<Boolean>(max_val + 1);
    for(int i = 0; i < max_val + 1; i++)
        prime.Insert(i, true);

    // Remaining part of SIEVE
    prime.Insert(1, false);
    prime.Insert(2, false);
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2;
                     i <= max_val; i += p)
                prime.Insert(i, false);
        }
    }

    // To store the maximum prime number
    int maximum = -1;
    for (int i = 0; i < n; i++)
    {

        // If current element is prime
        // then update the maximum prime
        if (prime[arr[i]])
        {
            maximum = Math.Max(maximum, arr[i]);
        }

    }

    // Return the maximum prime
    // number from the array
    return maximum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 10, 15, 7, 6, 8, 13 };
    int n = arr.Length;

    Console.WriteLine(getPrime(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of primes
// in the given array
function getPrime($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // To store the maximum prime number
    $maximum = -1;

    for ($i = 0; $i < $n; $i++)
    {

        // If current element is prime
        // then update the maximum prime
        if ($prime[$arr[$i]])
            $maximum = max($maximum, $arr[$i]);
    }

    // Return the maximum prime
    // number from the array
    return $maximum;
}

// Driver code
$arr = array( 2, 10, 15, 7, 6, 8, 13 );
$n = count($arr) ;

echo getPrime($arr, $n);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required
// prime number from the array
function getPrime(arr, n)
{
    // Find maximum value in the array
    let max_val = Math.max(...arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (let p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // To store the maximum prime number
    let maximum = -1;
    for (let i = 0; i < n; i++) {

        // If current element is prime
        // then update the maximum prime
        if (prime[arr[i]])
            maximum = Math.max(maximum, arr[i]);
    }

    // Return the maximum prime
    // number from the array
    return maximum;
}

// Driver code
    let arr = [ 2, 10, 15, 7, 6, 8, 13 ];
    let n = arr.length;

    document.write(getPrime(arr, n));

</script>
```

**Output:** 

```
13
```