# 数组中所有素数的和

> 原文:[https://www . geesforgeks . org/数组中所有素数之和/](https://www.geeksforgeeks.org/sum-of-all-prime-numbers-in-an-array/)

给定一个由 N 个正整数组成的数组 arr[]。任务是编写一个程序，找出给定数组中所有素元素的和。
**例** :

> **输入** : arr[] = {1，3，4，5，7}
> **输出** : 15
> 有三个素数，3，5 和 7 的和=15。
> **输入** : arr[] = {1，2，3，4，5，6，7}
> **输出** : 17

**天真方法:**一个简单的解决方法是遍历数组，不断检查每个元素是否是素数，同时添加素数元素。
**高效方法:**使用厄拉多塞的[筛生成数组中最大元素的所有素数，并将它们存储在哈希中。现在遍历数组，用筛子找出那些质数元素的和。
下面是高效方法的实现:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find sum of
// primes in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find count of prime
int primeSum(int arr[], int n)
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

    // Sum all primes in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << primeSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// primes in given array.
import java.util.*;

class GFG
{

// Function to find count of prime
static int primeSum(int arr[], int n)
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
    prime.add(0,Boolean.FALSE);
    prime.add(1,Boolean.FALSE);
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

    // Sum all primes in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (prime.get(arr[i]))
            sum += arr[i];

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;
    System.out.print(primeSum(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 program to find sum of
# primes in given array.

# Function to find count of prime
def primeSum( arr, n):
    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    # THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be False
    # if i is Not a prime, else true.
    prime=[True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, max_val + 1):
        if(p * p > max_val):
            break

        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val+1, p):
                prime[i] = False

    # Sum all primes in arr[]
    sum = 0

    for i in range(n):
        if (prime[arr[i]]):
            sum += arr[i]

    return sum

# Driver code
arr =[1, 2, 3, 4, 5, 6, 7]

n = len(arr)

print(primeSum(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find sum of
// primes in given array.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to find count of prime
static int primeSum(int []arr, int n)
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
        prime.Insert(i,true);

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
                prime.Insert(i,false);
        }
    }

    // Sum all primes in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;
    Console.WriteLine(primeSum(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find sum of
// primes in given array.

// Function to find count of prime
function primeSum(arr, n) {
    // Find maximum value in the array
    let max_val = arr.sort((a, b) => b - a)[0];

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

    // Sum all primes in arr[]
    let sum = 0;
    for (let i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code

let arr = [1, 2, 3, 4, 5, 6, 7];
let n = arr.length;

document.write(primeSum(arr, n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
17
```

**时间复杂度:** O(n*loglogn)