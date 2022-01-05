# 计算给定数组中的复合斐波那契数

> 原文:[https://www . geesforgeks . org/count-composite-Fibonacci-numbers-from-given-array/](https://www.geeksforgeeks.org/count-composite-fibonacci-numbers-from-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中存在的[复合](https://www.geeksforgeeks.org/composite-number/) [斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。

**示例:**

> **输入:** arr[] = {13，55，7，3，5，21，233，144，6}
> **输出:** 55 21 144
> **解释:**
> 复合数组元素为{55，21，144，6}。
> 斐波那契数组元素为{55，21，144}。
> 因此，既复合又斐波那契的数组元素是{55，21，144}。
> 
> **输入:** arr[] = {34，13，11，8，3，55，233}
> **输出:** 3
> **解释:**
> 复合数组元素为{34，8，55}
> 斐波那契数组元素为{34，8，55}
> 因此，既复合又斐波那契的数组元素为{34，8，55}。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，说 **Max** 来存储数组中最大的[元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   创建一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储所有[斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)到**最大值**。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**筛【】**，使用厄拉多塞的[筛存储所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质数](https://www.geeksforgeeks.org/prime-numbers/)。
*   最后，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查当前数组元素是否同时为[复合](https://www.geeksforgeeks.org/composite-number/)和[斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。如果发现为真，则打印当前元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all Fibonacci
// numbers up to Max
set<int> createhashmap(int Max)
{
    // Store all Fibonacci numbers
    // upto Max
    set<int> hashmap;

    // Stores previous element
    // of Fibonacci sequence
    int curr = 1;

    // Stores previous element
    // of Fibonacci sequence
    int prev = 0;

    // Insert prev into hashmap
    hashmap.insert(prev);

    // Insert all the Fibonacci
    // numbers up to Max
    while (curr <= Max) {

        // Insert curr into hashmap
        hashmap.insert(curr);

        // Stores curr into temp
        int temp = curr;

        // Update curr
        curr = curr + prev;

        // Update prev
        prev = temp;
    }

    return hashmap;
}

// Function to find all Composite
// numbers up to Max
vector<bool> SieveOfEratosthenes(
    int Max)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    vector<bool> isPrime(Max, true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for (int p = 2; p * p <= Max; p++) {

        // If P is a prime number
        if (isPrime[p]) {

            // Set all multiple of P
            // as non-prime
            for (int i = p * p; i <= Max;
                 i += p) {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to find the numbers which is
// both a composite and Fibonacci number
int cntFibonacciPrime(int arr[], int N)
{

    // Stores the largest element
    // of the array
    int Max = arr[0];

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // Update Max
        Max = max(Max, arr[i]);
    }

    // isPrim[i] check i is
    // a prime number or not
    vector<bool> isPrime
        = SieveOfEratosthenes(Max);

    // Stores all the Fibonacci numbers
    set<int> hashmap
        = createhashmap(Max);

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // current element is not
        // a composite number
        if (arr[i] == 1)
            continue;

        // If current element is a Fibonacci
        // and composite number
        if ((hashmap.count(arr[i]))
            && !isPrime[arr[i]]) {

            // Print current element
            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 13, 55, 7, 3, 5, 21,
                  233, 144, 89 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cntFibonacciPrime(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static  boolean[] isPrime;

// Function to find all
// Fibonacci numbers up
// to Max
static HashSet<Integer>
       createhashmap(int Max)
{
  // Store all Fibonacci numbers
  // upto Max
  HashSet<Integer> hashmap =
          new HashSet<>();

  // Stores previous element
  // of Fibonacci sequence
  int curr = 1;

  // Stores previous element
  // of Fibonacci sequence
  int prev = 0;

  // Insert prev into hashmap
  hashmap.add(prev);

  // Insert all the Fibonacci
  // numbers up to Max
  while (curr < Max)
  {
    // Insert curr into
    // hashmap
    hashmap.add(curr);

    // Stores curr into
    // temp
    int temp = curr;

    // Update curr
    curr = curr + prev;

    // Update prev
    prev = temp;
  }

  return hashmap;
}

// Function to find all
// Composite numbers up
// to Max
static void SieveOfEratosthenes(int Max)
{
  // isPrime[i]: Stores if i is
  // a prime number or not
  isPrime = new boolean[Max];
  Arrays.fill(isPrime, true);

  isPrime[0] = false;
  isPrime[1] = false;

  // Calculate all prime numbers
  // up to Max using Sieve of
  // Eratosthenes
  for (int p = 2;
           p * p <= Max; p++)
  {
    // If P is a prime number
    if (isPrime[p])
    {
      // Set all multiple of P
      // as non-prime
      for (int i = p * p; i <= Max;
               i += p)
      {   
        // Update isPrime
        isPrime[i] = false;
      }
    }
  }
}

// Function to find the numbers which is
// both a composite and Fibonacci number
static void cntFibonacciPrime(int arr[],
                              int N)
{
  // Stores the largest element
  // of the array
  int Max = arr[0];

  // Traverse the array arr[]
  for (int i = 1; i < N; i++)
  {
    // Update Max
    Max = Math.max(Max, arr[i]);
  }

  // isPrim[i] check i is
  // a prime number or not
  SieveOfEratosthenes(Max);

  // Stores all the Fibonacci
  // numbers
  HashSet<Integer> hashmap =
          createhashmap(Max);

  // Traverse the array arr[]
  for (int i = 0; i < N; i++)
  {
    // current element is not
    // a composite number
    if (arr[i] == 1)
      continue;

    // If current element is a
    // Fibonacci and composite
    // number
    if ((hashmap.contains(arr[i])) &&
        !isPrime[arr[i]])
    {
      // Print current element
      System.out.print(arr[i] + " ");
    }
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {13, 55, 7, 3, 5,
               21, 233, 144, 89};
  int N = arr.length;
  cntFibonacciPrime(arr, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to find all Fibonacci
# numbers up to Max
def createhashmap(Max):

    # Store all Fibonacci numbers
    # upto Max
    hashmap = {""}

    # Stores previous element
    # of Fibonacci sequence
    curr = 1

    # Stores previous element
    # of Fibonacci sequence
    prev = 0

    # Insert prev into hashmap
    hashmap.add(prev)

    # Insert all the Fibonacci
    # numbers up to Max
    while (curr <= Max):

        # Insert curr into hashmap
        hashmap.add(curr)

        # Stores curr into temp
        temp = curr

        # Update curr
        curr = curr + prev

        # Update prev
        prev = temp

    return hashmap

# Function to find all Composite
# numbers up to Max
def SieveOfEratosthenes(Max):

    # isPrime[i]: Stores if i is
    # a prime number or not
    isPrime = [1 for x in range(Max + 1)]
    isPrime[0] = 0
    isPrime[1] = 0

    # Calculate all prime numbers up to
    # Max using Sieve of Eratosthenes
    for p in range(0, int(math.sqrt(Max))):

        # If P is a prime number
        if (isPrime[p]):

            # Set all multiple of P
            # as non-prime
            for i in range(2 * p, Max, p):
                 isPrime[i] = 0

    return isPrime

# Function to find the numbers which is
# both a composite and Fibonacci number
def cntFibonacciPrime(arr, N):

    # Stores the largest element
    # of the array
    Max = arr[0]

    # Traverse the array arr[]
    for i in range(0, N):

        # Update Max
        Max = max(Max, arr[i])

    # isPrim[i] check i is
    # a prime number or not
    isPrime = SieveOfEratosthenes(Max)

    # Stores all the Fibonacci numbers
    hashmap = createhashmap(Max)

    # Traverse the array arr[]
    for i in range(0, N):

        # Current element is not
        # a composite number
        if arr[i] == 1:
            continue

        # If current element is a Fibonacci
        # and composite number
        if ((arr[i] in hashmap) and
            (not(isPrime[arr[i]]))):

             # Print current element
             print(arr[i], end = " ")

# Driver Code
arr = [ 13, 55, 7, 3, 5,
        21, 233, 144, 89 ]
N = len(arr)

cntFibonacciPrime(arr, N)

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static bool[] isPrime;

// Function to find all
// Fibonacci numbers up
// to Max
static HashSet<int> createhashmap(int Max)
{

  // Store all Fibonacci numbers
  // upto Max
  HashSet<int> hashmap = new HashSet<int>();

  // Stores previous element
  // of Fibonacci sequence
  int curr = 1;

  // Stores previous element
  // of Fibonacci sequence
  int prev = 0;

  // Insert prev into hashmap
  hashmap.Add(prev);

  // Insert all the Fibonacci
  // numbers up to Max
  while (curr < Max)
  {

    // Insert curr into
    // hashmap
    hashmap.Add(curr);

    // Stores curr into
    // temp
    int temp = curr;

    // Update curr
    curr = curr + prev;

    // Update prev
    prev = temp;
  }
  return hashmap;
}

// Function to find all
// Composite numbers up
// to Max
static void SieveOfEratosthenes(int Max)
{

  // isPrime[i]: Stores if i is
  // a prime number or not
  isPrime = new bool[Max];
  for(int i = 0;i<Max;i++)
    isPrime[i] = true;

  isPrime[0] = false;
  isPrime[1] = false;

  // Calculate all prime numbers
  // up to Max using Sieve of
  // Eratosthenes
  for(int p = 2; p * p <= Max; p++)
  {

    // If P is a prime number
    if (isPrime[p])
    {

      // Set all multiple of P
      // as non-prime
      for(int i = p * p; i <= Max;
              i += p)
      { 

        // Update isPrime
        isPrime[i] = false;
      }
    }
  }
}

// Function to find the numbers which is
// both a composite and Fibonacci number
static void cntFibonacciPrime(int []arr,
                              int N)
{

  // Stores the largest element
  // of the array
  int Max = arr[0];

  // Traverse the array []arr
  for(int i = 1; i < N; i++)
  {

    // Update Max
    Max = Math.Max(Max, arr[i]);
  }

  // isPrim[i] check i is
  // a prime number or not
  SieveOfEratosthenes(Max);

  // Stores all the Fibonacci
  // numbers
  HashSet<int> hashmap = createhashmap(Max);

  // Traverse the array []arr
  for(int i = 0; i < N; i++)
  {

    // current element is not
    // a composite number
    if (arr[i] == 1)
      continue;

    // If current element is a
    // Fibonacci and composite
    // number
    if ((hashmap.Contains(arr[i])) &&
        !isPrime[arr[i]])
    {

      // Print current element
      Console.Write(arr[i] + " ");
    }
  }
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = { 13, 55, 7, 3, 5,
                21, 233, 144, 89 };
  int N = arr.Length;

  cntFibonacciPrime(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find all Fibonacci
// numbers up to Max
function createhashmap(Max)
{

    // Store all Fibonacci numbers
    // upto Max
    var hashmap = new Set();

    // Stores previous element
    // of Fibonacci sequence
    var curr = 1;

    // Stores previous element
    // of Fibonacci sequence
    var prev = 0;

    // Insert prev into hashmap
    hashmap.add(prev);

    // Insert all the Fibonacci
    // numbers up to Max
    while (curr <= Max)
    {

        // Insert curr into hashmap
        hashmap.add(curr);

        // Stores curr into temp
        var temp = curr;

        // Update curr
        curr = curr + prev;

        // Update prev
        prev = temp;
    }
    return hashmap;
}

// Function to find all Composite
// numbers up to Max
function SieveOfEratosthenes(Max)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    var isPrime = Array(Max + 1).fill(true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for(var p = 2; p * p <= Max; p++)
    {

        // If P is a prime number
        if (isPrime[p])
        {

            // Set all multiple of P
            // as non-prime
            for(var i = p * p; i <= Max;
                    i += p)
            {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to find the numbers which is
// both a composite and Fibonacci number
function cntFibonacciPrime(arr, N)
{

    // Stores the largest element
    // of the array
    var Max = arr[0];

    // Traverse the array arr[]
    for(var i = 1; i < N; i++)
    {

        // Update Max
        Max = Math.max(Max, arr[i]);
    }

    // isPrim[i] check i is
    // a prime number or not
    var isPrime = SieveOfEratosthenes(Max);

    // Stores all the Fibonacci numbers
    var hashmap = createhashmap(Max);

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {

        // current element is not
        // a composite number
        if (arr[i] == 1)
            continue;

        // If current element is a Fibonacci
        // and composite number
        if (hashmap.has(arr[i]) &&
               !isPrime[arr[i]])
        {

            // Print current element
            document.write( arr[i] + " ");
        }
    }
}

// Driver Code
var arr = [ 13, 55, 7, 3, 5, 21,
            233, 144, 89 ];
var N = arr.length;

cntFibonacciPrime(arr, N);

// This code is contributed by itsok

</script>
```

**Output:** 

```
55 21 144
```

***时间复杂度:** O(N + Max * log(log(Max))，其中 **Max** 是数组中最大的元素*
***辅助空间:** O(N)*