# 打印 N 加上质数形成的最近质数

> 原文:[https://www . geesforgeks . org/print-最接近的质数-通过将质数加到-n 形成/](https://www.geeksforgeeks.org/print-the-nearest-prime-number-formed-by-adding-prime-numbers-to-n/)

给定一个数 n，任务是如果这个数不是素数，则打印最近的素数，方法是从 2 开始依次添加素数，使其成为素数。
**例:**

> **输入:** N = 8
> **输出:** 13
> 8 不是素数，所以加上第一个素数得到 10
> 10 不是素数，因此加上第二个素数，即 3 得到 13，即素数。
> **输入:** N = 45
> **输出:** 47

**逼近**使用厄拉多塞的[筛，在*is prime【】*列表中用 1 标记质数索引，并将所有质数存储在一个列表*prime【】*中。继续把质数按顺序加到 N 上，直到它变成质数。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to print the
// nearest prime number by
// sequentially adding the
// prime numbers
#include<bits/stdc++.h>
using namespace std;

// Function to store prime
// numbers using prime sieve
void prime_sieve(int MAX, vector<int> &isprime,
                          vector<int> &prime)
{

    // iterate for all
    // the numbers
    int i = 2;
    while (i * i <= MAX)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (isprime[i] == 1)
        {

            // append the prime
            // to the list
            prime.push_back(i);

            // Update all multiples of p
            for (int j = i * 2; j < MAX; j += i)
            {
                isprime[j] = 0;
            }
        }

        i += 1;
    }
}

// Function to print
// the nearest prime
int printNearest(int N)
{
    int MAX = 1e6;

    // store all the
    // index with 1
    vector<int> isprime(MAX, 1);

    // 0 and 1 are not prime
    isprime[0] = isprime[1] = 0;

    // list to store
    // prime numbers
    vector<int> prime;

    // variable to
    // add primes
    int i = 0;

    // call the sieve function
    prime_sieve(MAX, isprime, prime);

    // Keep on adding prime
    // numbers till the nearest
    // prime number is achieved

    while (!isprime[N])
    {
        N += prime[i];
        i += 1;
    }

    // return the
    // nearest prime
    return N ;
}

// Driver Code
int main()
{
    int N = 8;
    printf("%d", printNearest(N));
    return 0;
}

// This code is contributed
// by Harshit Saini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// nearest prime number by
// sequentially adding the
// prime numbers
import java.util.*;

class GFG
{

// Function to store prime
// numbers using prime sieve
static void prime_sieve(int MAX, int []isprime,
                        Vector<Integer> prime)
{

    // iterate for all
    // the numbers
    int i = 2;
    while (i * i <= MAX)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (isprime[i] == 1)
        {

            // append the prime
            // to the list
            prime.add(i);

            // Update all multiples of p
            for (int j = i * 2;
                     j < MAX; j += i)
            {
                isprime[j] = 0;
            }
        }

        i += 1;
    }
}

// Function to print
// the nearest prime
static int printNearest(int N)
{
    int MAX = (int) 1e6;

    // store all the
    // index with 1 except 0,1 index
    int [] isprime = new int[MAX];
    for(int i = 2; i < MAX; i++)
        isprime[i] = 1;

    // list to store
    // prime numbers
    Vector<Integer> prime = new Vector<Integer>();

    // variable to add primes
    int i = 0;

    // call the sieve function
    prime_sieve(MAX, isprime, prime);

    // Keep on adding prime
    // numbers till the nearest
    // prime number is achieved
    while (isprime[N] == 0)
    {
        N += prime.get(i);
        i += 1;
    }

    // return the
    // nearest prime
    return N ;
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;
    System.out.printf("%d", printNearest(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print the nearest prime
# number by sequentially adding the prime numbers

# Function to store prime numbers using prime sieve
def prime_sieve(MAX, isprime, prime):

    # iterate for all the numbers
    i = 2
    while (i * i <= MAX):

        # If prime[p] is not changed,
        # then it is a prime
        if (isprime[i] == 1):

            # append the prime to the list
            prime.append(i)

            # Update all multiples of p
            for j in range(i * 2, MAX, i):
                isprime[j] = 0

        i += 1

# Function to print the nearest prime
def printNearest(N):

    MAX = 10**6

    # store all the index with 1
    isprime = [1] * MAX

    # 0 and 1 are not prime
    isprime[0] = isprime[1] = 0

    # list to store prime numbers
    prime = []

    # variable to add primes
    i = 0

    # call the sieve function
    prime_sieve(MAX, isprime, prime)

    # Keep on adding prime numbers
    # till the nearest prime number
    # is achieved
    while not isprime[N]:
        N += prime[i]
        i += 1

    # return the nearest prime
    return N

# Driver Code
N = 8
print(printNearest(N))
```

## C#

```
// C# program to print the
// nearest prime number by
// sequentially adding the
// prime numbers
using System;
using System.Collections.Generic;

class GFG
{

// Function to store prime
// numbers using prime sieve
static void prime_sieve(int MAX, int []isprime,
                        List<int> prime)
{

    // iterate for all the numbers
    int i = 2;
    while (i * i <= MAX)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (isprime[i] == 1)
        {

            // append the prime to the list
            prime.Add(i);

            // Update all multiples of p
            for (int j = i * 2;
                     j < MAX; j += i)
            {
                isprime[j] = 0;
            }
        }

        i += 1;
    }
}

// Function to print
// the nearest prime
static int printNearest(int N)
{
    int MAX = (int) 1e6;
    int i = 0;

    // store all the
    // index with 1 except 0,1 index
    int [] isprime = new int[MAX];
    for(i = 2; i < MAX; i++)
        isprime[i] = 1;

    // list to store
    // prime numbers
    List<int> prime = new List<int>();

    // variable to add primes
    i = 0;

    // call the sieve function
    prime_sieve(MAX, isprime, prime);

    // Keep on adding prime
    // numbers till the nearest
    // prime number is achieved
    while (isprime[N] == 0)
    {
        N += prime[i];
        i += 1;
    }

    // return the
    // nearest prime
    return N;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 8;
    Console.Write("{0}", printNearest(N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to print the
// nearest prime number by
// sequentially adding the
// prime numbers

// Function to store prime
// numbers using prime sieve
function prime_sieve(MAX, isprime, prime)
{

    // iterate for all
    // the numbers
    var i = 2;
    while (i * i <= MAX)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (isprime[i] == 1)
        {

            // append the prime
            // to the list
            prime.push(i);

            // Update all multiples of p
            for (var j = i * 2; j < MAX; j += i)
            {
                isprime[j] = 0;
            }
        }

        i += 1;
    }
}

// Function to print
// the nearest prime
function printNearest(N)
{
    var MAX = 1e6;

    // store all the
    // index with 1
    var isprime = Array(MAX).fill(1);

    // 0 and 1 are not prime
    isprime[0] = isprime[1] = 0;

    // list to store
    // prime numbers
    var prime = [];

    // variable to
    // add primes
    var i = 0;

    // call the sieve function
    prime_sieve(MAX, isprime, prime);

    // Keep on adding prime
    // numbers till the nearest
    // prime number is achieved

    while (!isprime[N])
    {
        N += prime[i];
        i += 1;
    }

    // return the
    // nearest prime
    return N ;
}

// Driver Code
var N = 8;
document.write( printNearest(N));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
13
```

**时间复杂度:**O(N * log(logN))
T3】辅助空间: O(N)