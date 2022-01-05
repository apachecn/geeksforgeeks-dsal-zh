# 求给定数组中非素元素的和

> 原文:[https://www . geeksforgeeks . org/find-给定数组中非素元素的和/](https://www.geeksforgeeks.org/find-the-sum-of-non-prime-elements-in-the-given-array/)

给定一个数组 **arr[]** ，任务是打印该数组中非素元素的和。
**例:**

> **输入:** arr[] = {1，3，7，4，9，8}
> **输出:** 22
> 非素元素为{1，4，9，8}和 1 + 4 + 9 + 8 = 22
> **输入:** arr[] = {11，4，10，7}
> **输出:** 14

**方法:**初始化 **sum = 0** 并开始逐元素遍历数组元素，如果当前元素不是素数，则更新 **sum = sum + arr[i]** 。最后打印**和**。可以使用厄拉多塞的[筛对初级性进行最佳测试。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find sum of
// non-primes in given array
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// non-prime elements from the array
int nonPrimeSum(int arr[], int n)
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

    // Sum all non-prime elements in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code
int main()
{

    int arr[] = { 1, 3, 7, 4, 9, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << nonPrimeSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// non-primes in given array
import java.util.*;

class GFG
{

//returns the maximum element
static int max_element(int arr[])
{
    int max_e = Integer.MIN_VALUE;
    for(int i = 0; i < arr.length; i++)
    {
    max_e = Math.max(max_e, arr[i]);
    }
    return max_e;
}

// Function to return the sum of
// non-prime elements from the array
static int nonPrimeSum(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = max_element(arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[] = new boolean[max_val + 1];

    for(int i = 0; i < prime.length; i++)
    prime[i] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Sum all non-prime elements in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code
public static void main(String args[])
{

    int arr[] = { 1, 3, 7, 4, 9, 8 };
    int n = arr.length;
    System.out.println( nonPrimeSum(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find sum of non-primes
# in given array

# from math lib. import sqrt
from math import sqrt

# Function to return the sum of
# non-prime elements from the array
def nonPrimeSum(arr, n) :

    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS 
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True] * (max_val + 1)

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False

    for p in range(2, int(sqrt(max_val)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p) :
                prime[i] = False

    # Sum all non-prime elements in arr[]
    sum = 0
    for i in range(0, n) :
        if (not prime[arr[i]]) :
            sum += arr[i]

    return sum

# Driver code
if __name__ == "__main__" :

    arr= [ 1, 3, 7, 4, 9, 8 ]
    n = len(arr)

    print(nonPrimeSum(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find sum of non-primes
// in given array
using System;

class GFG
{

// returns the maximum element
static int max_element(int[] arr)
{
    int max_e = int.MinValue;
    for(int i = 0; i < arr.Length; i++)
    {
        max_e = Math.Max(max_e, arr[i]);
    }
    return max_e;
}

// Function to return the sum of
// non-prime elements from the array
static int nonPrimeSum(int[] arr, int n)
{
    // Find maximum value in the array
    int max_val = max_element(arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]".
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    bool[] prime = new bool[max_val + 1];

    for(int i = 0; i < prime.Length; i++)
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
            for (int i = p * 2;
                     i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Sum all non-prime elements in arr[]
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]])
            sum += arr[i];

    return sum;
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 3, 7, 4, 9, 8 };
    int n = arr.Length;
    Console.WriteLine(nonPrimeSum(arr, n));
}
}

// This code is contributed
// by Mukul Singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// non-primes in given array

// Function to return the sum of
// non-prime elements from the array
function nonPrimeSum($arr, $n)
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
            for ($i = $p * 2;
                 $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // Sum all non-prime elements in arr[]
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        if (!$prime[$arr[$i]])
             $sum += $arr[$i];

    return $sum;
}

// Driver code
$arr = array( 1, 3, 7, 4, 9, 8 );
$n = count($arr);

echo nonPrimeSum($arr, $n);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// non-primes in given array

    //returns the maximum element
    function max_element(arr)
    {
        let max_e = Number.MIN_VALUE;
        for(let i = 0; i < arr.length; i++)
        {
            max_e = Math.max(max_e, arr[i]);
        }
        return max_e;
    }

    // Function to return the sum of
    // non-prime elements from the array
    function nonPrimeSum(arr,n)
    {
        // Find maximum value in the array
        let max_val = max_element(arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        let prime = new Array(max_val + 1);

        for(let i = 0; i < prime.length; i++)
            prime[i] = true;

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (let p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (let i = p * 2; i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Sum all non-prime elements in arr[]
        let sum = 0;
        for (let i = 0; i < n; i++)
            if (!prime[arr[i]])
                sum += arr[i];

        return sum;
    }

    // Driver code

    let arr=[1, 3, 7, 4, 9, 8 ];
    let n = arr.length;
    document.write( nonPrimeSum(arr, n));

    // This code is contributed by unknown2108

</script>
```

**Output:** 

```
22
```