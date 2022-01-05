# N 个数乘积的除数

> 原文:[https://www . geesforgeks . org/n-numbers 的除数/](https://www.geeksforgeeks.org/number-of-divisors-of-product-of-n-numbers/)

给定一个整数数组 **arr[]** ，任务是计算给定数组中所有元素乘积的除数[数](https://www.geeksforgeeks.org/total-number-divisors-given-number/)。
**例:**

> **输入:** arr[] = {3，5，7 }
> T3】输出: 8
> 3 * 5 * 7 = 105。
> 105 的因子为 1、3、5、7、15、21、35、105。
> **输入:** arr[] = {5，5}
> **输出:** 3
> 5 * 5 = 25。
> 25 的因子为 1、5、25。

一个**简单的解法**是将所有 **N** 个整数相乘，计算乘积的除数。然而，如果产品超过了 **10 <sup>7</sup>** ，那么我们就不能使用这种方法，因为大于 10^7 的数不能用筛方法有效地进行素因子分解。
一个**高效解**不涉及所有数字乘积的计算。我们已经知道，当我们乘以 2 的时候，乘方就会相加。例如

> A = 2 <sup>7</sup> ，B = 2<sup>3</sup>
> A * B = 2<sup>10</sup>
> 因此，我们需要保持数字乘积中每一次幂的计数，这可以通过将每个元素的幂的计数相加来完成。

因此，要计算除数，主要的焦点是遇到的素数。因此，我们将只强调产品中遇到的质数，而不关心产品本身。遍历数组时，我们会记录遇到的每个素数。

> 除数=**(p<sub>1</sub>+1)*(p<sub>2</sub>+1)*(p<sub>3</sub>+1)*……*(p<sub>n</sub>+1)**
> 其中 p <sub>1</sub> ，p <sub>2</sub> ，p <sub>3</sub> ，…，p <sub>n</sub> 是在所有元素的素因式分解中遇到的素

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MAX 10000002

using namespace std;
int prime[MAX];

// Array to store count of primes
int prime_count[MAX];

// Function to store smallest prime factor
// of every number till MAX
void sieve()
{
    memset(prime, 0, sizeof(prime));
    prime[0] = prime[1] = 1;
    for (int i = 2; i * i < MAX; i++) {
        if (prime[i] == 0) {
            for (int j = i * 2; j < MAX; j += i) {
                if (prime[j] == 0)
                    prime[j] = i;
            }
        }
    }
    for (int i = 2; i < MAX; i++) {

        // If the number is prime then it's
        // smallest prime factor is the number
        // itself
        if (prime[i] == 0)
            prime[i] = i;
    }
}

// Function to return the count of the divisors for
// the product of all the numbers from the array
long long numberOfDivisorsOfProduct(const int* arr,
                                           int n)
{
    memset(prime_count, 0, sizeof(prime_count));

    for (int i = 0; i < n; i++) {
        int temp = arr[i];
        while (temp != 1) {

            // Increase the count of prime
            // encountered
            prime_count[prime[temp]]++;
            temp = temp / prime[temp];
        }
    }

    long long ans = 1;

    // Multiplying the count of primes
    // encountered
    for (int i = 2; i < MAX; i++) {
        ans = ans * (prime_count[i] + 1);
    }

    return ans;
}

// Driver code
int main()
{
    sieve();
    int arr[] = { 2, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << numberOfDivisorsOfProduct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.Arrays;

// Java implementation of the approach
class GFG {

    final static int MAX = 10000002;

    static int prime[] = new int[MAX];

// Array to store count of primes
    static int prime_count[] = new int[MAX];

// Function to store smallest prime factor
// of every number till MAX
    static void sieve() {
        Arrays.fill(prime, 0, MAX, 0);
        prime[0] = prime[1] = 1;
        for (int i = 2; i * i < MAX; i++) {
            if (prime[i] == 0) {
                for (int j = i * 2; j < MAX; j += i) {
                    if (prime[j] == 0) {
                        prime[j] = i;
                    }
                }
            }
        }
        for (int i = 2; i < MAX; i++) {

            // If the number is prime then it's
            // smallest prime factor is the number
            // itself
            if (prime[i] == 0) {
                prime[i] = i;
            }
        }
    }

// Function to return the count of the divisors for
// the product of all the numbers from the array
    static long numberOfDivisorsOfProduct(int[] arr,
            int n) {
        Arrays.fill(prime_count, 0, MAX, 0);

        for (int i = 0; i < n; i++) {
            int temp = arr[i];
            while (temp != 1) {

                // Increase the count of prime
                // encountered
                prime_count[prime[temp]]++;
                temp = temp / prime[temp];
            }
        }

        long ans = 1;

        // Multiplying the count of primes
        // encountered
        for (int i = 2; i < MAX; i++) {
            ans = ans * (prime_count[i] + 1);
        }

        return ans;
    }

// Driver code
    public static void main(String[] args) {
        sieve();
        int arr[] = {2, 4, 6};
        int n = arr.length;
        System.out.println(numberOfDivisorsOfProduct(arr, n));

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 10000002
prime = [0] * (MAX)
MAX_sqrt = int(MAX ** (0.5))

# Array to store count of primes
prime_count = [0] * (MAX)

# Function to store smallest prime
# factor in prime[]
def sieve():

    prime[0], prime[1] = 1, 1
    for i in range(2, MAX_sqrt):
        if prime[i] == 0:
            for j in range(i * 2, MAX, i):
                if prime[j] == 0:
                    prime[j] = i

    for i in range(2, MAX):

        # If the number is prime then it's
        # the smallest prime factor is the
        # number itself
        if prime[i] == 0:
            prime[i] = i

# Function to return the count of the divisors for
# the product of all the numbers from the array
def numberOfDivisorsOfProduct(arr, n):

    for i in range(0, n):
        temp = arr[i]
        while temp != 1:

            # Increase the count of prime
            # encountered
            prime_count[prime[temp]] += 1
            temp = temp // prime[temp]

    ans = 1

    # Multiplying the count of primes
    # encountered
    for i in range(2, len(prime_count)):
        ans = ans * (prime_count[i] + 1)

    return ans

# Driver code
if __name__ == "__main__":

    sieve()
    arr = [2, 4, 6]
    n = len(arr)
    print(numberOfDivisorsOfProduct(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    static int MAX = 1000000;

    static int []prime = new int[MAX];

// Array to store count of primes
    static int []prime_count = new int[MAX];

// Function to store smallest prime factor
// of every number till MAX
    static void sieve() { 
        for(int i =0;i<MAX;i++)
            prime[i]=0;
        prime[0] = prime[1] = 1;
        for (int i = 2; i * i < MAX; i++) {
            if (prime[i] == 0) {
                for (int j = i * 2; j < MAX; j += i) {
                    if (prime[j] == 0) {
                        prime[j] = i;
                    }
                }
            }
        }
        for (int i = 2; i < MAX; i++) {

            // If the number is prime then it's
            // smallest prime factor is the number
            // itself
            if (prime[i] == 0) {
                prime[i] = i;
            }
        }
    }

// Function to return the count of the divisors for
// the product of all the numbers from the array
    static long numberOfDivisorsOfProduct(int[] arr,
            int n) { 
        for(int i =0;i<MAX;i++)
            prime_count[i]=0;
        for (int i = 0; i < n; i++) {
            int temp = arr[i];
            while (temp != 1) {

                // Increase the count of prime
                // encountered
                prime_count[prime[temp]]++;
                temp = temp / prime[temp];
            }
        }

        long ans = 1;

        // Multiplying the count of primes
        // encountered
        for (int i = 2; i < MAX; i++) {
            ans = ans * (prime_count[i] + 1);
        }

        return ans;
    }

// Driver code
    public static void Main() {
        sieve();
        int []arr = {2, 4, 6};
        int n = arr.Length;
        Console.Write(numberOfDivisorsOfProduct(arr, n));

    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 10000002

let prime = new Array(MAX);

// Array to store count of primes
let prime_count = new Array(MAX);

// Function to store smallest prime factor
// of every number till MAX
function sieve() {
    prime.fill(0)
    prime[0] = prime[1] = 1;
    for (let i = 2; i * i < MAX; i++) {
        if (prime[i] == 0) {
            for (let j = i * 2; j < MAX; j += i) {
                if (prime[j] == 0)
                    prime[j] = i;
            }
        }
    }
    for (let i = 2; i < MAX; i++) {

        // If the number is prime then it's
        // smallest prime factor is the number
        // itself
        if (prime[i] == 0)
            prime[i] = i;
    }
}

// Function to return the count of the divisors for
// the product of all the numbers from the array
function numberOfDivisorsOfProduct(arr, n) {
    prime_count.fill(0)

    for (let i = 0; i < n; i++) {
        let temp = arr[i];
        while (temp != 1) {

            // Increase the count of prime
            // encountered
            prime_count[prime[temp]]++;
            temp = temp / prime[temp];
        }
    }

    let ans = 1;

    // Multiplying the count of primes
    // encountered
    for (let i = 2; i < MAX; i++) {
        ans = ans * (prime_count[i] + 1);
    }

    return ans;
}

// Driver code

sieve();
let arr = [2, 4, 6];
let n = arr.length;
document.write(numberOfDivisorsOfProduct(arr, n));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
10
```

在**内存高效的**方法中，数组可以被**无序映射**代替，以只存储已经遇到的那些素数的计数。
下面是内存高效方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MAX 10000002

using namespace std;
int prime[MAX];

// Map to store count of primes
unordered_map<int, int> prime_count;

// Function to store smallest prime factor
// in prime[]
void sieve()
{
    memset(prime, 0, sizeof(prime));
    prime[0] = prime[1] = 1;
    for (int i = 2; i * i < MAX; i++) {
        if (prime[i] == 0) {
            for (int j = i * 2; j < MAX; j += i) {
                if (prime[j] == 0)
                    prime[j] = i;
            }
        }
    }
    for (int i = 2; i < MAX; i++) {

        // If the number is prime then
        // it's the smallest prime factor
        // is the number itself
        if (prime[i] == 0)
            prime[i] = i;
    }
}

// Function to return the count of the divisors for
// the product of all the numbers from the array
long long numberOfDivisorsOfProduct(const int* arr,
                                            int n)
{

    for (int i = 0; i < n; i++) {
        int temp = arr[i];
        while (temp != 1) {

            // Increase the count of prime
            // encountered
            prime_count[prime[temp]]++;
            temp = temp / prime[temp];
        }
    }

    long long ans = 1;

    // Multiplying the count of primes
    // encountered
    unordered_map<int, int>::iterator it;
    for (it = prime_count.begin();
         it != prime_count.end(); it++) {
        ans = ans * (it->second + 1);
    }

    return ans;
}

// Driver code
int main()
{
    sieve();
    int arr[] = { 3, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << numberOfDivisorsOfProduct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
static int MAX = 10000002;
static int []prime = new int[MAX];

// Map to store count of primes
static Map<Integer, Integer> prime_count = new HashMap<>();

// Function to store smallest prime factor
// in prime[]
static void sieve()
{
    prime[0] = 1;
    prime[1] = 1;
    for (int i = 2; i * i < MAX; i++)
    {
        if (prime[i] == 0)
        {
            for (int j = i * 2; j < MAX; j += i)
            {
                if (prime[j] == 0)
                    prime[j] = i;
            }
        }
    }
    for (int i = 2; i < MAX; i++)
    {

        // If the number is prime then
        // it's the smallest prime factor
        // is the number itself
        if (prime[i] == 0)
            prime[i] = i;
    }
}

// Function to return the count of the divisors for
// the product of all the numbers from the array
static long numberOfDivisorsOfProduct(int arr[],
                                            int n)
{

    for (int i = 0; i < n; i++)
    {
        int temp = arr[i];
        while (temp != 1)
        {

            // Increase the count of prime
            // encountered
            if(!prime_count.containsKey(prime[temp]))
            {
                prime_count.put(prime[temp], 0);   
            }
            prime_count.put(prime[temp], prime_count.get(prime[temp]) + 1);
            temp = temp / prime[temp];
        }
    }
    long ans = 1;

    // Multiplying the count of primes
    // encountered
    for(Map.Entry<Integer,Integer> it : prime_count.entrySet())
    {
        ans = ans * (it.getValue() + 1);
    }
    return ans;
}

// Driver code
public static void main(String []args)
{
    sieve();
    int arr[] = new int[] { 3, 5, 7 };
    int n = arr.length;
    System.out.print(numberOfDivisorsOfProduct(arr, n));
}
}

// This code is contributed by rutvik_56.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

MAX = 10000002
prime = [0] * (MAX)
MAX_sqrt = int(MAX ** (0.5))

# Map to store count of primes
prime_count = defaultdict(lambda:0)

# Function to store smallest prime
# factor in prime[]
def sieve():

    prime[0], prime[1] = 1, 1
    for i in range(2, MAX_sqrt):
        if prime[i] == 0:
            for j in range(i * 2, MAX, i):
                if prime[j] == 0:
                    prime[j] = i

    for i in range(2, MAX):

        # If the number is prime then
        # it's the smallest prime factor
        # is the number itself
        if prime[i] == 0:
            prime[i] = i

# Function to return the count of the divisors for
# the product of all the numbers from the array
def numberOfDivisorsOfProduct(arr, n):

    for i in range(0, n):
        temp = arr[i]
        while temp != 1:

            # Increase the count of prime
            # encountered
            prime_count[prime[temp]] += 1
            temp = temp // prime[temp]

    ans = 1

    # Multiplying the count of primes
    # encountered
    for key in prime_count:
        ans = ans * (prime_count[key] + 1)

    return ans

# Driver code
if __name__ == "__main__":

    sieve()
    arr = [3, 5, 7]
    n = len(arr)
    print(numberOfDivisorsOfProduct(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG
{

  static int MAX = 10000002;
  static int []prime = new int[MAX];

  // Map to store count of primes
  static Dictionary<int,int> prime_count = new Dictionary<int,int>();

  // Function to store smallest prime factor
  // in prime[]
  static void sieve()
  {
    prime[0] = 1;
    prime[1] = 1;
    for (int i = 2; i * i < MAX; i++)
    {
      if (prime[i] == 0)
      {
        for (int j = i * 2; j < MAX; j += i)
        {
          if (prime[j] == 0)
            prime[j] = i;
        }
      }
    }
    for (int i = 2; i < MAX; i++)
    {

      // If the number is prime then
      // it's the smallest prime factor
      // is the number itself
      if (prime[i] == 0)
        prime[i] = i;
    }
  }

  // Function to return the count of the divisors for
  // the product of all the numbers from the array
  static long numberOfDivisorsOfProduct(int []arr,
                                        int n)
  {

    for (int i = 0; i < n; i++)
    {
      int temp = arr[i];
      while (temp != 1)
      {

        // Increase the count of prime
        // encountered
        if(!prime_count.ContainsKey(prime[temp]))
        {
          prime_count[prime[temp]] = 0;   
        }
        prime_count[prime[temp]] += 1;   
        temp = temp / prime[temp];
      }
    }
    long ans = 1;

    // Multiplying the count of primes
    // encountered
    foreach(KeyValuePair<int,int> it in prime_count)
    {
      ans = ans * (it.Value + 1);
    }
    return ans;
  }

  // Driver code
  public static void Main(string []args)
  {
    sieve();
    int []arr = new int[] { 3, 5, 7 };
    int n = arr.Length;
    Console.Write(numberOfDivisorsOfProduct(arr, n));
  }
}

// This code is contributed by pratham76.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let MAX = 10000002;

let prime = new Array(MAX);
for(let i=0;i<MAX;i++)
    prime[i]=0;

// Map to store count of primes
let prime_count = new Map();

// Function to store smallest prime factor
// in prime[]
function sieve()
{
    prime[0] = 1;
    prime[1] = 1;
    for (let i = 2; i * i < MAX; i++)
    {
        if (prime[i] == 0)
        {
            for (let j = i * 2; j < MAX; j += i)
            {
                if (prime[j] == 0)
                    prime[j] = i;
            }
        }
    }
    for (let i = 2; i < MAX; i++)
    {

        // If the number is prime then
        // it's the smallest prime factor
        // is the number itself
        if (prime[i] == 0)
            prime[i] = i;
    }
}

// Function to return the count of the divisors for
// the product of all the numbers from the array
function numberOfDivisorsOfProduct(arr,n)
{
    for (let i = 0; i < n; i++)
    {
        let temp = arr[i];
        while (temp != 1)
        {

            // Increase the count of prime
            // encountered
            if(!prime_count.has(prime[temp]))
            {
                prime_count.set(prime[temp], 0);  
            }
            prime_count.set(prime[temp], prime_count.get(prime[temp]) + 1);
            temp = Math.floor(temp / prime[temp]);
        }
    }
    let ans = 1;

    // Multiplying the count of primes
    // encountered
    for(let it of prime_count.values())
    {
        ans = ans * (it + 1);
    }
    return ans;
}

// Driver code
sieve();
let arr = [ 3, 5, 7 ];
let n = arr.length;
document.write(numberOfDivisorsOfProduct(arr, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
8
```