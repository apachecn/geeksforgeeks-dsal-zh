# 具有主频的数组中元素的和

> 原文:[https://www . geeksforgeeks . org/具有素频率的数组元素之和/](https://www.geeksforgeeks.org/sum-of-elements-in-an-array-having-prime-frequency/)

给定一个数组 **arr** ，任务是找出数组中具有素频率的元素的和。
**注:** 1 既不是素数，也不是复合数。
**例:**

> **输入:** arr[] = {5，4，6，5，4，6}
> **输出:** 15
> 所有元素出现 2 次这是一个质数
> 所以，5 + 4 + 6 = 15
> **输入:** arr[] = {1，2，3，3，2，3，3}
> **输出:** 5
> 只有 2 和 3 出现质数的次数 i.e
> 所以，2 + 3 = 5

**进场:**

*   遍历数组，将所有元素的频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   构建厄拉多塞的[筛，用于测试一个数在 O(1)时间内的素性。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   使用上一步中计算的筛数组计算具有主频的元素的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of elements
// in an array having prime frequency
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

// Function to return the sum of elements
// in an array having prime frequency
int sumOfElements(int arr[], int n)
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

    int sum = 0;

    // Traverse the map using iterators
    for (auto it = m.begin(); it != m.end(); it++) {

        // Count the number of elements
        // having prime frequencies
        if (prime[it->second]) {
            sum += (it->first);
        }
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 6, 5, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumOfElements(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of elements
// in an array having prime frequency
import java.util.*;

class GFG
{

    // Function to create Sieve to check primes
    static void SieveOfEratosthenes(boolean prime[], int p_size)
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
                for (int i = p * 2; i <= p_size; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to return the sum of elements
    // in an array having prime frequency
    static int sumOfElements(int arr[], int n)
    {
        boolean prime[] = new boolean[n + 1];
        Arrays.fill(prime, true);

        SieveOfEratosthenes(prime, n + 1);

        int i, j;

        // Map is used to store
        // element frequencies
        HashMap<Integer, Integer> m = new HashMap<>();
        for (i = 0; i < n; i++)
        {
            if(m.containsKey(arr[i]))
                m.put(arr[i], m.get(arr[i]) + 1);
            else
                m.put(arr[i], 1);
        }

        int sum = 0;

        // Traverse the map
        for (Map.Entry<Integer, Integer> entry : m.entrySet())
        {
            int key = entry.getKey();
            int value = entry.getValue();

            // Count the number of elements
            // having prime frequencies
            if (prime[value])
            {
                sum += (key);
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 5, 4, 6, 5, 4, 6 };
        int n = arr.length;

        System.out.println(sumOfElements(arr, n));
    }
}

// This code is contributed by ghanshyampandey
```

## 蟒蛇 3

```
# Python3 program to find Sum of elements
# in an array having prime frequency
import math as mt

# Function to create Sieve to
# check primes
def SieveOfEratosthenes(prime, p_size):

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    for p in range(2, mt.ceil(mt.sqrt(p_size + 1))):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size + 1, p):
                prime[i] = False

# Function to return the Sum of elements
# in an array having prime frequency
def SumOfElements(arr, n):
    prime = [True for i in range(n + 1)]
    SieveOfEratosthenes(prime, n + 1)

    i, j = 0, 0

    # Map is used to store
    # element frequencies
    m = dict()
    for i in range(n):
        if arr[i] in m.keys():
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1

    Sum = 0

    # Traverse the map using iterators
    for i in m:

        # Count the number of elements
        # having prime frequencies
        if (prime[m[i]]):
            Sum += (i)

    return Sum

# Driver code
arr = [5, 4, 6, 5, 4, 6 ]
n = len(arr)
print(SumOfElements(arr, n))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to find sum of elements
// in an array having prime frequency
using System;
using System.Collections.Generic;

class GFG
{

    // Function to create Sieve to check primes
    static void SieveOfEratosthenes(bool []prime, int p_size)
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
                for (int i = p * 2; i <= p_size; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to return the sum of elements
    // in an array having prime frequency
    static int sumOfElements(int []arr, int n)
    {
        bool []prime = new bool[n + 1];
        for(int i = 0; i < n+1; i++)
            prime[i] = true;

        SieveOfEratosthenes(prime, n + 1);

        // Map is used to store
        // element frequencies
        Dictionary<int,int> m = new Dictionary<int,int>();
        for (int i = 0 ; i < n; i++)
        {
            if(m.ContainsKey(arr[i]))
            {
                var val = m[arr[i]];
                m.Remove(arr[i]);
                m.Add(arr[i], val + 1);
            }
            else
            {
                m.Add(arr[i], 1);
            }
        }

        int sum = 0;

        // Traverse the map
        foreach(KeyValuePair<int, int> entry in m)
        {
            int key = entry.Key;
            int value = entry.Value;

            // Count the number of elements
            // having prime frequencies
            if (prime[value])
            {
                sum += (key);
            }
        }

        return sum;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 5, 4, 6, 5, 4, 6 };
        int n = arr.Length;

        Console.WriteLine(sumOfElements(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find sum of elements
// in an array having prime frequency

// Function to create Sieve to check primes
function SieveOfEratosthenes(prime, p_size)
{

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
}

// Function to return the sum of elements
// in an array having prime frequency
function sumOfElements(arr, n) {
    let prime = new Array(n + 1);
    prime.fill(true)

    SieveOfEratosthenes(prime, n + 1);

    let i, j;

    // Map is used to store
    // element frequencies
    let m = new Map();
    for (i = 0; i < n; i++) {
        if (m.has(arr[i]))
            m.set(arr[i], m.get(arr[i]) + 1);
        else
            m.set(arr[i], 1);
    }

    let sum = 0;

    // Traverse the map using iterators
    for (let it of m) {

        // Count the number of elements
        // having prime frequencies
        if (prime[it[1]]) {
            sum += (it[0]);
        }
    }

    return sum;
}

// Driver code

let arr = [5, 4, 6, 5, 4, 6];
let n = arr.length;

document.write(sumOfElements(arr, n));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
15
```