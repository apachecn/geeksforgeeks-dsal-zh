# 具有素数频率的数组中元素的乘积

> 原文:[https://www . geeksforgeeks . org/具有素数频率的数组元素乘积/](https://www.geeksforgeeks.org/product-of-elements-in-an-array-having-prime-frequency/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找出数组中具有素频率的元素的乘积。因为产品可以很大，所以打印产品的模 **10 <sup>9</sup> + 7** 。**注意**说明 **1** 既不是素的也不是复合的。
**示例:**

> **输入:** arr[] = {5，4，6，5，4，6}
> **输出:** 120
> 所有元素出现 2 次这是一个素数
> 所以，5 * 4 * 6 = 120
> **输入:** arr[] = {1，2，3，3，2，3，3}
> **输出:** 6
> 只有 2 和 3 出现素数 I 次
> 所以，2 * 3 = 6

**进场:**

*   遍历数组，将所有元素的频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   构建厄拉多塞的[筛，用于测试一个数在 O(1)时间内的素性。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   使用上一步中计算的筛阵列计算具有主频的元素的乘积。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MOD 1000000007

// Function to create Sieve to check primes
void SieveOfEratosthenes(bool prime[], int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the product of elements
// in an array having prime frequency
int productPrimeFreq(int arr[], int n)
{
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, n + 1);

    int i, j;

    // Map is used to store
    // element frequencies
    unordered_map<int, int> m;
    for (i = 0; i < n; i++)
        m[arr[i]]++;

    long product = 1;

    // Traverse the map using iterators
    for (auto it = m.begin(); it != m.end(); it++) {

        // Count the number of elements
        // having prime frequencies
        if (prime[it->second]) {
            product *= (it->first % MOD);
            product %= MOD;
        }
    }

    return (int)(product);
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 6, 5, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << productPrimeFreq(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MOD = 1000000007;

// Function to create Sieve to check primes
static void SieveOfEratosthenes(boolean prime[],
                                int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2;
                     i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the product of elements
// in an array having prime frequency
static int productPrimeFreq(int arr[], int n)
{
    boolean []prime = new boolean[n + 1];
    for (int i = 0; i < n; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, n + 1);

    int i, j;

    // Map is used to store
    // element frequencies
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    for (i = 0 ; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }
    long product = 1;

    // Traverse the map using iterators
    for (Map.Entry<Integer,
                   Integer> it : mp.entrySet())
    {

        // Count the number of elements
        // having prime frequencies
        if (prime[it.getValue()])
        {
            product *= (it.getKey() % MOD);
            product %= MOD;
        }
    }
    return (int)(product);
}

// Driver code
static public void main (String []arg)
{
    int arr[] = { 5, 4, 6, 5, 4, 6 };
    int n = arr.length;

    System.out.println(productPrimeFreq(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 1000000007

# Function to create Sieve to check primes
def SieveOfEratosthenes(prime, p_size):

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    for p in range(2, p_size):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range(2 * p, p_size, p):
                prime[i] = False

# Function to return the product of elements
# in an array having prime frequency
def productPrimeFreq(arr, n):
    prime = [True for i in range(n + 1)]

    SieveOfEratosthenes(prime, n + 1)

    i, j = 0, 0

    # Map is used to store
    # element frequencies
    m = dict()
    for i in range(n):
        m[arr[i]] = m.get(arr[i], 0) + 1

    product = 1

    # Traverse the map using iterators
    for it in m:

        # Count the number of elements
        # having prime frequencies
        if (prime[m[it]]):
            product *= it % MOD
            product %= MOD

    return product

# Driver code
arr = [5, 4, 6, 5, 4, 6]
n = len(arr)

print(productPrimeFreq(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic;

class GFG
{
static int MOD = 1000000007;

// Function to create Sieve to check primes
static void SieveOfEratosthenes(bool []prime,
                                int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2;
                     i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the product of elements
// in an array having prime frequency
static int productPrimeFreq(int []arr, int n)
{
    bool []prime = new bool[n + 1];
    int i;
    for (i = 0; i < n; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, n + 1);

    // Map is used to store
    // element frequencies
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    for (i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            var val = mp[arr[i]];
            mp.Remove(arr[i]);
            mp.Add(arr[i], val + 1);
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }
    long product = 1;

    // Traverse the map using iterators
    foreach(KeyValuePair<int, int> it in mp)
    {

        // Count the number of elements
        // having prime frequencies
        if (prime[it.Value])
        {
            product *= (it.Key % MOD);
            product %= MOD;
        }
    }
    return (int)(product);
}

// Driver code
static public void Main (String []arg)
{
    int []arr = { 5, 4, 6, 5, 4, 6 };
    int n = arr.Length;

    Console.WriteLine(productPrimeFreq(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach
let MOD = 1000000007;

// Function to create Sieve to check primes
function SieveOfEratosthenes(prime, p_size){
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;
    for (let p = 2; p * p <= p_size; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {
            // Update all multiples of p,
            // set them to non-prime
            for (let i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
    return prime;
}

// Function to return the product of elements
// in an array having prime frequency
function productPrimeFreq(arr, n){
    let prime = [];
    for(let i = 0;i<n+1;i++){
        prime.push(true);
    }
    prime = SieveOfEratosthenes(prime, n + 1);
    let i, j;
    // Map is used to store
    // element frequencies
    let m = new Map();
    for (i = 0; i < n; i++){
      if(m[arr[i]])
        m[arr[i]]++;
      else
        m[arr[i]] = 1;
    }

    let product = 1;

    // Traverse the map using iterators
    for (var it in m) {
        // Count the number of elements
        // having prime frequencies
        if (prime[m[it]]) {
            product *= (it % MOD);
            product %= MOD;
        }
    }

    return (product);
}

// Driver code
let a = [ 5, 4, 6, 5, 4, 6 ];
let len = a.length;
document.write(productPrimeFreq(a, len));
</script>
```

**Output:** 

```
120
```