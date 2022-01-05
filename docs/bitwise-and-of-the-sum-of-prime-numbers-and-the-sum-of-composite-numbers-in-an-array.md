# 一个数组中素数之和与复合数之和的按位“与”

> 原文:[https://www . geeksforgeeks . org/质数的逐位和以及数组中复合数的和/](https://www.geeksforgeeks.org/bitwise-and-of-the-sum-of-prime-numbers-and-the-sum-of-composite-numbers-in-an-array/)

给定一个正数数组，任务是求非素数之和与素数之和的按位“与”。**注意****1**既不是素数也不是复合数。
**例** :

> **输入:** arr[] = {1，3，5，10，15，7}
> **输出:** 9
> 非素数之和= 10 + 15 = 25
> 素数之和= 3+5+7 = 15
> 25&15 = 9
> **输入:** arr[] = {3，4，6，7}
> **输出:**10

**天真的方法:**一个简单的解决方案是遍历数组，并不断检查每个元素是否是质数。如果这个数是质数，那么把它加到存储数组中质数总和的 S1，或者把它加到存储非质数总和的 S2。最后，打印 S1 & S2。
**时间复杂度:** O(N * sqrt(N))
**高效方法:**使用厄拉多塞的[筛生成数组最大元素之前的所有素数，并将其存储在哈希中。现在，遍历数组，检查数字是否是质数。最后，计算并打印素数之和与复合数之和的按位“与”。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the bitwise AND of the
// sum of primes and the sum of non-primes
int calculateAND(int arr[], int n)
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
    // the sum of non-primes in S2
    int S1 = 0, S2 = 0;
    for (int i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // The number is prime
            S1 += arr[i];
        }
        else if (arr[i] != 1) {

            // The number is not prime
            S2 += arr[i];
        }
    }

    // Return the bitwise AND of the sums
    return (S1 & S2);
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << calculateAND(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

class GFG
{
    static int getMax(int[] A)
    {
        int max = Integer.MIN_VALUE;
        for (int i: A)
        {
            max = Math.max(max, i);
        }
        return max;
    }

    // Function to return the bitwise AND of the
    // sum of primes and the sum of non-primes
    static int calculateAND(int arr[], int n)
    {
        // using Collections.max() to find
        // maximum element using only 1 line.
        // Find maximum value in the array
        int max_val = getMax(arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean prime[] = new boolean [max_val + 1];
        int i;

        for (i = 0; i < max_val + 1; i++)
            prime[i] = true;

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for ( i = p * 2; i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the sum of primes in S1 and
        // the sum of non-primes in S2
        int S1 = 0, S2 = 0;
        for (i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {

                // The number is prime
                S1 += arr[i];
            }
            else if (arr[i] != 1)
            {

                // The number is not prime
                S2 += arr[i];
            }
        }

        // Return the bitwise AND of the sums
        return (S1 & S2);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 3, 4, 6, 7 };
        int n = arr.length;

        System.out.println(calculateAND(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the bitwise AND of the
# sum of primes and the sum of non-primes
def calculateAND(arr, n):

    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, max_val + 1):

        if p * p >= max_val:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p
            for i in range(2 * p, max_val + 1, p):
                prime[i] = False

    # Store the sum of primes in S1 and
    # the sum of non-primes in S2
    S1 = 0
    S2 = 0
    for i in range(n):

        if (prime[arr[i]]):

            # The number is prime
            S1 += arr[i]
        elif (arr[i] != 1):

            # The number is not prime
            S2 += arr[i]

    # Return the bitwise AND of the sums
    return (S1 & S2)

# Driver code
arr = [3, 4, 6, 7]
n = len(arr)

print(calculateAND(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int getMax(int[] A)
    {
        int max = int.MinValue;
        foreach (int i in A)
        {
            max = Math.Max(max, i);
        }
        return max;
    }

    // Function to return the bitwise AND of the
    // sum of primes and the sum of non-primes
    static int calculateAND(int []arr, int n)
    {
        // using Collections.max() to find
        // maximum element using only 1 line.
        // Find maximum value in the array
        int max_val = getMax(arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        bool []prime = new bool [max_val + 1];
        int i;

        for (i = 0; i < max_val + 1; i++)
            prime[i] = true;

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (i = p * 2; i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the sum of primes in S1 and
        // the sum of non-primes in S2
        int S1 = 0, S2 = 0;
        for (i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {

                // The number is prime
                S1 += arr[i];
            }
            else if (arr[i] != 1)
            {

                // The number is not prime
                S2 += arr[i];
            }
        }

        // Return the bitwise AND of the sums
        return (S1 & S2);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 3, 4, 6, 7 };
        int n = arr.Length;

        Console.WriteLine(calculateAND(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the bitwise AND of the
// sum of primes and the sum of non-primes
function calculateAND(arr, n)
{
    // Find maximum value in the array
    var max_val = arr.reduce((a,b)=>Math.max(a,b));

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    var prime = Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (var p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Store the sum of primes in S1 and
    // the sum of non-primes in S2
    var S1 = 0, S2 = 0;
    for (var i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // The number is prime
            S1 += arr[i];
        }
        else if (arr[i] != 1) {

            // The number is not prime
            S2 += arr[i];
        }
    }

    // Return the bitwise AND of the sums
    return (S1 & S2);
}

// Driver code
var arr = [ 3, 4, 6, 7 ];
var n = arr.length;
document.write( calculateAND(arr, n));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N * log(log(N))
**空间复杂度:** O(max_val)，其中 max_val 是给定数组中元素的最大值。