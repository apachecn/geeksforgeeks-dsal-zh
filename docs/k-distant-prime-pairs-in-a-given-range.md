# 给定范围内的 K 个远素数对

> 原文:[https://www . geesforgeks . org/k-远距素对给定范围/](https://www.geeksforgeeks.org/k-distant-prime-pairs-in-a-given-range/)

给定两个整数 **L、R** 和一个整数 **K** ，任务是打印给定范围内所有成对的[质数](https://www.geeksforgeeks.org/prime-numbers/)，其差值为 **K** 。

**示例:**

> **输入:** L = 1，R = 19，K = 6
> **输出:** (5，11) (7，13) (11，17) (13，19)
> **说明:**差 6 的素数对是(5，11)，(7，13)，(11，17)和(13，19)。
> 
> **输入:** L = 4，R = 13，K = 2
> **输出:** (5，7) (11，13)
> **说明:**差 2 的素数对是(5，7)和(11，13)。

**天真方法:**最简单的方法是从给定范围生成所有可能的有差异的对 **K** ，并检查这两个对元素是否都是[质数](https://www.geeksforgeeks.org/prime-numbers/)。如果存在这样的配对，那么打印该配对。

***时间复杂度:**O(sqrt((N))*(R–L+1)<sup>2</sup>，其中 N 为**【L，R】**范围内的任意数字。*
***辅助空间:** O(1)*

**高效途径:**对上述途径进行优化，思路是利用厄拉多塞的[筛，找出给定范围**【L，R】**内的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)，存储在[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **M** 中。现在，遍历 **M** 中的每个值(比如 **val** ，如果 **(val + K)** 也出现在地图 **M** 中，则打印该对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate prime numbers
// in the given range [L, R]
void findPrimeNos(int L, int R,
                  unordered_map<int,
                                int>& M)
{
    // Store all value in the range
    for (int i = L; i <= R; i++) {
        M[i]++;
    }

    // Erase 1 as its non-prime
    if (M.find(1) != M.end()) {
        M.erase(1);
    }

    // Perform Sieve of Eratosthenes
    for (int i = 2; i <= sqrt(R); i++) {

        int multiple = 2;

        while ((i * multiple) <= R) {

            // Find current multiple
            if (M.find(i * multiple)
                != M.end()) {

                // Erase as it is a
                // non-prime
                M.erase(i * multiple);
            }

            // Increment multiple
            multiple++;
        }
    }
}

// Function to print all the prime pairs
// in the given range that differs by K
void getPrimePairs(int L, int R, int K)
{
    unordered_map<int, int> M;

    // Generate all prime number
    findPrimeNos(L, R, M);

    // Traverse the Map M
    for (auto& it : M) {

        // If it.first & (it.first + K)
        // is prime then print this pair
        if (M.find(it.first + K)
            != M.end()) {
            cout << "(" << it.first
                 << ", "
                 << it.first + K
                 << ") ";
        }
    }
}

// Driver Code
int main()
{
    // Given range
    int L = 1, R = 19;

    // Given K
    int K = 6;

    // Function Call
    getPrimePairs(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class solution{

// Function to generate prime
// numbers in the given range [L, R]
static void findPrimeNos(int L, int R,
                         Map<Integer,
                             Integer> M,
                         int K)
{
  // Store all value in the range
  for (int i = L; i <= R; i++)
  {
    if(M.get(i) != null)
      M.put(i, M.get(i) + 1);
    else
      M.put(i, 1);
  }

  // Erase 1 as its
  // non-prime
  if (M.get(1) != null)
  {
    M.remove(1);
  }

  // Perform Sieve of
  // Eratosthenes
  for (int i = 2;
           i <= Math.sqrt(R); i++)
  {
    int multiple = 2;

    while ((i * multiple) <= R)
    {
      // Find current multiple
      if (M.get(i * multiple) != null)
      {
        // Erase as it is a
        // non-prime
        M.remove(i * multiple);
      }

      // Increment multiple
      multiple++;
    }
  }

  // Traverse the Map M
  for (Map.Entry<Integer,
                 Integer> entry :
       M.entrySet()) 
  {
    // If it.first & (it.first + K)
    // is prime then print this pair

    if (M.get(entry.getKey() + K) != null)
    {
      System.out.print("(" + entry.getKey() +
                       ", " + (entry.getKey() +
                       K) + ") ");
    }
  }
}

// Function to print all
// the prime pairs in the
// given range that differs by K
static void getPrimePairs(int L,
                          int R, int K)
{
  Map<Integer,
      Integer> M = new HashMap<Integer,
                               Integer>(); 

  // Generate all prime number
  findPrimeNos(L, R, M, K);
}

// Driver Code
public static void main(String args[])
{
  // Given range
  int L = 1, R = 19;

  // Given K
  int K = 6;

  // Function Call
  getPrimePairs(L, R, K);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to generate prime numbers
# in the given range [L, R]
def findPrimeNos(L, R, M):

    # Store all value in the range
    for i in range(L, R + 1):
        M[i] = M.get(i, 0) + 1

    # Erase 1 as its non-prime
    if (1 in M):
        M.pop(1)

    # Perform Sieve of Eratosthenes
    for i in range(2, int(sqrt(R)) + 1, 1):
        multiple = 2

        while ((i * multiple) <= R):

            # Find current multiple
            if ((i * multiple) in M):

                # Erase as it is a
                # non-prime
                M.pop(i * multiple)

            # Increment multiple
            multiple += 1

# Function to print all the prime pairs
# in the given range that differs by K
def getPrimePairs(L, R, K):

    M = {}

    # Generate all prime number
    findPrimeNos(L, R, M)

    # Traverse the Map M
    for key, values in M.items():

        # If it.first & (it.first + K)
        # is prime then print this pair
        if ((key + K) in M):
            print("(", key, ",",
                  key + K, ")", end = " ")

# Driver Code
if __name__ == '__main__':

    # Given range
    L = 1
    R = 19

    # Given K
    K = 6

    # Function Call
    getPrimePairs(L, R, K)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class solution{

// Function to generate prime
// numbers in the given range [L, R]
static void findPrimeNos(int L, int R,
                         Dictionary<int,
                         int> M, int K)
{
  // Store all value in the range
  for (int i = L; i <= R; i++)
  {
      if(M.ContainsKey(i))
      M.Add(i, M[i] + 1);
    else
      M.Add(i, 1);
  }

  // Erase 1 as its
  // non-prime
  if (M[1] != 0)
  {
    M.Remove(1);
  }

  // Perform Sieve of
  // Eratosthenes
  for (int i = 2;
           i <= Math.Sqrt(R); i++)
  {
    int multiple = 2;

    while ((i * multiple) <= R)
    {
      // Find current multiple
      if (M.ContainsKey(i * multiple))
      {
        // Erase as it is a
        // non-prime
        M.Remove(i * multiple);
      }

      // Increment multiple
      multiple++;
    }
  }

  // Traverse the Map M
  foreach (KeyValuePair<int, 
                        int> entry in  M) 
  {
    // If it.first & (it.first + K)
    // is prime then print this pair

    if (M.ContainsKey(entry.Key + K))
    {
      Console.Write("(" + entry.Key +
                    ", " + (entry.Key +
                    K) + ") ");
    }
  }
}

// Function to print all
// the prime pairs in the
// given range that differs by K
static void getPrimePairs(int L,
                          int R, int K)
{
  Dictionary<int,
             int> M = new Dictionary<int,
                                     int>(); 

  // Generate all prime number
  findPrimeNos(L, R, M, K);
}

// Driver Code
public static void Main(String []args)
{
  // Given range
  int L = 1, R = 19;

  // Given K
  int K = 6;

  // Function Call
  getPrimePairs(L, R, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to generate prime numbers
// in the given range [L, R]
function findPrimeNos(L, R, M)
{

    // Store all value in the range
    for(var i = L; i <= R; i++)
    {
        if (M.has(i))
            M.set(i, M.get(i) + 1)
        else
            M.set(i, 1)
    }

    // Erase 1 as its non-prime
    if (M.has(1))
    {
        M.delete(1);
    }

    // Perform Sieve of Eratosthenes
    for(var i = 2; i <= parseInt(Math.sqrt(R)); i++)
    {
        var multiple = 2;

        while ((i * multiple) <= R)
        {

            // Find current multiple
            if (M.has(i * multiple))
            {

                // Erase as it is a
                // non-prime
                M.delete(i * multiple);
            }

            // Increment multiple
            multiple++;
        }
    }
    return M;
}

// Function to print all the prime pairs
// in the given range that differs by K
function getPrimePairs(L, R,  K)
{
    var M = new Map();

    // Generate all prime number
    M = findPrimeNos(L, R, M);

    // Traverse the Map M
    M.forEach((value, key) => {

        // If it.first & (it.first + K)
        // is prime then print this pair
        if (M.has(key + K))
        {
            document.write("(" + key + ", " +
                          (key + K) + ") ");
        }
    });
}

// Driver Code

// Given range
var L = 1, R = 19;

// Given K
var K = 6;

// Function Call
getPrimePairs(L, R, K);

// This code is contributed by rutvik_56

</script>
```

**Output**

```
(5, 11) (7, 13) (11, 17) (13, 19) 
```

***时间复杂度:**O(N * log *(log(N))+sqrt(R–L))，其中 N = R–L+1*
***辅助空间:** O(N)*