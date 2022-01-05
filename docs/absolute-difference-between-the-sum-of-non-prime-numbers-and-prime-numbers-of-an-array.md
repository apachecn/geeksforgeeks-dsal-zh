# 一个数组的非素数和素数之和的绝对差

> 原文:[https://www . geesforgeks . org/非质数和质数之和与数组的绝对差/](https://www.geeksforgeeks.org/absolute-difference-between-the-sum-of-non-prime-numbers-and-prime-numbers-of-an-array/)

给定一组正数，任务是计算非素数和素数之和的绝对差。
**注:** 1 既不是素数也不是非素数。
**示例:**

```
Input : 1 3 5 10 15 7
Output : 10
Explanation: Sum of non-primes = 25
             Sum of primes = 15

Input : 3 4 6 7 
Output : 0
```

**天真方法:**一个简单的解决方案是遍历数组，并不断检查每个元素是否是质数。如果数是质数，那么把它加到代表质数之和的 S2 和上，否则检查它是否不是 1，然后把它加到非质数之和上，比如说 S1。遍历整个数组后，取两者的绝对差值(S1-S2)。
**时间复杂度** : O(Nsqrt(N))
**高效方法:**使用厄拉多塞的[筛生成数组最大元素之前的所有素数，并将其存储在哈希中。现在，遍历数组并检查该数字是否出现在哈希映射中。然后，把这些数字加起来和 S2 相加，如果不是 1，就加起来和 S1 相加。
遍历整个数组后，显示两者的绝对差值。
**时间复杂度** : O(Nlog(log(N))](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to find the Absolute Difference
// between the Sum of Non-Prime numbers
// and Prime numbers of an Array

#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// the sum of non-primes and the
// sum of primes of an array.
int CalculateDifference(int arr[], int n)
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

    // Store the sum of primes in S1 and
    // the sum of non primes in S2
    int S1 = 0, S2 = 0;
    for (int i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // the number is prime
            S1 += arr[i];
        }
        else if (arr[i] != 1) {

            // the number is non-prime
            S2 += arr[i];
        }
    }

    // Return the absolute difference
    return abs(S2 - S1);
}

int main()
{

    // Get the array
    int arr[] = { 1, 3, 5, 10, 15, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Find the absolute difference
    cout << CalculateDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Absolute
// Difference between the Sum of
// Non-Prime numbers and Prime numbers
// of an Array
import java.util.*;

class GFG
{

// Function to find the difference
// between the sum of non-primes
// and the sum of primes of an array.
static int CalculateDifference(int arr[],
                               int n)
{
    // Find maximum value in the array
    int max_val = Integer.MIN_VALUE;
    for(int i = 0; i < n; i++)
    {
        if(arr[i] > max_val)
            max_val = arr[i];
    }

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    boolean []prime = new boolean[max_val + 1];

    for(int i = 0; i <= max_val; i++)
        prime[i] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2;
             p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2;
                     i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Store the sum of primes in
    // S1 and the sum of non
    // primes in S2
    int S1 = 0, S2 = 0;
    for (int i = 0; i < n; i++)
    {

        if (prime[arr[i]])
        {

            // the number is prime
            S1 += arr[i];
        }
        else if (arr[i] != 1)
        {

            // the number is non-prime
            S2 += arr[i];
        }
    }

    // Return the absolute difference
    return Math.abs(S2 - S1);
}

// Driver Code
public static void main(String []args)
{

    // Get the array
    int arr[] = { 1, 3, 5, 10, 15, 7 };
    int n = arr.length;

    // Find the absolute difference
    System.out.println(CalculateDifference(arr, n));
}
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 program to find the Absolute
# Difference between the Sum of Non-Prime
# numbers and Prime numbers of an Array
import sys

# Function to find the difference
# between the sum of non-primes
# and the sum of primes of an array.
def CalculateDifference(arr, n):

    # Find maximum value in the array
    max_val = -1
    for i in range(0, n):
        if(arr[i] > max_val):
            max_val = arr[i]

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    p = 2
    while (p * p <= max_val):

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True:

            # Update all multiples of p
            for i in range(p * 2,
                           max_val + 1, p):
                prime[i] = False
        p += 1

    # Store the sum of primes in
    # S1 and the sum of non primes
    # in S2
    S1 = 0
    S2 = 0
    for i in range (0, n):

        if prime[arr[i]]:

            # the number is prime
            S1 += arr[i]

        elif arr[i] != 1:

            # the number is non-prime
            S2 += arr[i]

    # Return the absolute difference
    return abs(S2 - S1)

# Driver code

# Get the array
arr = [ 1, 3, 5, 10, 15, 7 ]
n = len(arr)

# Find the absolute difference
print(CalculateDifference(arr, n))

# This code is contributed
# by ihritik
```

## C#

```
// C# program to find the Absolute
// Difference between the Sum of
// Non-Prime numbers and Prime
// numbers of an Array
using System;

class GFG
{

// Function to find the difference
// between the sum of non-primes
// and the sum of primes of an array.
static int CalculateDifference(int []arr,
                               int n)
{
    // Find maximum value in the array
    int max_val = int.MinValue;
    for(int i = 0; i < n; i++)
    {
        if(arr[i] > max_val)
            max_val = arr[i];
    }

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    bool []prime = new bool[max_val + 1];

    for(int i = 0; i <= max_val; i++)
        prime[i] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2;
             p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2;
                     i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Store the sum of primes in
    // S1 and the sum of non primes
    // in S2
    int S1 = 0, S2 = 0;
    for (int i = 0; i < n; i++)
    {
        if (prime[arr[i]])
        {

            // the number is prime
            S1 += arr[i];
        }
        else if (arr[i] != 1)
        {

            // the number is non-prime
            S2 += arr[i];
        }
    }

    // Return the absolute difference
    return Math.Abs(S2 - S1);
}

// Driver Code
public static void Main(string []args)
{

    // Get the array
    int []arr = { 1, 3, 5, 10, 15, 7 };
    int n = arr.Length;

    // Find the absolute difference
    Console.WriteLine(CalculateDifference(arr, n));
}
}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Absolute
// Difference between the Sum of
// Non-Prime numbers and Prime
// numbers of an Array

// Function to find the difference
// between the sum of non-primes and
// the sum of primes of an array.
function CalculateDifference($arr, $n)
{
    // Find maximum value in the array
    $max_val = PHP_INT_MIN;
    for($i = 0; $i < $n; $i++)
    {
        if($arr[$i] > $max_val)
            $max_val = $arr[$i];
    }

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, true);

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
                $prime[$i] = false;
        }
    }

    // Store the sum of primes in
    // S1 and the sum of non
    // primes in S2
    $S1 = 0;
    $S2 = 0;
    for ($i = 0; $i < $n; $i++)
    {

        if ($prime[$arr[$i]])
        {

            // the number is prime
            $S1 += $arr[$i];
        }
        else if ($arr[$i] != 1)
        {

            // the number is non-prime
            $S2 += $arr[$i];
        }
    }

    // Return the absolute difference
    return abs($S2 - $S1);
}

// Driver code

// Get the array
$arr = array( 1, 3, 5, 10, 15, 7 );
$n = sizeof($arr);

// Find the absolute difference
echo CalculateDifference($arr, $n);

// This code is contributed
// by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript program to find the Absolute
// Difference between the Sum of
// Non-Prime numbers and Prime numbers
// of an Array

    // Function to find the difference
    // between the sum of non-primes
    // and the sum of primes of an array.
    function CalculateDifference(arr , n)
    {
        // Find maximum value in the array
        var max_val = Number.MIN_VALUE;
        for (i = 0; i < n; i++) {
            if (arr[i] > max_val)
                max_val = arr[i];
        }

        // USE SIEVE TO FIND ALL PRIME NUMBERS
        // LESS THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]".
        // A value in prime[i] will finally be
        // false if i is Not a prime, else true.
        var prime = Array(max_val + 1);

        for (i = 0; i <= max_val; i++)
            prime[i] = true;

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (i = p * 2; i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the sum of primes in
        // S1 and the sum of non
        // primes in S2
        var S1 = 0, S2 = 0;
        for (i = 0; i < n; i++) {

            if (prime[arr[i]]) {

                // the number is prime
                S1 += arr[i];
            } else if (arr[i] != 1) {

                // the number is non-prime
                S2 += arr[i];
            }
        }

        // Return the absolute difference
        return Math.abs(S2 - S1);
    }

    // Driver Code

        // Get the array
        var arr = [ 1, 3, 5, 10, 15, 7 ];
        var n = arr.length;

        // Find the absolute difference
        document.write(CalculateDifference(arr, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
10
```