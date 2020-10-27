# 使用分段筛的最长质数子数组

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是找到最长的子数组，其中该子数组中的所有数字均为质数。
**范例：**

> **输入：** arr [] = {3，5，2，66，7，11，8}
> **输出：** 3
> **说明：**
> 最大连续素数序列为{2，3，5}
> 
> **输入：** arr [] = {1,2,11,32,8,9}
> **输出：** 2
> **说明：** ]最大连续素数序列为{2，11}

**方法：**
对于按 **10 <sup>6</sup>** 顺序排列的数组元素，我们在[本文的](https://www.geeksforgeeks.org/maximum-no-of-contiguous-prime-numbers-in-an-array/)[中讨论了一种方法。
对于按 **10 <sup>9</sup>** 顺序排列的数组元素，想法是使用](https://www.geeksforgeeks.org/maximum-no-of-contiguous-prime-numbers-in-an-array/)[分段筛](https://www.geeksforgeeks.org/segmented-sieve/)查找[质数](https://www.geeksforgeeks.org/prime-numbers/) 值最高为 **10 <sup>9</sup>** 。
**步骤**：

1.  使用本文中讨论的方法，在数组的最小元素和最大元素的范围之间找到[质数](https://www.geeksforgeeks.org/prime-numbers/)。
2.  在计算出[范围之间的素数](https://www.geeksforgeeks.org/prime-numbers/)之后。 可以使用 [Kadane 算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来计算具有[质数](https://www.geeksforgeeks.org/prime-numbers/)的最长子数组。 步骤如下：
    *   使用名为 **current_max** 和 **max_so_far** 的两个变量遍历给定数组 **arr []** 。
    *   如果找到素数，则增加 **current_max** 并将其与 **max_so_far** 进行比较。
    *   如果 **current_max** 大于 **max_so_far** ，则将 max_so_far 更新为 **current_max** 。
    *   如果有任何元素不是主要元素，则将 **current_max** 重置为 0。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find longest subarray
// of prime numbers
#include <bits/stdc++.h>
using namespace std;

// To store the prime numbers
unordered_set<int> allPrimes;

// Function that find prime numbers
// till limit
void simpleSieve(int limit,
                 vector<int>& prime)
{
    bool mark[limit + 1];
    memset(mark, false, sizeof(mark));

    // Find primes using
    // Sieve of Eratosthenes
    for (int i = 2; i <= limit; ++i) {
        if (mark[i] == false) {
            prime.push_back(i);
            for (int j = i; j <= limit;
                 j += i) {
                mark[j] = true;
            }
        }
    }
}

// Function that finds all prime
// numbers in given range using
// Segmented Sieve
void primesInRange(int low, int high)
{
    // Find the limit
    int limit = floor(sqrt(high)) + 1;

    // To store the prime numbers
    vector<int> prime;

    // Comput all primes less than
    // or equals to sqrt(high)
    // using Simple Sieve
    simpleSieve(limit, prime);

    // Count the elements in the
    // range [low, high]
    int n = high - low + 1;

    // Declaring boolean for the
    // range [low, high]
    bool mark[n + 1];

    // Initialise bool[] to false
    memset(mark, false, sizeof(mark));

    // Traverse the prime numbers till
    // limit
    for (int i = 0; i < prime.size(); i++) {

        int loLim = floor(low / prime[i]);
            loLim
            *= prime[i];

        // Find the minimum number in
        // [low..high] that is a
        // multiple of prime[i]
        if (loLim < low) {
            loLim += prime[i];
        }

        if (loLim == prime[i]) {
            loLim += prime[i];
        }

        // Mark the multiples of prime[i]
        // in [low, high] as true
        for (int j = loLim; j <= high;
             j += prime[i])
            mark[j - low] = true;
    }

    // Element which are not marked in
    // range are Prime
    for (int i = low; i <= high; i++) {
        if (!mark[i - low]) {
            allPrimes.insert(i);
        }
    }
}

// Function that finds longest subarray
// of prime numbers
int maxPrimeSubarray(int arr[], int n)
{
    int current_max = 0;
    int max_so_far = 0;

    for (int i = 0; i < n; i++) {

        // If element is Non-prime then
        // updated current_max to 0
        if (!allPrimes.count(arr[i]))
            current_max = 0;

        // If element is prime, then
        // update current_max and
        // max_so_far
        else {
            current_max++;
            max_so_far = max(current_max,
                             max_so_far);
        }
    }

    // Return the count of longest
    // subarray
    return max_so_far;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 3, 29,
                  11, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Find minimum and maximum element
    int max_el = *max_element(arr, arr + n);
    int min_el = *min_element(arr, arr + n);

    // Find prime in the range
    // [min_el, max_el]
    primesInRange(min_el, max_el);

    // Function call
    cout << maxPrimeSubarray(arr, n);
    return 0;
}

```

## Python3

```py

# Python3 program to find longest subarray 
# of prime numbers 
import math

# To store the prime numbers
allPrimes = set()

# Function that find prime numbers 
# till limit 
def simpleSieve(limit, prime):

    mark = [False] * (limit + 1)

    # Find primes using 
    # Sieve of Eratosthenes
    for i in range(2, limit + 1):
        if mark[i] == False:
            prime.append(i)

            for j in range(i, limit + 1, i):
                mark[j] = True

# Function that finds all prime 
# numbers in given range using 
# Segmented Sieve
def primesInRange(low, high):

    # Find the limit
    limit = math.floor(math.sqrt(high)) + 1

    # To store the prime numbers
    prime = []

    # Compute all primes less than 
    # or equals to sqrt(high) 
    # using Simple Sieve 
    simpleSieve(limit, prime)

    # Count the elements in the 
    # range [low, high] 
    n = high - low + 1

    # Declaring and initializing boolean 
    # for the range[low,high] to False
    mark = [False] * (n + 1)

    # Traverse the prime numbers till 
    # limit 
    for i in range(len(prime)):
        loLim = low // prime[i]
        loLim *= prime[i]

        # Find the minimum number in 
        # [low..high] that is a 
        # multiple of prime[i] 
        if loLim < low:
            loLim += prime[i]

        if loLim == prime[i]: 
            loLim += prime[i]

        # Mark the multiples of prime[i] 
        # in [low, high] as true 
        for j in range(loLim, high + 1, prime[i]):
            mark[j - low] = True

    # Element which are not marked in 
    # range are Prime
    for i in range(low, high + 1):
        if not mark[i - low]:
            allPrimes.add(i)

# Function that finds longest subarray 
# of prime numbers 
def maxPrimeSubarray(arr, n):

    current_max = 0
    max_so_far = 0

    for i in range(n):

        # If element is Non-prime then 
        # updated current_max to 0 
        if arr[i] not in allPrimes:
            current_max = 0

        # If element is prime, then 
        # update current_max and 
        # max_so_far 
        else:
            current_max += 1
            max_so_far = max(current_max, 
                             max_so_far)

    # Return the count of longest 
    # subarray 
    return max_so_far

# Driver Code
arr = [ 1, 2, 4, 3, 29, 11, 7, 8, 9 ]
n = len(arr)

# Find minimum and maximum element 
max_el = max(arr)
min_el = min(arr)

# Find prime in the range 
# [min_el, max_el] 
primesInRange(min_el, max_el)

# Function call 
print(maxPrimeSubarray(arr, n))

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program to find longest subarray
// of prime numbers
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// To store the prime numbers
static HashSet<int> allPrimes = new HashSet<int>();

// Function that find prime numbers
// till limit
static void simpleSieve(int limit,
                        ref ArrayList prime)
{
    bool []mark = new bool[limit + 1];
    Array.Fill(mark, false);

    // Find primes using
    // Sieve of Eratosthenes
    for(int i = 2; i <= limit; ++i)
    {
        if (mark[i] == false) 
        {
            prime.Add(i);
            for(int j = i; j <= limit; j += i) 
            {
                mark[j] = true;
            }
        }
    }
}

// Function that finds all prime
// numbers in given range using
// Segmented Sieve
static void primesInRange(int low, int high)
{

    // Find the limit
    int limit = (int)Math.Floor(Math.Sqrt(high)) + 1;

    // To store the prime numbers
    ArrayList prime = new ArrayList();

    // Comput all primes less than
    // or equals to sqrt(high)
    // using Simple Sieve
    simpleSieve(limit, ref prime);

    // Count the elements in the
    // range [low, high]
    int n = high - low + 1;

    // Declaring boolean for the
    // range [low, high]
    bool []mark = new bool[n + 1];

    // Initialise bool[] to false
    Array.Fill(mark, false);

    // Traverse the prime numbers till
    // limit
    for(int i = 0; i < prime.Count; i++) 
    {
        int loLim = (int)Math.Floor((double)low / 
                                    (int)prime[i]);
            loLim *= (int)prime[i];

        // Find the minimum number in
        // [low..high] that is a
        // multiple of prime[i]
        if (loLim < low)
        {
            loLim += (int)prime[i];
        }

        if (loLim == (int)prime[i]) 
        {
            loLim += (int)prime[i];
        }

        // Mark the multiples of prime[i]
        // in [low, high] as true
        for(int j = loLim; j <= high;
                j += (int)prime[i])
            mark[j - low] = true;
    }

    // Element which are not marked in
    // range are Prime
    for(int i = low; i <= high; i++)
    {
        if (!mark[i - low]) 
        {
            allPrimes.Add(i);
        }
    }
}

// Function that finds longest subarray
// of prime numbers
static int maxPrimeSubarray(int []arr, int n)
{
    int current_max = 0;
    int max_so_far = 0;

    for(int i = 0; i < n; i++)
    {

        // If element is Non-prime then
        // updated current_max to 0
        if (!allPrimes.Contains(arr[i]))
            current_max = 0;

        // If element is prime, then
        // update current_max and
        // max_so_far
        else
        {
            current_max++;
            max_so_far = Math.Max(current_max,
                                  max_so_far);
        }
    }

    // Return the count of longest
    // subarray
    return max_so_far;
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 1, 2, 4, 3, 29,
                  11, 7, 8, 9 };
    int n = arr.Length;

    // Find minimum and maximum element
    int max_el = Int32.MinValue;
    int min_el = Int32.MaxValue;

    for(int i = 0; i < n; i++)
    {
        if (arr[i] < min_el)
        {
            min_el = arr[i];
        }
        if (arr[i] > max_el)
        {
            max_el = arr[i];
        }
    }

    // Find prime in the range
    // [min_el, max_el]
    primesInRange(min_el, max_el);

    // Function call
    Console.Write(maxPrimeSubarray(arr, n));
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
4

```

**时间复杂度：** O（N），其中 N 是数组的长度。
**辅助空间：** O（N），其中 N 是数组的长度。



* * *

* * *



