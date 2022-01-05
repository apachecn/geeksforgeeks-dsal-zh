# 一个数组的非素数和素数的异或的绝对差

> 原文:[https://www . geeksforgeeks . org/非质数与质数的异或绝对差数组/](https://www.geeksforgeeks.org/absolute-difference-between-the-xor-of-non-prime-numbers-and-prime-numbers-of-an-array/)

给定一个由正整数 **N** 组成的数组 **arr[]** ，任务是计算非素数和素数异或的绝对差。**注意****1**既不是质数也不是合成数。
**举例:**

> **输入:** arr[] = {1，3，5，10，15，7}
> **输出:** 4
> 非素数异或= 10 ^ 15 = 5
> 素数异或= 3 ^ 5 ^ 7 = 1
> | 5–1 | = 4
> **输入:** arr[] = {3，4，6，7}
> **输出:** 2

**天真的方法:**一个简单的解决方案是遍历数组，并不断检查每个元素是否是质数。如果这个数是质数，那么将其异或到 **X1** 代表质数的**异或，否则将其异或到 **X2** 代表非质数**异或**。遍历整个数组后，取 **X1** 和 **X2** 的绝对差值。
**高效方法:**使用厄拉多塞的[筛生成数组最大元素之前的所有素数。现在，遍历数组并检查当前元素是否是质数。如果元素是质数，则将其与 **X1** 异或，否则将其与 **X2** 异或。最终打印**ABS(X1–X2)**。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the absolute difference
// between the XOR of non-primes and the
// XOR of primes in the given array
int calculateDifference(int arr[], int n)
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

    // Store the XOR of primes in X1 and
    // the XOR of non primes in X2
    int X1 = 1, X2 = 1;
    for (int i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // The number is prime
            X1 ^= arr[i];
        }
        else if (arr[i] != 1) {

            // The number is non-prime
            X2 ^= arr[i];
        }
    }

    // Return the absolute difference
    return abs(X1 - X2);
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 5, 10, 15, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Find the absolute difference
    cout << calculateDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    // Function to return
    // max_element from an array
    static int max_element(int[] arr)
    {
        int max = arr[0];

        for (int ele : arr)
            if (max < ele)
                max = ele;

        return max;
    }

    // Function to find the absolute difference
    // between the XOR of non-primes and the
    // XOR of primes in the given array
    static int calculateDifference(int[] arr, int n)
    {

        // Find maximum value in the array
        int max_val = max_element(arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS
        // LESS THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]".
        // A value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean[] prime = new boolean[max_val + 1];
        Arrays.fill(prime, true);

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
                for (int i = p * 2;
                         i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the XOR of primes in X1 and
        // the XOR of non primes in X2
        int x1 = 1, x2 = 1;
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])

                // The number is prime
                x1 ^= arr[i];
            else if (arr[i] != 1)

                // The number is non-prime
                x2 ^= arr[i];
        }

        // Return the absolute difference
        return Math.abs(x1 - x2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 5, 10, 15, 7 };
        int n = arr.length;

        // Find the absolute difference
        System.out.println(calculateDifference(arr, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the absolute difference
# between the XOR of non-primes and the
# XOR of primes in the given array
def calculateDifference(arr, n):

    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, max_val + 1):

        if p * p > max_val + 1:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(2 * p, max_val + 1, p):
                prime[i] = False

    # Store the XOR of primes in X1 and
    # the XOR of non primes in X2
    X1 = 1
    X2 = 1
    for i in range(n):

        if (prime[arr[i]]):

            # The number is prime
            X1 ^= arr[i]

        elif (arr[i] != 1):

            # The number is non-prime
            X2 ^= arr[i]

    # Return the absolute difference
    return abs(X1 - X2)

# Driver code
arr = [1, 3, 5, 10, 15, 7]
n = len(arr)

# Find the absolute difference
print(calculateDifference(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return
    // max_element from an array
    static int max_element(int[] arr)
    {
        int max = arr[0];

        foreach (int ele in arr)
            if (max < ele)
                max = ele;

        return max;
    }

    // Function to find the absolute difference
    // between the XOR of non-primes and the
    // XOR of primes in the given array
    static int calculateDifference(int[] arr, int n)
    {

        // Find maximum value in the array
        int max_val = max_element(arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS
        // LESS THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]".
        // A value in prime[i] will finally be false
        // if i is Not a prime, else true.
        bool[] prime = new bool[max_val + 1];
        for(int index = 0; index < max_val + 1; index++)
            prime[index] = true;

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
                for (int i = p * 2;
                        i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the XOR of primes in X1 and
        // the XOR of non primes in X2
        int x1 = 1, x2 = 1;
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])

                // The number is prime
                x1 ^= arr[i];
            else if (arr[i] != 1)

                // The number is non-prime
                x2 ^= arr[i];
        }

        // Return the absolute difference
        return Math.Abs(x1 - x2);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 3, 5, 10, 15, 7 };
        int n = arr.Length;

        // Find the absolute difference
        Console.WriteLine(calculateDifference(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the absolute difference
// between the XOR of non-primes and the
// XOR of primes in the given array
function calculateDifference(arr, n)
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
    for (let p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Store the XOR of primes in X1 and
    // the XOR of non primes in X2
    let X1 = 1, X2 = 1;
    for (let i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // The number is prime
            X1 ^= arr[i];
        }
        else if (arr[i] != 1) {

            // The number is non-prime
            X2 ^= arr[i];
        }
    }

    // Return the absolute difference
    return Math.abs(X1 - X2);
}

// Driver code
    let arr = [ 1, 3, 5, 10, 15, 7 ];
    let n = arr.length;

    // Find the absolute difference
    document.write(calculateDifference(arr, n));

</script>
```

**Output**

```
4
```

**时间复杂度:O(N*log(logN))**

**辅助空间:O(max_val)**