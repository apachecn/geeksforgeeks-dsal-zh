# 排列前 N 个正整数，使得素数位于素数索引处|集合 2

> 原文:[https://www . geeksforgeeks . org/first-n-正整数排列-这样-质数位于质数索引-set-2/](https://www.geeksforgeeks.org/permutation-of-first-n-positive-integers-such-that-prime-numbers-are-at-prime-indices-set-2/)

给定一个整数 **N** ，任务是找到前 N 个正整数的排列数，使得素数位于素数索引处(对于基于 1 的索引)。
**注:**既然，途径数可能很大，返回答案模 10 <sup>9</sup> + 7。
**示例:**

> **输入:** N = 3
> **输出:** 2
> **解释:**
> 前 3 个正整数的可能排列，使得质数位于质数指数为:{1，2，3}、{1，3，2}
> **输入:** N = 5
> **输出:** 12

**进场:使用** [**厄拉多塞**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
筛子

*   首先，[用厄拉多塞筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)统计 1 到 N 之间的所有素数。
*   接下来，迭代每个位置，得到质数，称之为 k。
*   所以，对于 k 素数，我们的选择有限，我们需要把它们排列在 k 个素数点上。
*   对于 n-k 个非质数，我们的选择也是有限的。我们需要把它们安排在 n-k 个非素数点上。
*   这两个事件是独立的，所以所有的方式都是它们的产物。
*   k 个框中排列 k 个对象的方式数为 **k！**

以下是上述方法的实现:

## C++

```
// C++ program to count
// permutations from 1 to N
// such that prime numbers
// occur at prime indices

#include <bits/stdc++.h>
using namespace std;

static const int MOD = 1e9 + 7;

int numPrimeArrangements(int n)
{
    vector<bool> prime(n + 1, true);
    prime[0] = false;
    prime[1] = false;

    // Computing count of prime
    // numbers using sieve
    for (int i = 2; i <= sqrt(n); i++) {
        if (prime[i])
            for (int factor = 2;
                 factor * i <= n;
                 factor++)
                prime[factor * i] = false;
    }

    int primeIndices = 0;
    for (int i = 1; i <= n; i++)
        if (prime[i])
            primeIndices++;

    int mod = 1e9 + 7, res = 1;

    // Computing permutations for primes
    for (int i = 1; i <= primeIndices; i++)
        res = (1LL * res * i) % mod;

    // Computing permutations for non-primes
    for (int i = 1; i <= (n - primeIndices); i++)
        res = (1LL * res * i) % mod;

    return res;
}

// Driver program
int main()
{
    int N = 5;
    cout << numPrimeArrangements(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// permutations from 1 to N
// such that prime numbers
// occur at prime indices

import java.util.*;

class GFG{

static int MOD = (int) (1e9 + 7);

static int numPrimeArrangements(int n)
{
    boolean []prime = new boolean[n + 1];
    Arrays.fill(prime, true);
    prime[0] = false;
    prime[1] = false;

    // Computing count of prime
    // numbers using sieve
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (prime[i])
            for (int factor = 2;
                 factor * i <= n;
                 factor++)
                prime[factor * i] = false;
    }

    int primeIndices = 0;
    for (int i = 1; i <= n; i++)
        if (prime[i])
            primeIndices++;

    int mod = (int) (1e9 + 7), res = 1;

    // Computing permutations for primes
    for (int i = 1; i <= primeIndices; i++)
        res = (int) ((1L * res * i) % mod);

    // Computing permutations for non-primes
    for (int i = 1; i <= (n - primeIndices); i++)
        res = (int) ((1L * res * i) % mod);

    return res;
}

// Driver program
public static void main(String[] args)
{
    int N = 5;
    System.out.print(numPrimeArrangements(N));
}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to count
# permutations from 1 to N
# such that prime numbers
# occur at prime indices
import math;

def numPrimeArrangements(n):

    prime = [True for i in range(n + 1)]

    prime[0] = False
    prime[1] = False

    # Computing count of prime
    # numbers using sieve
    for i in range(2,int(math.sqrt(n)) + 1):
        if prime[i]:
            factor = 2

            while factor * i <= n:
                prime[factor * i] = False
                factor += 1

    primeIndices = 0       
    for i in range(1, n + 1):
        if prime[i]:
            primeIndices += 1

    mod = 1000000007
    res = 1

    # Computing permutations for primes
    for i in range(1, primeIndices + 1):
        res = (res * i) % mod

    # Computing permutations for non-primes
    for i in range(1, n - primeIndices + 1):
        res = (res * i) % mod

    return res

# Driver code       
if __name__=='__main__':

    N = 5

    print(numPrimeArrangements(N))

# This code is contributed by rutvik_56  
```

## C#

```
// C# program to count permutations
// from 1 to N such that prime numbers
// occur at prime indices
using System;

class GFG{

//static int MOD = (int) (1e9 + 7);

static int numPrimeArrangements(int n)
{
    bool []prime = new bool[n + 1];

    for(int i = 0; i < prime.Length; i++)
       prime[i] = true;
    prime[0] = false;
    prime[1] = false;

    // Computing count of prime
    // numbers using sieve
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {
       if (prime[i])
       {
           for(int factor = 2;
                   factor * i <= n;
                   factor++)
              prime[factor * i] = false;
       }
    }

    int primeIndices = 0;
    for(int i = 1; i <= n; i++)
       if (prime[i])
           primeIndices++;

    int mod = (int) (1e9 + 7), res = 1;

    // Computing permutations for primes
    for(int i = 1; i <= primeIndices; i++)
       res = (int) ((1L * res * i) % mod);

    // Computing permutations for non-primes
    for(int i = 1; i <= (n - primeIndices); i++)
       res = (int) ((1L * res * i) % mod);

    return res;
}

// Driver code
public static void Main(String[] args)
{
    int N = 5;

    Console.Write(numPrimeArrangements(N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// javascript program to count
// permutations from 1 to N
// such that prime numbers
// occur at prime indices
var MOD = parseInt(1e9 + 7);

function numPrimeArrangements(n)
{
    var prime = Array.from({length: n+1}, (_, i) => true);
    prime[0] = false;
    prime[1] = false;

    // Computing count of prime
    // numbers using sieve
    for (var i = 2; i <= Math.sqrt(n); i++) {
        if (prime[i])
            for (factor = 2;
                 factor * i <= n;
                 factor++)
                prime[factor * i] = false;
    }

    var primeIndices = 0;
    for (var i = 1; i <= n; i++)
        if (prime[i])
            primeIndices++;

    var mod = parseInt( (1e9 + 7)), res = 1;

    // Computing permutations for primes
    for (var i = 1; i <= primeIndices; i++)
        res = ((1 * res * i) % mod);

    // Computing permutations for non-primes
    for (var i = 1; i <= (n - primeIndices); i++)
        res = ((1 * res * i) % mod);

    return res;
}

// Driver program
var N = 5;
document.write(numPrimeArrangements(N));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N * log(log(N)))*

***辅助空间:**O(N)*T4】