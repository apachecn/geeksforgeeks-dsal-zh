# 检查数字是否为质数

> 原文:[https://www . geesforgeks . org/check-如果数字是质数幂数/](https://www.geeksforgeeks.org/check-if-the-number-is-a-prime-power-number/)

给定一个整数 **N** ，任务是检查这个数是否是素数的幂。如果是，则打印数字及其等于 n 的幂，否则打印-1。

> 素数的幂是单个素数的正整数幂。
> 例如:7 = 7 <sup>1</sup> 、9 = 3 <sup>2</sup> 和 32 = 2 <sup>5</sup> 是素数的幂，而 6 = 2 × 3、12 = 22 × 3 和 36 = 62 = 22 × 32 则不是。(数字 1 不算质数。)

**注意:**如果没有这样的质数，打印-1。

**示例:**

> **输入:** N = 49
> **输出:** 7 <sup>2</sup>
> 说明:
> N 可以表示为素数 7 的幂。
> N = 49 = 7 <sup>2</sup>
> 
> **输入:** N = 100
> **输出:** -1
> **说明:**
> N 不能表示为任意素数的幂。

**方法:**思路是用厄拉多塞的[筛找出所有质数。然后，迭代所有质数，检查是否有任何质数除以给定的数 N，如果有，则除以它，直到它变成 1 或不能被那个质数整除。最后，检查该数是否等于 1，如果是，则返回质数，否则给定的数不能表示为某次幂的质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation to check if
// a number is a prime power number
#include<bits/stdc++.h>
using namespace std;

// Array to store the
// prime numbers
bool is_prime[1000001];
vector<int> primes;

// Function to mark the prime
// numbers using Sieve of
// Eratosthenes
void SieveOfEratosthenes(int n)
{
    int p = 2;

    for(int i = 0; i < n; i++)
       is_prime[i] = true;

    while (p * p <= n)
    {

        // If prime[p] is not
        // changed, then it is a prime
        if (is_prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * p; i < n + 1; i += p)
            {
               is_prime[i] = false;
            }
        }
        p += 1;
    }
    for(int i = 2; i < n + 1; i++)
    {
       if (is_prime[i])
           primes.push_back(i);
    }
}

// Function to check if the
// number can be represented
// as a power of prime
pair<int, int> power_of_prime(int n)
{
    for(auto i : primes)
    {

       if (n % i == 0)
       {
           int c = 0;
           while(n % i == 0)
           {
               n /= i;
               c += 1;
           }
           if(n == 1)
              return {i, c};
           else
              return {-1, 1};
       }
    }
}

// Driver Code        
int main()
{
    int n = 49;
    SieveOfEratosthenes(int(sqrt(n)) + 1);

    // Function Call
    pair<int, int> p = power_of_prime(n);

    if (p.first > 1)
        cout << p.first << " ^ "
             << p.second << endl;
    else
        cout << -1 << endl;
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if 
// a number is a prime power number
import java.io.*;
import java.util.*;
import java.lang.Math;

class GFG{

// Array to store the 
// prime numbers    
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Function to mark the prime 
// numbers using Sieve of 
// Eratosthenes
public static void sieveOfEratosthenes(int n)
{

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    boolean prime[] = new boolean[n + 1];

    for(int i = 0; i < n; i++)
        prime[i] = true;

    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if(prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for(int i = 2; i <= n; i++)
    {
        if(prime[i] == true)
            primes.add(i);
    }
}

// Function to check if the 
// number can be represented 
// as a power of prime
public static int[] power_of_prime(int n)
{
    for(int ii = 0; ii < primes.size(); ii++)
    {
        int i = primes.get(ii);

        if (n % i == 0)
        {
            int c = 0;
            while(n % i == 0)
            {
                n /= i;
                c += 1;
            }

            if(n == 1)
                return new int[]{i, c};
            else
                return new int[]{-1, 1};
        }
    }
    return new int[]{-1, 1};
}

// Driver code
public static void main(String args[])
{
    int n = 49;
    int sq = (int)(Math.sqrt(n));
    sieveOfEratosthenes(sq + 1);

    // Function call
    int arr[] = power_of_prime(n);

    if (arr[0] > 1)
        System.out.println(arr[0] + " ^ " + arr[1]);
    else
        System.out.println("-1");
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number is a prime power number

from math import *

# Array to store the
# prime numbers
is_prime = [True for i in range(10**6 + 1)]
primes =[]

# Function to mark the prime
# numbers using Sieve of
# Eratosthenes
def SieveOfEratosthenes(n):
    p = 2
    while (p * p <= n):
        # If prime[p] is not
        # changed, then it is a prime
        if (is_prime[p] == True):
            # Update all multiples of p
            for i in range(p * p, n + 1, p):
                is_prime[i] = False
        p += 1
    for i in range(2, n + 1):
        if is_prime[i]:
            primes.append(i)

# Function to check if the
# number can be represented
# as a power of prime
def power_of_prime(n):
    for i in primes:
        if n % i == 0:
            c = 0
            while n % i == 0:
                n//= i
                c += 1
            if n == 1:
                return (i, c)
            else:
                return (-1, 1)

# Driver Code        
if __name__ == "__main__":
    n = 49
    SieveOfEratosthenes(int(sqrt(n))+1)

    # Function Call
    num, power = power_of_prime(n)
    if num > 1:
        print(num, "^", power)
    else:
        print(-1)
```

## C#

```
// C# implementation to check if
// a number is a prime power number
using System;
using System.Collections;

class GFG{

// Array to store the
// prime numbers    
static ArrayList primes = new ArrayList();

// Function to mark the prime
// numbers using Sieve of
// Eratosthenes
public static void sieveOfEratosthenes(int n)
{

    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    bool []prime = new bool[n + 1];

    for(int i = 0; i < n; i++)
        prime[i] = true;

    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for(int i = 2; i <= n; i++)
    {
        if (prime[i] == true)
            primes.Add(i);
    }
}

// Function to check if the
// number can be represented
// as a power of prime
public static int[] power_of_prime(int n)
{
    for(int ii = 0; ii < primes.Count; ii++)
    {
        int i = (int)primes[ii];

        if (n % i == 0)
        {
            int c = 0;
            while (n % i == 0)
            {
                n /= i;
                c += 1;
            }

            if (n == 1)
                return new int[]{i, c};
            else
                return new int[]{-1, 1};
        }
    }
    return new int[]{-1, 1};
}

// Driver code
public static void Main(string []args)
{
    int n = 49;
    int sq = (int)(Math.Sqrt(n));
    sieveOfEratosthenes(sq + 1);

    // Function call
    int []arr = power_of_prime(n);

    if (arr[0] > 1)
        Console.Write(arr[0] + " ^ " +
                      arr[1]);
    else
        Console.Write("-1");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// a number is a prime power number

// Array to store the
// prime numbers   
let primes = [];

// Function to mark the prime
// numbers using Sieve of
// Eratosthenes
function sieveOfEratosthenes(n)
{

    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    let prime = Array.from({length: n+1}, (_, i) => 0);

    for(let i = 0; i < n; i++)
        prime[i] = true;

    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Prlet all prime numbers
    for(let i = 2; i <= n; i++)
    {
        if (prime[i] == true)
            primes.push(i);
    }
}

// Function to check if the
// number can be represented
// as a power of prime
function power_of_prime(n)
{
    for(let ii = 0; ii < primes.length; ii++)
    {
        let i = primes[ii];

        if (n % i == 0)
        {
            let c = 0;
            while (n % i == 0)
            {
                n /= i;
                c += 1;
            }

            if (n == 1)
                return [i, c];
            else
                return [-1, 1];
        }
    }
    return [-1, 1];
}

// Driver Code

        let n = 49;
    let sq = (Math.sqrt(n));
    sieveOfEratosthenes(sq + 1);

    // Function call
    let arr = power_of_prime(n);

    if (arr[0] > 1)
        document.write(arr[0] + " ^ " +
                      arr[1]);
    else
        document.write("-1");

</script>
```

**Output:** 

```
7 ^ 2
```