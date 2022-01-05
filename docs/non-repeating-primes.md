# 非重复素数

> 原文:[https://www.geeksforgeeks.org/non-repeating-primes/](https://www.geeksforgeeks.org/non-repeating-primes/)

给定一个包含重复质数和非质数的数组 **arr[]** ，任务是找出只出现一次的质数。

**示例:**

> **输入:** arr[] = {2，3，4，6，7，9，7，23，21，2，3}
> **输出:** 23
> **解释:**
> 在给定数组中，23 是唯一出现一次的素数。
> 
> **输入:** arr[] = {17，19，7，5，29，5，2，2，7，17，19}
> **输出:** 29
> **说明:**
> 在给定数组中，29 是唯一出现一次的素数。

**天真方法:**要解决上面提到的问题，解决方法是检查每个元素是否是质数。如果它是质数，那么检查它是否只出现一次。一旦找到一个出现一次的主元素，就打印它。

***时间复杂度:** O(N <sup>2</sup> )*

**高效方法:**上述方法可以使用[筛选](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)和[哈希算法](https://www.geeksforgeeks.org/hashing-in-java/)进一步优化。

1.  在[散列表](https://www.geeksforgeeks.org/hashing-data-structure/)中使用筛预计算并存储质数。
2.  还要创建一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 来存储数字及其频率。
3.  逐一遍历数组中的所有元素，然后:
    *   使用 O(1)中的筛散列表检查当前数字是否为质数。
    *   如果数字是质数，那么增加它在 HashMap 中的频率。
4.  遍历 HashMap，打印所有频率为 1 的数字。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// Non-repeating Primes

import java.util.*;

class GFG {

    // Function to find count of prime
    static Vector<Boolean> findPrimes(
        int arr[], int n)
    {
        // Find maximum value in the array
        int max_val = Arrays
                          .stream(arr)
                          .max()
                          .getAsInt();

        // Find and store all prime numbers
        // up to max_val using Sieve

        // Create a boolean array "prime[0..n]".
        // A value in prime[i]
        // will finally be false
        // if i is Not a prime, else true.
        Vector<Boolean> prime
            = new Vector<>(max_val + 1);

        for (int i = 0; i < max_val + 1; i++)
            prime.add(i, Boolean.TRUE);

        // Remaining part of SIEVE
        prime.add(0, Boolean.FALSE);
        prime.add(1, Boolean.FALSE);
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime.get(p) == true) {

                // Update all multiples of p
                for (int i = p * 2;
                     i <= max_val;
                     i += p)
                    prime.add(i, Boolean.FALSE);
            }
        }

        return prime;
    }

    // Function to print
    // Non-repeating primes
    static void nonRepeatingPrimes(
        int arr[], int n)
    {

        // Precompute primes using Sieve
        Vector<Boolean> prime
            = findPrimes(arr, n);

        // Create HashMap to store
        // frequency of prime numbers
        HashMap<Integer, Integer> mp
            = new HashMap<>();

        // Traverse through array elements and
        // Count frequencies of all primes
        for (int i = 0; i < n; i++) {
            if (prime.get(arr[i]))
                if (mp.containsKey(arr[i]))
                    mp.put(arr[i],
                           mp.get(arr[i]) + 1);
                else
                    mp.put(arr[i], 1);
        }

        // Traverse through map and
        // print non repeating primes
        for (Map.Entry<Integer, Integer>
                 entry : mp.entrySet()) {
            if (entry.getValue() == 1)
                System.out.println(
                    entry.getKey());
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 6, 7, 9,
                      7, 23, 21, 3 };
        int n = arr.length;

        nonRepeatingPrimes(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# Non-repeating Primes

# Function to find count of prime
def findPrimes( arr, n):

    # Find maximum value in the array
    max_val =  max(arr)

    # Find and store all prime numbers
    # up to max_val using Sieve
    # Create a boolean array "prime[0..n]".
    # A value in prime[i]
    # will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    p = 2
    while(p * p <= max_val):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p): 
                prime[i] = False
        p += 1     
    return prime;

# Function to print
# Non-repeating primes
def nonRepeatingPrimes(arr, n):

    # Precompute primes using Sieve
    prime = findPrimes(arr, n);

    # Create HashMap to store
    # frequency of prime numbers
    mp = dict()

    # Traverse through array elements and
    # Count frequencies of all primes
    for i in range(n):  
        if (prime[arr[i]]):
            if (arr[i] in mp):
                mp[arr[i]] += 1
            else:
                mp[arr[i]] = 1

    # Traverse through map and
    # print non repeating primes
    for entry in mp.keys():
        if (mp[entry] == 1):
            print(entry);

# Driver code
if __name__ == '__main__':
    arr = [ 2, 3, 4, 6, 7, 9, 7, 23, 21, 3]
    n = len(arr)
    nonRepeatingPrimes(arr, n);

# This code is contributed by pratham76.
```

## C#

```
// C# program to find
// Non-repeating Primes
using System;
using System.Collections;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to find count of prime
static List<bool> findPrimes(int []arr, int n)
{

    // Find maximum value in the array
    int max_val = arr.Max();

    // Find and store all prime numbers
    // up to max_val using Sieve

    // Create a boolean array "prime[0..n]".
    // A value in prime[i]
    // will finally be false
    // if i is Not a prime, else true.
    List<bool> prime = new List<bool>(max_val + 1);

    for(int i = 0; i < max_val + 1; i++)
        prime.Add(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * 2;
                    i <= max_val;
                    i += p)
                prime[i] = false;
        }
    }
    return prime;
}

// Function to print
// Non-repeating primes
static void nonRepeatingPrimes(int []arr, int n)
{

    // Precompute primes using Sieve
    List<bool> prime = findPrimes(arr, n);

    // Create HashMap to store
    // frequency of prime numbers
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse through array elements and
    // Count frequencies of all primes
    for(int i = 0; i < n; i++)
    {
        if (prime[arr[i]])
            if (mp.ContainsKey(arr[i]))
                mp[arr[i]]++;
            else
                mp.Add(arr[i], 1);
    }

    // Traverse through map and
    // print non repeating primes
    foreach(KeyValuePair<int, int> entry in mp)
    {
        if (entry.Value == 1)
            Console.WriteLine(entry.Key);
    }
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 2, 3, 4, 6, 7, 9,
                  7, 23, 21, 3 };
    int n = arr.Length;

    nonRepeatingPrimes(arr, n);
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
2
23
```

***时间复杂度:**O(O(n * log(log(n))))*
***辅助空间:** O(K)，其中 K 是数组中最大的值。*