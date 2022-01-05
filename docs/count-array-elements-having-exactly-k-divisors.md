# 计数正好有 K 除数的数组元素

> 原文:[https://www . geeksforgeeks . org/count-array-elements-having-just-k-dividers/](https://www.geeksforgeeks.org/count-array-elements-having-exactly-k-divisors/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算正好具有 **K** 个除数的数组元素的数量。

**示例:**

> **输入:** N = 5，arr[] = { 3，6，2，9，4 }，K = 2
> **输出:** 2
> **说明:** arr[0] (= 3)和 arr[2] (= 2)正好有 2 个除数。
> 
> **输入:** N = 5，arr[] = { 3，6，2，9，4 }，K = 3
> **输出:** 2
> **说明:** arr[3] (= 9)和 arr[4] (= 4)正好有 3 个除数

**方法:**解决这个问题的思路是计算每个数组元素的[除数总数](https://www.geeksforgeeks.org/total-number-divisors-given-number/)，并将其存储在**地图**中。然后，[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数组元素，检查是否正好有 **K** 除数。打印此类数字的计数。按照以下步骤解决问题:

*   [找到数组中存在的最大元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)。
*   初始化一个数组**质数[]** 。
*   使用厄拉多塞的[筛将范围**【2】**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[**内存在的所有**质数**存储在数组**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**中的最大元素**质数**中。**
*   **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[使用给定的公式对每个数组元素进行素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/):**

**[![](img/6942c9229d7ce0910153a7fa509b5243.png)](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-8bcae33d8d9b84c13a2f77f132a31eb5_l3.svg)**

**其中*a<sub>I</sub>T3】是[质因数](https://www.geeksforgeeks.org/prime-factor/)和*p<sub>I</sub>T9】是它们所对应的积分幂。****

*   **使用以下公式计算每个数组元素的除数总数:**

**[![](img/83a68a84693cc3b7d5db5baa9b63fd78.png)](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-f441246827323a14504121a27496962b_l3.svg)**

*   **初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储每个数组元素的除数总数。**
*   **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并初始化一个变量，比如说**计数**，到**计数正好有 **K** 除数总数的元素数量**。**
*   **打印精确具有 **K** 除数的元素数量。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores prime numbers
// using Sieve of Eratosthenes
bool prime[100000];

// Function to find the maximum element
int maximumElement(int arr[], int N)
{
  // Stores the maximum element
  // of the array
  int max = arr[0];

  // Traverse the array
  for (int i = 0; i < N; i++) {

    // If current element
    // is maximum so far
    if (max < arr[i]) {

      // Update maximum
      max = arr[i];
    }
  }

  // Return maximum element
  return max;
}

// Function to find the prime numbers
// using sieve of eratosthenes algorithm
void sieveOfEratosthenes(int max)
{
  // Calculate primes using Sieve
  memset(prime, true, max+1);

  for (int p = 2; p * p < max; p++)

    // If current element is prime
    if (prime[p] == true)

      // Make all multiples non-prime
      for (int i = p * 2; i < max; i += p)
        prime[i] = false;
}

// Function to count divisors of n
int divCount(int n)
{

  // Traversing through
  // all prime numbers
  int total = 1;
  for (int p = 2; p <= n; p++) {

    // If it is a prime number
    if (prime[p]) {

      // Calculate number of divisors
      // with the formula
      // number of divisors = (p1 + 1) * (p2 + 1)
      // *.....* (pn + 1)
      // n = (a1 ^ p1) * (a2 ^ p2) .... *(an ^ pn)
      // ai: prime divisor of n
      // pi: power in factorization
      int count = 0;

      if (n % p == 0) {

        while (n % p == 0) {
          n = n / p;
          count++;
        }
        total = total * (count + 1);
      }
    }
  }

  // Return the total number of divisors
  return total;
}

// Function to count array elements
// having exactly K divisors
int countElements(int arr[], int N, int K)
{

  // Initialize a map to store
  // count of divisors of array elements
  map<int, int> map;

  // Traverse the array
  for (int i = 0; i < N; i++) {

    // If element is not already present in
    // the Map, then insert it into the Map
    if (map.find(arr[i]) == map.end()) {
      // Function call to count the total
      // number of divisors
      map.insert({arr[i], divCount(arr[i])});
    }
  }

  // Stores the number of
  // elements with divisor K
  int count = 0;

  // Traverse the array
  for (int i = 0; i < N; i++) {

    // If current element
    // has exactly K divisors
    if (map.at(arr[i]) == K) {
      count++;
    }
  }

  // Return the number of
  // elements having K divisors
  return count;
}

// Driver Code
int main()
{

  int arr[] = { 3, 6, 2, 9, 4 };
  int N = sizeof(arr) / sizeof(arr[0]);
  int K = 2;

  // Find the maximum element
  int max = maximumElement(arr, N);

  // Generate all prime numbers
  sieveOfEratosthenes(max);

  cout << countElements(arr, N, K);

  return 0;
}

// This code is contributed by Dharanendra L V
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Stores prime numbers
    // using Sieve of Eratosthenes
    public static boolean prime[];

    // Function to find the maximum element
    public static int maximumElement(
        int arr[], int N)
    {
        // Stores the maximum element
        // of the array
        int max = arr[0];

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If current element
            // is maximum so far
            if (max < arr[i]) {

                // Update maximum
                max = arr[i];
            }
        }

        // Return maximum element
        return max;
    }

    // Function to find the prime numbers
    // using sieve of eratosthenes algorithm
    public static void sieveOfEratosthenes(int max)
    {
        // Initialize primes having
        // size of maximum element + 1
        prime = new boolean[max + 1];

        // Calculate primes using Sieve
        Arrays.fill(prime, true);

        for (int p = 2; p * p < max; p++)

            // If current element is prime
            if (prime[p] == true)

                // Make all multiples non-prime
                for (int i = p * 2; i < max; i += p)
                    prime[i] = false;
    }

    // Function to count divisors of n
    public static int divCount(int n)
    {

        // Traversing through
        // all prime numbers
        int total = 1;
        for (int p = 2; p <= n; p++) {

            // If it is a prime number
            if (prime[p]) {

                // Calculate number of divisors
                // with the formula
                // number of divisors = (p1 + 1) * (p2 + 1)
                // *.....* (pn + 1)
                // n = (a1 ^ p1) * (a2 ^ p2) .... *(an ^ pn)
                // ai: prime divisor of n
                // pi: power in factorization
                int count = 0;

                if (n % p == 0) {

                    while (n % p == 0) {
                        n = n / p;
                        count++;
                    }
                    total = total * (count + 1);
                }
            }
        }

        // Return the total number of divisors
        return total;
    }

    // Function to count array elements
    // having exactly K divisors
    public static int countElements(
        int arr[], int N, int K)
    {

        // Initialize a map to store
        // count of divisors of array elements
        Map<Integer, Integer> map
            = new HashMap<Integer, Integer>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If element is not already present in
            // the Map, then insert it into the Map
            if (!map.containsKey(arr[i])) {
                // Function call to count the total
                // number of divisors
                map.put(arr[i], divCount(arr[i]));
            }
        }

        // Stores the number of
        // elements with divisor K
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If current element
            // has exactly K divisors
            if (map.get(arr[i]) == K) {
                count++;
            }
        }

        // Return the number of
        // elements having K divisors
        return count;
    }

    // Driver Code
    public static void main(
        String[] args)
    {
        int arr[] = { 3, 6, 2, 9, 4 };
        int N = arr.length;
        int K= 2;

        // Find the maximum element
        int max = maximumElement(arr, N);

        // Generate all prime numbers
        sieveOfEratosthenes(max);

        System.out.println(countElements(arr, N, K));
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Stores prime numbers
# using Sieve of Eratosthenes

# Function to find the maximum element
def maximumElement(arr, N):

    # Stores the maximum element
    # of the array
    max = arr[0]

    # Traverse the array
    for i in range(N):

        # If current element
        # is maximum so far
        if (max < arr[i]):

            # Update maximum
            max = arr[i]

    # Return maximum element
    return max

# Function to find the prime numbers
# using sieve of eratosthenes algorithm
def sieveOfEratosthenes(max):
    global prime
    for p in range(2, max + 1):
        if p * p > max:
            break

        # If current element is prime
        if (prime[p] == True):

            # Make all multiples non-prime
            for i in range(2 * p, max, p):
                prime[i] = False
    return prime

# Function to count divisors of n
def divCount(n):

    # Traversing through
    # all prime numbers
    total = 1
    for p in range(2, n + 1):

        # If it is a prime number
        if (prime[p]):

            # Calculate number of divisors
            # with the formula
            # number of divisors = (p1 + 1) * (p2 + 1)
            # *.....* (pn + 1)
            # n = (a1 ^ p1) * (a2 ^ p2) .... *(an ^ pn)
            # ai: prime divisor of n
            # pi: power in factorization
            count = 0

            if (n % p == 0):
                while (n % p == 0):
                    n = n // p
                    count += 1
                total = total * (count + 1)

    # Return the total number of divisors
    return total

# Function to count array elements
# having exactly K divisors
def countElements(arr, N, K):

    # Initialize a map to store
    # count of divisors of array elements
    mp = {}

    # Traverse the array
    for i in range(N):

        # If element is not already present in
        # the Map, then insert it into the Map
        if (arr[i] not in mp):

            # Function call to count the total
            # number of divisors
            mp[arr[i]] = divCount(arr[i])

    # Stores the number of
    # elements with divisor K
    count = 0

    # Traverse the array
    for i in range(N):

        # If current element
        # has exactly K divisors
        if (mp[arr[i]] == K):
            count += 1

    # Return the number of
    # elements having K divisors
    return count

# Driver Code
if __name__ == '__main__':
    prime = [True for i in range(10**6)]
    arr = [3, 6, 2, 9, 4]
    N = len(arr)
    K= 2

    # Find the maximum element
    max = maximumElement(arr, N)

    # Generate all prime numbers
    prime = sieveOfEratosthenes(max)
    print(countElements(arr, N, K))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Stores prime numbers
    // using Sieve of Eratosthenes
    public static bool []prime;

    // Function to find the maximum element
    public static int maximumElement(
        int []arr, int N)
    {

        // Stores the maximum element
        // of the array
        int max = arr[0];

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If current element
            // is maximum so far
            if (max < arr[i])
            {

                // Update maximum
                max = arr[i];
            }
        }

        // Return maximum element
        return max;
    }

    // Function to find the prime numbers
    // using sieve of eratosthenes algorithm
    public static void sieveOfEratosthenes(int max)
    {

        // Initialize primes having
        // size of maximum element + 1
        prime = new bool[max + 1];

        // Calculate primes using Sieve
        for (int i = 0; i < prime.Length; i++)
        prime[i] = true;
        for (int p = 2; p * p < max; p++)

            // If current element is prime
            if (prime[p] == true)

                // Make all multiples non-prime
                for (int i = p * 2; i < max; i += p)
                    prime[i] = false;
    }

    // Function to count divisors of n
    public static int divCount(int n)
    {

        // Traversing through
        // all prime numbers
        int total = 1;
        for (int p = 2; p <= n; p++)
        {

            // If it is a prime number
            if (prime[p])
            {

                // Calculate number of divisors
                // with the formula
                // number of divisors = (p1 + 1) * (p2 + 1)
                // *.....* (pn + 1)
                // n = (a1 ^ p1) * (a2 ^ p2) .... *(an ^ pn)
                // ai: prime divisor of n
                // pi: power in factorization
                int count = 0;
                if (n % p == 0)
                {
                    while (n % p == 0)
                    {
                        n = n / p;
                        count++;
                    }
                    total = total * (count + 1);
                }
            }
        }

        // Return the total number of divisors
        return total;
    }

    // Function to count array elements
    // having exactly K divisors
    public static int countElements(int []arr,
                                    int N, int K)
    {

        // Initialize a map to store
        // count of divisors of array elements
        Dictionary<int, int> map
            = new Dictionary<int, int>();

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If element is not already present in
            // the Map, then insert it into the Map
            if (!map.ContainsKey(arr[i]))
            {

                // Function call to count the total
                // number of divisors
                map.Add(arr[i], divCount(arr[i]));
            }
        }

        // Stores the number of
        // elements with divisor K
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If current element
            // has exactly K divisors
            if (map[arr[i]] == K)
            {
                count++;
            }
        }

        // Return the number of
        // elements having K divisors
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = {3, 6, 2, 9, 4};
        int N = arr.Length;
        int K= 2;

        // Find the maximum element
        int max = maximumElement(arr, N);

        // Generate all prime numbers
        sieveOfEratosthenes(max);
        Console.WriteLine(countElements(arr, N, K));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Stores prime numbers
// using Sieve of Eratosthenes
let prime = new Array(100000);

// Function to find the maximum element
function maximumElement(arr, N)
{
// Stores the maximum element
// of the array
let max = arr[0];

// Traverse the array
for (let i = 0; i < N; i++) {

    // If current element
    // is maximum so far
    if (max < arr[i]) {

    // Update maximum
    max = arr[i];
    }
}

// Return maximum element
return max;
}

// Function to find the prime numbers
// using sieve of eratosthenes algorithm
function sieveOfEratosthenes(max)
{
// Calculate primes using Sieve
prime.fill(true, 0, max + 1)

for (let p = 2; p * p < max; p++)

    // If current element is prime
    if (prime[p] == true)

    // Make all multiples non-prime
    for (let i = p * 2; i < max; i += p)
        prime[i] = false;
}

// Function to count divisors of n
function divCount(n)
{

// Traversing through
// all prime numbers
let total = 1;
for (let p = 2; p <= n; p++) {

    // If it is a prime number
    if (prime[p]) {

    // Calculate number of divisors
    // with the formula
    // number of divisors = (p1 + 1) * (p2 + 1)
    // *.....* (pn + 1)
    // n = (a1 ^ p1) * (a2 ^ p2) .... *(an ^ pn)
    // ai: prime divisor of n
    // pi: power in factorization
    let count = 0;

    if (n % p == 0) {

        while (n % p == 0) {
        n = n / p;
        count++;
        }
        total = total * (count + 1);
    }
    }
}

// Return the total number of divisors
return total;
}

// Function to count array elements
// having exactly K divisors
function countElements(arr, N, K)
{

// Initialize a map to store
// count of divisors of array elements
let map = new Map();

// Traverse the array
for (let i = 0; i < N; i++) {

    // If element is not already present in
    // the Map, then insert it into the Map
    if (!map.has(arr[i])) {
    // Function call to count the total
    // number of divisors
    map.set(arr[i], divCount(arr[i]));
    }
}

// Stores the number of
// elements with divisor K
let count = 0;

// Traverse the array
for (let i = 0; i < N; i++) {

    // If current element
    // has exactly K divisors
    if (map.get(arr[i]) == K) {
    count++;
    }
}

// Return the number of
// elements having K divisors
return count;
}

// Driver Code

let arr = [ 3, 6, 2, 9, 4 ];
let N = arr.length;
let K = 2;

// Find the maximum element
let max = maximumElement(arr, N);

// Generate all prime numbers
sieveOfEratosthenes(max);

document.write(countElements(arr, N, K));

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N + maxlog(log(max) + log(max))，其中 **max** 为最大数组元素。*
***辅助空间:** O(max)，其中 **max** 为最大阵元。***