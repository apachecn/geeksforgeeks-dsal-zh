# 数组中素数对的数量

> 原文:[https://www . geesforgeks . org/数组中质数对数/](https://www.geeksforgeeks.org/number-of-prime-pairs-in-an-array/)

给定一个数组。任务是计算可能的对，这些对可以用数组中两个元素都是质数的元素组成。
**注**:像(a，b)和(b，a)这样的配对不应该被认为是不同的。
**示例:**

```
Input: arr[] = {1, 2, 3, 5, 7, 9}
Output: 6
From the given array, prime pairs are
(2, 3), (2, 5), (2, 7), (3, 5), (3, 7), (5, 7)

Input: arr[] = {1, 4, 5, 9, 11}
Output: 1
```

一种简单的方法是计算数组中所有可能的对，并检查对中的两个元素是否都是质数。
一个**有效的方法**是使用厄拉多塞筛计算数组中的素数。假设是 C .现在，可能对的总数等于 **C*(C-1)/2。**
以下是上述方法的实施:

## C++

```
// CPP program to find count of
// prime pairs in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find count of prime pairs
int pairCount(int arr[], int n)
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

    // Find all primes in arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    // return the count of
    // possible prime pairs
    // Number of unique pairs
    // with N elements is N*(N-1)/2
    return (count * (count - 1)) / 2;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << pairCount(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of
// prime pairs in given array.
import java.util.*;

class GFG {

    // Function to find count of prime pairs
    static int pairCount(int arr[], int n)
    {

        // Find maximum value in the array
        int max_val = Arrays.stream(arr).max().getAsInt();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        Vector<Boolean> prime = new Vector<>(max_val + 1);
        for (int i = 0; i < max_val + 1; i++) {
            prime.add(true);
        }

        // Remaining part of SIEVE
        prime.add(0, Boolean.FALSE);
        prime.add(1, Boolean.FALSE);
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime.get(p) == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p) {
                    prime.add(i, Boolean.FALSE);
                }
            }
        }

        // Find all primes in arr[]
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (prime.get(arr[i])) {
                count++;
            }
        }

        // return the count of
        // possible prime pairs
        // Number of unique pairs
        // with N elements is N*(N-1)/2
        return (count * (count - 1)) / 2;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
        int n = arr.length;
        System.out.println(pairCount(arr, n));
    }
}

/* This code has been contributed
by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python 3 program to find count of
# prime pairs in given array.
from math import sqrt

# Function to find count of prime pairs
def pairCount(arr, n):

    # Find maximum value in the array
    max_val = arr[0]
    for i in range(len(arr)):
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
    k = int(sqrt(max_val)) + 1
    for p in range(2, k, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i] = False

    # Find all primes in arr[]
    count = 0
    for i in range(0, n, 1):
        if (prime[arr[i]]):
                count += 1

    # return the count of possible prime
    # pairs. Number of unique pairs
    # with N elements is N*(N-1)/2
    return (count * (count - 1)) / 2

# Driver code
if __name__ =='__main__':
    arr = [1, 2, 3, 4, 5, 6, 7]
    n = len(arr)
    print(int(pairCount(arr, n)))

# This code is contributed by
# Shahshank_Sharma
```

## C#

```
// C# program to find count of
// prime pairs in given array.

using System;
using System.Linq;

class GFG {

    // Function to find count of prime pairs
    static int pairCount(int[] arr, int n)
    {

        // Find maximum value in the array
        int max_val = arr.Max();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        bool[] prime = new bool[max_val + 1];
        for (int i = 0; i < max_val + 1; i++) {
            prime[i] = true;
        }

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Find all primes in arr[]
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (prime[arr[i]]) {
                count++;
            }
        }

        // return the count of
        // possible prime pairs
        // Number of unique pairs
        // with N elements is N*(N-1)/2
        return (count * (count - 1)) / 2;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5, 6, 7 };
        int n = arr.Length;
        Console.WriteLine(pairCount(arr, n));
    }
}

// This code has been contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of
// prime pairs in given array.

// Function to find count of prime pairs
function pairCount($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    // vector<bool> prime(max_val + 1, true);
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

    // Find all primes in arr[]
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$arr[$i]])
            $count++;

    // return the count of
    // possible prime pairs
    // Number of unique pairs
    // with N elements is N*(N-1)/2
    return ($count * ($count - 1)) / 2;
}

// Driver code
$arr = array (1, 2, 3, 4, 5, 6, 7 );
$n = sizeof($arr);
echo pairCount($arr, $n);

// This code is contributed by ajit...
?>
```

## java 描述语言

```
<script>

    // Javascript program to find count of
    // prime pairs in given array.

    // Function to find count of prime pairs
    function pairCount(arr, n)
    {

        // Find maximum value in the array
        let max_val = 0;
        for (let i = 0; i < n; i++)
        {
            max_val = Math.max(max_val, arr[i]);
        }

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        let prime = new Array(max_val + 1);
        for (let i = 0; i < max_val + 1; i++) {
            prime[i] = true;
        }

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (let p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (let i = p * 2; i <= max_val; i += p)
                {
                    prime[i] = false;
                }
            }
        }

        // Find all primes in arr[]
        let count = 0;
        for (let i = 0; i < n; i++) {
            if (prime[arr[i]]) {
                count++;
            }
        }

        // return the count of
        // possible prime pairs
        // Number of unique pairs
        // with N elements is N*(N-1)/2
        return (count * (count - 1)) / 2;
    }

    let arr = [ 1, 2, 3, 4, 5, 6, 7 ];
    let n = arr.length;
    document.write(pairCount(arr, n));

</script>
```

**Output:** 

```
6
```