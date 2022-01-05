# 排列前 N 个正整数，使得素数位于素数索引处

> 原文:[https://www . geeksforgeeks . org/第一个 n 个正整数的排列-质数位于质数索引处/](https://www.geeksforgeeks.org/permutation-of-first-n-positive-integers-such-that-prime-numbers-are-at-prime-indices/)

给定一个整数 **N** ，任务是找到前 N 个正整数的排列数，使得素数位于素数索引处(对于基于 1 的索引)。
**注:**既然，途径数可能很大，返回答案模 10 <sup>9</sup> + 7。
**示例:**

> **输入:** N = 3
> **输出:** 2
> **解释:**
> 前 3 个正整数的可能排列，使得质数位于质数指数为:{1，2，3}、{1，3，2}
> **输入:** N = 5
> **输出:** 12
> **解释** :
> 前 5 个正整数的一些可能排列，

**逼近:**从 1 到 N 有 K 个素数，从索引 1 到 N 正好有 K 个素数索引，所以素数的排列数是 K！。同样，非质数的排列数是(N-K)！。所以排列总数是 K！*(N-K)！
**例如:**

```
Given test case: [1,2,3,4,5]. 
2, 3 and 5 are fixed on prime index slots, 
we can only swap them around. 
There are 3 x 2 x 1 = 3! ways
[[2,3,5], [2,5,3], [3,2,5], 
[3,5,2], [5,2,3], [5,3,2]], 
For Non-prime numbers - {1,4}  
[[1,4], [4,1]]  
So the total is  3!*2!
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// permutation of first N positive
// integers such that prime numbers
// are at the prime indices
#define mod 1000000007
#include<bits/stdc++.h>
using namespace std;

int fact(int n)
{
    int ans = 1;
    while(n > 0)
    {
        ans = ans * n;
        n--;
    }
    return ans;
}

// Function to check that
// a number is prime or not
bool isPrime(int n)
{
    if(n <= 1)
    return false;

    // Loop to check that
    // number is divisible by any
    // other number or not except 1
    for(int i = 2; i< sqrt(n) + 1; i++)
    {
       if(n % i == 0)
          return false;
       else
          return true;
    }
}

// Function to find the permutations
void findPermutations(int n)
{
    int prime = 0;

    // Loop to find the
    // number of prime numbers
    for(int j = 1; j < n + 1; j++)
    {
       if(isPrime(j))
          prime += 1;
    }

    // Permutation of N
    // positive integers
    int W = fact(prime) * fact(n - prime);

    cout << (W % mod);
}

// Driver Code
int main()
{
    int n = 7;
    findPermutations(n);
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// permutation of first N positive
// integers such that prime numbers
// are at the prime indices
import java.io.*;

class GFG{

static int mod = 1000000007;
static int fact(int n)
{
    int ans = 1;
    while(n > 0)
    {
        ans = ans * n;
        n--;
    }
    return ans;
}

// Function to check that
// a number is prime or not
static boolean isPrime(int n)
{
    if(n <= 1)
       return false;

    // Loop to check that
    // number is divisible by any
    // other number or not except 1
    for(int i = 2; i< Math.sqrt(n) + 1; i++)
    {
       if(n % i == 0)
          return false;
       else
          return true;
    }
    return true;
}

// Function to find the permutations
static void findPermutations(int n)
{
    int prime = 0;

    // Loop to find the
    // number of prime numbers
    for(int j = 1; j < n + 1; j++)
    {
       if(isPrime(j))
          prime += 1;
    }

    // Permutation of N
    // positive integers
    int W = fact(prime) * fact(n - prime);

    System.out.println(W % mod);
}

// Driver Code
public static void main (String[] args)
{
    int n = 7;

    findPermutations(n);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation to find the
# permutation of first N positive
# integers such that prime numbers
# are at the prime indices

import math

# Function to check that
# a number is prime or not
def isPrime(n):
    if n <= 1:
        return False

    # Loop to check that
    # number is divisible by any
    # other number or not except 1
    for i in range(2, int(n**0.5)+1):
        if n % i == 0:
            return False
    else:
        return True

# Constant value for modulo
CONST = int(math.pow(10, 9))+7

# Function to find the permutations
def findPermutations(n):
    prime = 0

    # Loop to find the 
    # number of prime numbers
    for j in range (1, n + 1):
        if isPrime(j):
            prime+= 1

    # Permutation of N
    # positive integers
    W = math.factorial(prime)*\
      math.factorial(n-prime)

    print (W % CONST)

# Driver Code
if __name__ == "__main__":
    n = 7

    # Function Call
    findPermutations(n)
```

## C#

```
// C# implementation to find the
// permutation of first N positive
// integers such that prime numbers
// are at the prime indices
using System;
class GFG{

static int mod = 1000000007;
static int fact(int n)
{
    int ans = 1;
    while(n > 0)
    {
        ans = ans * n;
        n--;
    }
    return ans;
}

// Function to check that
// a number is prime or not
static bool isPrime(int n)
{
    if(n <= 1)
    return false;

    // Loop to check that
    // number is divisible by any
    // other number or not except 1
    for(int i = 2; i < Math.Sqrt(n) + 1; i++)
    {
        if(n % i == 0)
            return false;
        else
            return true;
    }
    return true;
}

// Function to find the permutations
static void findPermutations(int n)
{
    int prime = 0;

    // Loop to find the
    // number of prime numbers
    for(int j = 1; j < n + 1; j++)
    {
        if(isPrime(j))
            prime += 1;
    }

    // Permutation of N
    // positive integers
    int W = fact(prime) * fact(n - prime);

    Console.Write(W % mod);
}

// Driver Code
public static void Main()
{
    int n = 7;

    findPermutations(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// permutation of first N positive
// integers such that prime numbers
// are at the prime indices
let mod = 1000000007;
function fact(n)
{
    let ans = 1;
    while(n > 0)
    {
        ans = ans * n;
        n--;
    }
    return ans;
}

// Function to check that
// a number is prime or not
function isPrime(n)
{
    if(n <= 1)
    return false;

    // Loop to check that
    // number is divisible by any
    // other number or not except 1
    for(let i = 2; i< Math.sqrt(n) + 1; i++)
    {
    if(n % i == 0)
        return false;
    else
        return true;
    }
}

// Function to find the permutations
function findPermutations(n)
{
    let prime = 0;

    // Loop to find the
    // number of prime numbers
    for(let j = 1; j < n + 1; j++)
    {
    if(isPrime(j))
        prime += 1;
    }

    // Permutation of N
    // positive integers
    let W = fact(prime) * fact(n - prime);

    document.write(W % mod);
}

// Driver Code

    let n = 7;
    findPermutations(n);

// This code is contributed by Manoj.

</script>
```

**Output:** 144 

时间复杂度:O(n <sup>3/2</sup> )

辅助空间:0(1)