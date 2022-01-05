# 求第 k 个数组中素数的和

> 原文:[https://www . geeksforgeeks . org/find-第 k 个数组中素数之和/](https://www.geeksforgeeks.org/find-the-sum-of-prime-numbers-in-the-kth-array/)

给定 **K** 个数组，其中第一个数组包含第一个素数，第二个数组包含接下来的 2 个素数，第三个数组包含接下来的 3 个素数，以此类推。任务是在 **K <sup>第</sup>T5】阵中寻找素数之和。
**举例:**** 

> **输入:** K = 3
> **输出:**31
> arr 1[]= { 2 }
> arr[]= { 3，5}
> arr[] = {7，11，13}
> 7 + 11 + 13 = 31
> **输入:** K = 2
> **输出:** 8

**方法:** [厄拉多塞的筛子](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)可以用来找到所需元素的所有素数。并且从 **1** 到**K–1**的数组中素数的计数将是**CNT = 1+2+3+……+(K–1)=(K *(K–1))/2**。现在，从筛阵中的第**(CNT+1)**素数开始，开始添加所有素数，直到恰好添加了 **K** 素数，然后打印总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// To store whether a number is prime or not
bool prime[MAX];

// Function for Sieve of Eratosthenes
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    for (int i = 0; i < MAX; i++)
        prime[i] = true;

    for (int p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed then it is a prime
        if (prime[p]) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// primes in the Kth array
int sumPrime(int k)
{

    // Update vector v to store all the
    // prime numbers upto MAX
    SieveOfEratosthenes();
    vector<int> v;
    for (int i = 2; i < MAX; i++) {
        if (prime[i])
            v.push_back(i);
    }

    // To store the sum of primes
    // in the kth array
    int sum = 0;

    // Count of primes which are in
    // the arrays from 1 to k - 1
    int skip = (k * (k - 1)) / 2;

    // k is the number of primes
    // in the kth array
    while (k > 0) {
        sum += v[skip];
        skip++;

        // A prime has been
        // added to the sum
        k--;
    }

    return sum;
}

// Driver code
int main()
{
    int k = 3;

    cout << sumPrime(k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 1000000;

// To store whether a number is prime or not
static boolean []prime = new boolean[MAX];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i < MAX; i++)
        prime[i] = true;

    for (int p = 2; p * p < MAX; p++)
    {

        // If prime[p] is not changed
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// primes in the Kth array
static int sumPrime(int k)
{

    // Update vector v to store all the
    // prime numbers upto MAX
    SieveOfEratosthenes();
    Vector<Integer> v = new Vector<>();
    for (int i = 2; i < MAX; i++)
    {
        if (prime[i])
            v.add(i);
    }

    // To store the sum of primes
    // in the kth array
    int sum = 0;

    // Count of primes which are in
    // the arrays from 1 to k - 1
    int skip = (k * (k - 1)) / 2;

    // k is the number of primes
    // in the kth array
    while (k > 0)
    {
        sum += v.get(skip);
        skip++;

        // A prime has been
        // added to the sum
        k--;
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int k = 3;

    System.out.println(sumPrime(k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

MAX = 1000000

# Create a boolean array "prime[0..n]" and
# initialize all entries it as true.
# A value in prime[i] will finally be false
# if i is Not a prime, else true.
prime = [True] * MAX

# Function for Sieve of Eratosthenes
def SieveOfEratosthenes() :

    for p in range(2, int(sqrt(MAX)) + 1) :

        # If prime[p] is not changed
        # then it is a prime
        if (prime[p]) :

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, MAX, p) :
                prime[i] = False;

# Function to return the sum of
# primes in the Kth array
def sumPrime(k) :

    # Update vector v to store all the
    # prime numbers upto MAX
    SieveOfEratosthenes();
    v = [];
    for i in range(2, MAX) :
        if (prime[i]) :
            v.append(i);

    # To store the sum of primes
    # in the kth array
    sum = 0;

    # Count of primes which are in
    # the arrays from 1 to k - 1
    skip = (k * (k - 1)) // 2;

    # k is the number of primes
    # in the kth array
    while (k > 0) :
        sum += v[skip];
        skip += 1;

        # A prime has been
        # added to the sum
        k -= 1;

    return sum;

# Driver code
if __name__ == "__main__" :

    k = 3;

    print(sumPrime(k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# mplementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 1000000;

// To store whether a number is prime or not
static bool []prime = new bool[MAX];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i < MAX; i++)
        prime[i] = true;

    for (int p = 2; p * p < MAX; p++)
    {

        // If prime[p] is not changed
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// primes in the Kth array
static int sumPrime(int k)
{

    // Update vector v to store all the
    // prime numbers upto MAX
    SieveOfEratosthenes();
    List<int> v = new List<int>();
    for (int i = 2; i < MAX; i++)
    {
        if (prime[i])
            v.Add(i);
    }

    // To store the sum of primes
    // in the kth array
    int sum = 0;

    // Count of primes which are in
    // the arrays from 1 to k - 1
    int skip = (k * (k - 1)) / 2;

    // k is the number of primes
    // in the kth array
    while (k > 0)
    {
        sum += v[skip];
        skip++;

        // A prime has been
        // added to the sum
        k--;
    }

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int k = 3;

    Console.WriteLine(sumPrime(k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach\

const MAX = 1000000;

// To store whether a number is prime or not
let prime = new Array(MAX);

// Function for Sieve of Eratosthenes
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    for (let i = 0; i < MAX; i++)
        prime[i] = true;

    for (let p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed then it is a prime
        if (prime[p]) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (let i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// primes in the Kth array
function sumPrime(k)
{

    // Update vector v to store all the
    // prime numbers upto MAX
    SieveOfEratosthenes();
    let v = [];
    for (let i = 2; i < MAX; i++) {
        if (prime[i])
            v.push(i);
    }

    // To store the sum of primes
    // in the kth array
    let sum = 0;

    // Count of primes which are in
    // the arrays from 1 to k - 1
    let skip = parseInt((k * (k - 1)) / 2);

    // k is the number of primes
    // in the kth array
    while (k > 0) {
        sum += v[skip];
        skip++;

        // A prime has been
        // added to the sum
        k--;
    }

    return sum;
}

// Driver code
    let k = 3;

    document.write(sumPrime(k));

</script>
```

**Output:** 

```
31
```