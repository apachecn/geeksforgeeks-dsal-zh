# 数组中所有可被 k 整除的复合数的和与积

> 原文:[https://www . geeksforgeeks . org/可被数组中的 k 整除的所有复合数的和与积/](https://www.geeksforgeeks.org/sum-and-product-of-all-composite-numbers-which-are-divisible-by-k-in-an-array/)

给定一个由 N 个正整数组成的数组 arr[]。任务是找出给定数组中可被给定数字 k 整除的所有复合元素的和。
**例:**

```
Input: arr[] = {1, 3, 4, 5, 7}, k = 2
Output: 4, 4
There is one composite number i.e. 4.
So, sum = 4 and product = 4

Input: arr[] = {1, 2, 3, 4, 5, 6, 7}, k = 2
Output: 10, 24
There is only two composite numbers i.e. 4 and 6.
So, sum = 10 and product = 24
```

**天真方法:**
一个简单的解决方案是遍历数组，不断检查每个元素是否是复合元素，是否也能被 k 整除，然后同时对复合元素进行加法和乘积运算。
**高效方法:**
使用厄拉多塞的筛子生成数组中最大元素的所有素数，并将它们存储在散列中。现在遍历数组，用筛子找出那些被 k 整除的复合元素的和与积。
下面是高效方法的实现:

## C++

```
// CPP program to find sum and product of
// composites which are divisible by k in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find count of composite
void compositeSumProduct(int arr[], int n, int k)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // Use sieve to find all prime numbers less than
    // or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Remaining part of SIEVE
    prime[0] = true;
    prime[1] = true;
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
    int sum = 0, product = 1;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]] && arr[i] % k == 0) {
            sum += arr[i];
            product *= arr[i];
        }

    cout << "Sum of composite numbers divisible by k is "
         << sum;
    cout << "\nProduct of composite numbers divisible by k is "
         << product;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    compositeSumProduct(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum and product of
// composites which are divisible by k in given array.
import java.util.Vector;

public class GFG {

    static int max_val(int[] arr) {
        int i;

        // Initialize maximum element
        int max = arr[0];

        // Traverse array elements from second and
        // compare every element with current max  
        for (i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }

        return max;
    }

// Function to find count of composite
    static void compositeSumProduct(int arr[], int n, int k) {
        // Find maximum value in the array
        int max_val = max_val(arr);

        // Use sieve to find all prime numbers less than
        // or equal to max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        Vector<Boolean> prime = new Vector<>();
        // Remaining part of SIEVE
        for(int i = 0;i<max_val+1;i++){
            prime.add(i, Boolean.TRUE);
        }
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

        // Sum all primes in arr[]
        int sum = 0, product = 1;
        for (int i = 0; i < n; i++) {
            //if (!prime[arr[i]] && arr[i] % k == 0)
            if (!prime.get(arr[i]) && arr[i] % k == 0) {
                sum += arr[i];
                product *= arr[i];
            }
        }
        System.out.println("Sum of composite numbers "
                + "divisible by k is " + sum);
        System.out.println("\nProduct of composite numbers"
                + " divisible by k is " + product);

    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {1, 2, 3, 4, 5, 6, 7};
        int n = arr.length;
        int k = 2;
        compositeSumProduct(arr, n, k);
    }

}
```

## 蟒蛇 3

```
# Python 3 program to find sum and product
# of composites which are divisible by k
# in given array.
from math import sqrt, ceil

# Function to find count of composite
def compositeSumProduct(arr, n, k):

    # Find maximum value in the array
    max_val = arr[0];
    for i in range(len(arr)):
        if(max_val < arr[i]):
            max_val = arr[i]

    # Use sieve to find all prime numbers
    # less than or equal to max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    k = int(sqrt(max_val))
    for p in range(2, k + 1, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val, p):
                prime[i] = False

    # Sum all primes in arr[]
    sum = 0
    product = 1
    for i in range(0, n, 1):
        if (prime[arr[i]] == False and
                  arr[i] % k == 0):
            sum += arr[i]
            product *= arr[i]

    print("Sum of composite numbers",
          "divisible by k is", sum)
    print("Product of composite numbers",
          "divisible by k is", product)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7]
    n = len(arr)
    k = 2
    compositeSumProduct(arr, n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum and product of
// composites which are divisible by k in given array.
using System;
using System.Collections.Generic;
public class GFG {

    static int max_val_func(int []arr) {
        int i;

        // Initialize maximum element
        int max = arr[0];

        // Traverse array elements from second and
        // compare every element with current max
        for (i = 1; i < arr.Length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }

        return max;
    }

// Function to find count of composite
    static void compositeSumProduct(int []arr, int n, int k) {
        // Find maximum value in the array
        int max_val = max_val_func(arr);

        // Use sieve to find all prime numbers less than
        // or equal to max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        List<int> prime = new List<int>();
        // Remaining part of SIEVE
        for(int i = 0;i<max_val+1;i++){
            prime.Insert(i, 1);
        }
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == 1) {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p) {
                    prime.Insert(i, 0);
                }
            }
        }

        // Sum all primes in arr[]
        int sum = 0, product = 1;
        for (int i = 0; i < n; i++) {
            //if (!prime[arr[i]] && arr[i] % k == 0)
            if (prime[arr[i]]==0 && arr[i] % k == 0) {
                sum += arr[i];
                product *= arr[i];
            }
        }
        Console.WriteLine("Sum of composite numbers "
                + "divisible by k is " + sum);
        Console.WriteLine("\nProduct of composite numbers"
                + " divisible by k is " + product);

    }

// Driver code
    static public void Main(String []args) {
        int []arr = {1, 2, 3, 4, 5, 6, 7};
        int n = arr.Length;
        int k = 2;
        compositeSumProduct(arr, n, k);
    }

}
//contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javsacript program to find sum and product of
// composites which are divisible by k in given array.

// Function to find count of composite
function compositeSumProduct(arr, n, k)
{

    // Find maximum value in the array
    let max_val = arr.sort((a, b) => b - a)[0];

    // Use sieve to find all prime numbers less than
    // or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = true;
    prime[1] = true;
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
    let sum = 0, product = 1;
    for (let i = 0; i < n; i++)
        if (!prime[arr[i]] && arr[i] % k == 0) {
            sum += arr[i];
            product *= arr[i];
        }

    document.write("Sum of composite numbers divisible by k is " + sum);
    document.write("<br>Product of composite numbers divisible by k is " + product);
}

// Driver code
let arr = [1, 2, 3, 4, 5, 6, 7];
let n = arr.length
let k = 2;
compositeSumProduct(arr, n, k);

// This code is contributed by gfgking
</script>
```

**时间复杂度:** O(n)其中 n 是数组中元素的最大值，而不是大小。

**Output:** 

```
Sum of composite numbers divisible by k is 10
Product of composite numbers divisible by k is 24
```