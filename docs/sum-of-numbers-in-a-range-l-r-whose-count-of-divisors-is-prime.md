# 除数为素数的[L，R]范围内的数的和

> 原文:[https://www . geesforgeks . org/范围内数的总和-l-r-谁的除数是质数/](https://www.geeksforgeeks.org/sum-of-numbers-in-a-range-l-r-whose-count-of-divisors-is-prime/)

给定 **Q** 查询，其中每个查询由整数范围**【L，R】**组成，任务是从给定范围中找到除数为素数的整数之和。
**例:**

> **输入:** Q[][] = {{2，4}}
> **输出:**
> 9
> 范围内所有数字只有 2 个除数
> 是质数。
> (2 + 3 + 4) = 9。
> **输入:** Q[][] = {{15，17}，{2，12}}
> **输出:**
> 33
> 41

**方法:**使用厄拉多塞的[筛找出每个元素的所有素数和除数，直到极限 N。现在创建一个前缀和数组**和[]** ，其中**和【I】**将存储范围**【0，I】**中的元素的和，这些元素的除数是使用前面创建的筛数组的质数。现在每个查询都可以在 O(1)中回答为**sum[r]–sum[l–1]**。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 100000;

// prime[i] stores 1 if i is prime
int prime[N];

// divi[i] stores the count of
// divisors of i
int divi[N];

// sum[i] will store the sum of all
// the integers from 0 to i whose
// count of divisors is prime
int sum[N];

// Function for Sieve of Eratosthenes
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be 0 if i is Not a prime, else true.
    for (int i = 0; i < N; i++)
        prime[i] = 1;

    // 0 and 1 is not prime
    prime[0] = prime[1] = 0;

    for (int p = 2; p * p < N; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == 1) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                prime[i] = 0;
        }
    }
}

// Function to count the divisors
void DivisorCount()
{

    // For each number i we will go to each of
    // the multiple of i and update the count
    // of divisor of its multiple j as i is one
    // of the factor of j
    for (int i = 1; i < N; i++) {
        for (int j = i; j < N; j += i) {
            divi[j]++;
        }
    }
}

// Function for pre-computation
void pre()
{
    for (int i = 1; i < N; i++) {

        // If count of divisors of i is prime
        if (prime[divi[i]] == 1) {
            sum[i] = i;
        }
    }

    // taking prefix sum
    for (int i = 1; i < N; i++)
        sum[i] += sum[i - 1];
}

// Driver code
int main()
{

    int l = 5, r = 8;

    // Find all the prime numbers till N
    SieveOfEratosthenes();

    // Update the count of divisors
    // of all the numbers till N
    DivisorCount();

    // Precomputation for the prefix sum array
    pre();

    // Perform query
    cout << sum[r] - sum[l - 1];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
import java.util.*;
class GFG
{

static int N = 100000;

// prime[i] stores 1 if i is prime
static int prime[] = new int[N];

// divi[i] stores the count of
// divisors of i
static int divi[] = new int[N];

// sum[i] will store the sum of all
// the integers from 0 to i whose
// count of divisors is prime
static int sum[] = new int[N];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be 0
    // if i is Not a prime, else true.
    for (int i = 0; i < N; i++)
        prime[i] = 1;

    // 0 and 1 is not prime
    prime[0] = prime[1] = 0;

    for (int p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == 1)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                prime[i] = 0;
        }
    }
}

// Function to count the divisors
static void DivisorCount()
{

    // For each number i we will go to each of
    // the multiple of i and update the count
    // of divisor of its multiple j as i is one
    // of the factor of j
    for (int i = 1; i < N; i++)
    {
        for (int j = i; j < N; j += i)
        {
            divi[j]++;
        }
    }
}

// Function for pre-computation
static void pre()
{
    for (int i = 1; i < N; i++)
    {

        // If count of divisors of i is prime
        if (prime[divi[i]] == 1)
        {
            sum[i] = i;
        }
    }

    // taking prefix sum
    for (int i = 1; i < N; i++)
        sum[i] += sum[i - 1];
}

// Driver code
public static void main(String args[])
{
    int l = 5, r = 8;

    // Find all the prime numbers till N
    SieveOfEratosthenes();

    // Update the count of divisors
    // of all the numbers till N
    DivisorCount();

    // Precomputation for the prefix sum array
    pre();

    // Perform query
    System.out.println( sum[r] - sum[l - 1]);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

N = 100000;

# Create a boolean array "prime[0..n]" and
# initialize all entries it as true.
# A value in prime[i] will finally be 0 if
# i is Not a prime, else true.
# prime[i] stores 1 if i is prime
prime = [1] * N;

# divi[i] stores the count of
# divisors of i
divi = [0] * N;

# sum[i] will store the sum of all
# the integers from 0 to i whose
# count of divisors is prime
sum = [0] * N;

# Function for Sieve of Eratosthenes
def SieveOfEratosthenes() :

    for i in range(N) :
        prime[i] = 1;

    # 0 and 1 is not prime
    prime[0] = prime[1] = 0;

    for p in range(2, int(sqrt(N)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == 1) :

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, N, p) :
                prime[i] = 0;

# Function to count the divisors
def DivisorCount() :

    # For each number i we will go to each of
    # the multiple of i and update the count
    # of divisor of its multiple j as i is one
    # of the factor of j
    for i in range(1, N) :
        for j in range(i, N , i) :
            divi[j] += 1;

# Function for pre-computation
def pre() :

    for i in range(1, N) :

        # If count of divisors of i is prime
        if (prime[divi[i]] == 1) :
            sum[i] = i;

    # taking prefix sum
    for i in range(1, N) :
        sum[i] += sum[i - 1];

# Driver code
if __name__ == "__main__" :

    l = 5; r = 8;

    # Find all the prime numbers till N
    SieveOfEratosthenes();

    # Update the count of divisors
    # of all the numbers till N
    DivisorCount();

    # Precomputation for the prefix sum array
    pre();

    # Perform query
    print(sum[r] - sum[l - 1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int N = 100000;

// prime[i] stores 1 if i is prime
static int []prime = new int[N];

// divi[i] stores the count of
// divisors of i
static int []divi = new int[N];

// sum[i] will store the sum of all
// the integers from 0 to i whose
// count of divisors is prime
static int []sum = new int[N];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be 0
    // if i is Not a prime, else true.
    for (int i = 0; i < N; i++)
        prime[i] = 1;

    // 0 and 1 is not prime
    prime[0] = prime[1] = 0;

    for (int p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == 1)
        {

            // Update all multiples of p greater than
            // or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                prime[i] = 0;
        }
    }
}

// Function to count the divisors
static void DivisorCount()
{

    // For each number i we will go to each of
    // the multiple of i and update the count
    // of divisor of its multiple j as i is one
    // of the factor of j
    for (int i = 1; i < N; i++)
    {
        for (int j = i; j < N; j += i)
        {
            divi[j]++;
        }
    }
}

// Function for pre-computation
static void pre()
{
    for (int i = 1; i < N; i++)
    {

        // If count of divisors of i is prime
        if (prime[divi[i]] == 1)
        {
            sum[i] = i;
        }
    }

    // taking prefix sum
    for (int i = 1; i < N; i++)
        sum[i] += sum[i - 1];
}

// Driver code
public static void Main(String []args)
{
    int l = 5, r = 8;

    // Find all the prime numbers till N
    SieveOfEratosthenes();

    // Update the count of divisors
    // of all the numbers till N
    DivisorCount();

    // Precomputation for the prefix sum array
    pre();

    // Perform query
    Console.WriteLine( sum[r] - sum[l - 1]);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of above approach  
var N = 100000;

// prime[i] stores 1 if i is prime
var prime = Array.from({length: N}, (_, i) => 0);

// divi[i] stores the count of
// divisors of i
var divi = Array.from({length: N}, (_, i) => 0);

// sum[i] will store the sum of all
// the integers from 0 to i whose
// count of divisors is prime
var sum = Array.from({length: N}, (_, i) => 0);

// Function for Sieve of Eratosthenes
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be 0
    // if i is Not a prime, else true.
    for (i = 0; i < N; i++)
        prime[i] = 1;

    // 0 and 1 is not prime
    prime[0] = prime[1] = 0;

    for (p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == 1)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (i = p * p; i < N; i += p)
                prime[i] = 0;
        }
    }
}

// Function to count the divisors
function DivisorCount()
{

    // For each number i we will go to each of
    // the multiple of i and update the count
    // of divisor of its multiple j as i is one
    // of the factor of j
    for (i = 1; i < N; i++)
    {
        for (j = i; j < N; j += i)
        {
            divi[j]++;
        }
    }
}

// Function for pre-computation
function pre()
{
    for (i = 1; i < N; i++)
    {

        // If count of divisors of i is prime
        if (prime[divi[i]] == 1)
        {
            sum[i] = i;
        }
    }

    // taking prefix sum
    for (i = 1; i < N; i++)
        sum[i] += sum[i - 1];
}

// Driver code

var l = 5, r = 8;

// Find all the prime numbers till N
SieveOfEratosthenes();

// Update the count of divisors
// of all the numbers till N
DivisorCount();

// Precomputation for the prefix sum array
pre();

// Perform query
document.write( sum[r] - sum[l - 1]);

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
12
```