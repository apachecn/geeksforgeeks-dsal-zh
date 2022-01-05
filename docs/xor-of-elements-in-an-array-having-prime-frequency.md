# 具有素数频率的数组中元素的异或运算

> 原文:[https://www . geeksforgeeks . org/具有素数频率的数组元素异或/](https://www.geeksforgeeks.org/xor-of-elements-in-an-array-having-prime-frequency/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找出数组中具有素数频率的元素的异或。**注意****1**既不是质数也不是合成数。
**举例:**

> **输入:** arr[] = {5，4，6，5，4，6}
> **输出:** 7
> 所有元素出现 2 次这是一个素数
> 所以，5 ^ 4 ^ 6 = 7
> **输入:** arr[] = {1，2，3，3，2，3，3}
> **输出:** 1
> 只有 2 和 3 出现素数次即 3
> 所以，2 ^ 3 = 1

**进场:**

*   遍历数组，将所有元素的频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   构建厄拉多塞的[筛，用于测试一个数在 O(1)时间内的素性。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   使用上一步中计算的筛数组计算素频率元素的异或。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

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

// Function to return the xor of elements
// in an array having prime frequency
int xorPrimeFreq(int arr[], int n)
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

    long xorVal = 0;

    // Traverse the map using iterators
    for (auto it = m.begin(); it != m.end(); it++) {

        // Count the number of elements
        // having prime frequencies
        if (prime[it->second]) {
            xorVal ^= it->first;
        }
    }

    return xorVal;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 6, 5, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << xorPrimeFreq(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find xor of elements
// in an array having prime frequency
import java.util.*;

class GFG
{

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

    // Function to return the xor of elements
    // in an array having prime frequency
    static int xorOfElements(int arr[], int n)
    {
        boolean prime[] = new boolean[n + 1];
        Arrays.fill(prime, true);

        SieveOfEratosthenes(prime, n + 1);

        int i, j;

        // Map is used to store
        // element frequencies
        HashMap<Integer,
                Integer> m = new HashMap<>();
        for (i = 0; i < n; i++)
        {
            if(m.containsKey(arr[i]))
                m.put(arr[i], m.get(arr[i]) + 1);
            else
                m.put(arr[i], 1);
        }

        int xor = 0;

        // Traverse the map
        for (Map.Entry<Integer,
                       Integer> entry : m.entrySet())
        {
            int key = entry.getKey();
            int value = entry.getValue();

            // xor the elements
            // having prime frequencies
            if (prime[value])
            {
                xor ^= (key);
            }
        }

        return xor;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 5, 4, 6, 5, 4, 6 };
        int n = arr.length;

        System.out.println(xorOfElements(arr, n));
    }
}

// This code is contributed by NikhilRathor
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to create Sieve to check primes
def SieveOfEratosthenes(prime, p_size) :

    # False here indicates
    # that it is not prime
    prime[0] = False;
    prime[1] = False;

    for p in range(2, int(sqrt(p_size)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]) :

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size + 1, p) :
                prime[i] = False;

    return prime

# Function to return the xor of elements
# in an array having prime frequency
def xorPrimeFreq( arr, n) :
    prime = [True] * (n + 1);

    prime = SieveOfEratosthenes(prime, n + 1);

    # Map is used to store
    # element frequencies
    m = dict.fromkeys(arr, 0);

    for i in range(n) :
        m[arr[i]] += 1;

    xorVal = 0;

    # Traverse the map using iterators
    for key,value in m.items() :

        # Count the number of elements
        # having prime frequencies
        if (prime[value]) :
            xorVal ^= key;

    return xorVal;

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 4, 6, 5, 4, 6 ];

    n = len(arr);

    print(xorPrimeFreq(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find xor of elements
// in an array having prime frequency
using System;
using System.Collections.Generic;   

class GFG
{

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

    // Function to return the xor of elements
    // in an array having prime frequency
    static int xorOfElements(int []arr, int n)
    {
        int i, j;
        bool []prime = new bool[n + 1];
        for(i = 0; i< n + 1; i++)
            prime[i] = true;

        SieveOfEratosthenes(prime, n + 1);

        // Map is used to store
        // element frequencies
        Dictionary<int,
                   int> m = new Dictionary<int,
                                           int>();
        for (i = 0; i < n; i++)
        {
            if(m.ContainsKey(arr[i]))
                m[arr[i]] = m[arr[i]] + 1;
            else
                m.Add(arr[i], 1);
        }

        int xor = 0;

        // Traverse the map
        foreach(KeyValuePair<int, int> entry in m)
        {
            int key = entry.Key;
            int value = entry.Value;

            // xor the elements
            // having prime frequencies
            if (prime[value])
            {
                xor ^= (key);
            }
        }
        return xor;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 5, 4, 6, 5, 4, 6 };
        int n = arr.Length;

        Console.WriteLine(xorOfElements(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach
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
function xorPrimeFreq(arr, n){
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

    let xorVal = 0;

    // Traverse the map using iterators
    for (var it in m) {

        // Count the number of elements
        // having prime frequencies
        if (prime[m[it]]) {
            xorVal ^= it;
        }
    }

    return xorVal;
}

// Driver code
let a = [ 5, 4, 6, 5, 4, 6 ];
let len = a.length;
document.write( xorPrimeFreq(a, len));
</script>
```

**Output:** 

```
7
```