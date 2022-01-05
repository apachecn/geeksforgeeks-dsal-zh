# 将一个数表示为 K 个唯一素数之和的不同方式数

> 原文:[https://www . geesforgeks . org/number-of-distinct-way-to-number-to-number-as-sum-k-unique-primes/](https://www.geeksforgeeks.org/number-of-distinct-ways-to-represent-a-number-as-sum-of-k-unique-primes/)

给定一个整数 **N** 和一个整数 **K** ，任务是计算**相异**方式的数量，将数量 N 表示为 K 个相异[素数](https://www.geeksforgeeks.org/prime-numbers/)的和。
**注:** Distinct 的意思是，让 N = 7，K = 2，那么唯一的办法可以是{2，5}，因为{5，2}和{2，5}是一样的。所以只有一个办法。

**示例:**

```
Input: N = 10, K = 2
Output: 1
Explanation:
The only way is {3, 7} or {7, 3}

Input: N = 100, K = 5
Output: 55
```

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[厄拉多塞筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)可以解决问题。

*   让 **dp[i][j][sum]** 成为我们的 **3D DP** 数组，该数组存储**不同的**方式的数量，以使用 **j** 数量的素数形成**和**，其中所选素数的最后一个索引是素数向量中的 **i** 。

*   利用厄拉多塞筛可以有效地计算素数。所以，我们可以在 **O(1)** 时间得到质数的检查。

*   **复发:**

> 我们可以把这个当前素数加到我们的和中，也可以把它排除。
> dp[i][j][sum] =求解(i+1，j+1，sum+质数[i]) +求解(i+1，j，sum)

下面是上述方法的实现:

## C++

```
// C++ program to count the Number
// of distinct ways to represent
// a number as K different primes
#include <bits/stdc++.h>
using namespace std;

// Prime vector
vector<int> prime;

// Sieve array of prime
bool isprime[1000];

// DP array
int dp[200][20][1000];

void sieve()
{
    // Initialise all numbers
    // as prime
    memset(isprime, true,
        sizeof(isprime));

    // Sieve of Eratosthenes.
    for (int i = 2; i * i <= 1000;
        i++)
    {
        if (isprime[i])
        {
            for (int j = i * i;
                j <= 1000; j += i)
            {
                isprime[j] = false;
            }
        }
    }
    // Push all the primes into
    // prime vector
    for (int i = 2; i <= 1000; i++)
    {
        if (isprime[i])
        {
            prime.push_back(i);
        }
    }
}

// Function to get the number of
// distinct ways to get sum
// as K different primes
int CountWays(int i, int j, int sum,
        int n, int k)
{

    // If index went out of prime
    // array size or the sum became
    // larger than n return 0
    if (i > prime.size() || sum > n)
    {
        return 0;
    }

    // If sum becomes equal to n and
    // j becomes exactly equal to k.
    // Return 1, else if j is still
    // not equal to k, return 0
    if (sum == n) {
        if (j == k) {
            return 1;
        }
        return 0;
    }

    // If sum!=n and still j as
    // exceeded, return 0
    if (j == k)
        return 0;

    // If that state is already
    // calculated, return directly
    // the ans
    if (dp[i][j][sum])
        return dp[i][j][sum];

    int inc = 0, exc = 0;
    // Include the current prime
    inc = CountWays(i + 1, j + 1,
                sum + prime[i],
                n, k);

    // Exclude the current prime
    exc = CountWays(i + 1, j, sum,
                n, k);

    // Return by memoizing the ans
    return dp[i][j][sum] = inc + exc;
}

// Driver code
int main()
{

    // Precompute primes by sieve
    sieve();

    int N = 100, K = 5;

    cout << CountWays(0, 0, 0, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of distinct ways to represent
// a number as K different primes
import java.io.*;
import java.util.*;

class GFG{

// Prime vector
static ArrayList<Integer> prime = new ArrayList<Integer>();

// Sieve array of prime
static boolean[] isprime = new boolean[1000];

// DP array
static int[][][] dp = new int[200][20][1000];

static void sieve()
{

    // Initialise all numbers
    // as prime
    for(int i = 0; i < 1000; i++)
        isprime[i] = true;

    //  Sieve of Eratosthenes.
    for(int i = 2; i * i < 1000; i++)
    {
        if (isprime[i])
        {
            for(int j = i * i;
                    j < 1000; j += i)
            {
                isprime[j] = false;
            }
        }
    }

    // Push all the primes into
    // prime vector
    for(int i = 2; i < 1000; i++)
    {
        if (isprime[i])
        {
            prime.add(i);
        }
    }
}

// Function to get the number of
// distinct ways to get sum
// as K different primes
static int CountWays(int i, int j, int sum,
                     int n, int k)
{

    // If index went out of prime
    // array size or the sum became
    // larger than n return 0
    if (i >= prime.size() - 1 || sum > n)
    {
        return 0;
    }

    // If sum becomes equal to n and
    // j becomes exactly equal to k.
    // Return 1, else if j is still
    // not equal to k, return 0
    if (sum == n)
    {
        if (j == k)
        {
            return 1;
        }
        return 0;
    }

    // If sum!=n and still j as
    // exceeded, return 0
    if (j == k)
        return 0;

    // If that state is already
    // calculated, return directly
    // the ans
    if (dp[i][j][sum] != 0)
        return dp[i][j][sum];

    int inc = 0, exc = 0;
    // Include the current prime
    inc = CountWays(i + 1, j + 1,
                  sum + prime.get(i),
                  n, k);

    // Exclude the current prime
    exc = CountWays(i + 1, j, sum, n, k);

    // Return by memoizing the ans
    return dp[i][j][sum] = inc + exc;
}

// Driver code
public static void main(String[] args)
{

    // Precompute primes by sieve
    sieve();

    int N = 100, K = 5;

    System.out.println(CountWays(0, 0, 0, N, K));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to count the number
# of distinct ways to represent
# a number as K different primes

# Prime list
prime = []

# Sieve array of prime
isprime = [True] * 1000

# DP array
dp = [[['0' for col in range(200)]
            for col in range(20)]
            for row in range(1000)]

def sieve():

    #  Sieve of Eratosthenes.
    for i in range(2, 1000):

        if (isprime[i]):
            for j in range(i * i, 1000, i):
                isprime[j] = False

    # Push all the primes into
    # prime vector
    for i in range(2, 1000):
        if (isprime[i]):
            prime.append(i)

# Function to get the number of
# distinct ways to get sum
# as K different primes
def CountWays(i, j, sums, n, k):

    # If index went out of prime
    # array size or the sum became
    # larger than n return 0
    if (i >= len(prime) or sums > n):
        return 0

    # If sum becomes equal to n and
    # j becomes exactly equal to k.
    # Return 1, else if j is still
    # not equal to k, return 0
    if (sums == n):
        if (j == k):
            return 1

        return 0

    # If sum!=n and still j as
    # exceeded, return 0
    if j == k:
        return 0

    # If that state is already
    # calculated, return directly
    # the ans
    if dp[i][j][sums] == 0:
        return dp[i][j][sums]

    inc = 0
    exc = 0

    # Include the current prime
    inc = CountWays(i + 1, j + 1,
                 sums + prime[i],
                 n, k)

    # Exclude the current prime
    exc = CountWays(i + 1, j, sums, n, k)

    # Return by memoizing the ans
    dp[i][j][sums] = inc + exc
    return dp[i][j][sums]

# Driver code
if __name__ == "__main__":

    # Precompute primes by sieve
    sieve()

    N = 100
    K = 5

    print(CountWays(0, 0, 0, N, K))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to count the number
// of distinct ways to represent
// a number as K different primes
using System;
using System.Collections.Generic;

class GFG{

// Prime vector
static List<int> prime = new List<int>();

// Sieve array of prime
static bool[] isprime = new bool[1000];

// DP array
static int[, , ] dp = new int[200, 20, 1000];

static void sieve()
{

    // Initialise all numbers
    // as prime
    for(int i = 0; i < 1000; i++)
        isprime[i] = true;

    //  Sieve of Eratosthenes.
    for(int i = 2; i * i < 1000; i++)
    {
        if (isprime[i])
        {
            for(int j = i * i;
                    j < 1000; j += i)
            {
                isprime[j] = false;
            }
        }
    }

    // Push all the primes into
    // prime vector
    for(int i = 2; i < 1000; i++)
    {
        if (isprime[i])
        {
            prime.Add(i);
        }
    }
}

// Function to get the number of
// distinct ways to get sum
// as K different primes
static int CountWays(int i, int j, int sum,
                     int n, int k)
{

    // If index went out of prime
    // array size or the sum became
    // larger than n return 0
    if (i >= prime.Count - 1 || sum > n)
    {
        return 0;
    }

    // If sum becomes equal to n and
    // j becomes exactly equal to k.
    // Return 1, else if j is still
    // not equal to k, return 0
    if (sum == n)
    {
        if (j == k)
        {
            return 1;
        }
        return 0;
    }

    // If sum!=n and still j as
    // exceeded, return 0
    if (j == k)
        return 0;

    // If that state is already
    // calculated, return directly
    // the ans
    if (dp[i, j, sum] != 0)
        return dp[i, j, sum];

    int inc = 0, exc = 0;

    // Include the current prime
    inc = CountWays(i + 1, j + 1,
                  sum + prime[i], n, k);

    // Exclude the current prime
    exc = CountWays(i + 1, j, sum, n, k);

    // Return by memoizing the ans
    return dp[i, j, sum] = inc + exc;
}

// Driver code
static public void Main()
{

    // Precompute primes by sieve
    sieve();

    int N = 100, K = 5;

    Console.WriteLine(CountWays(0, 0, 0, N, K));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program to count the Number
// of distinct ways to represent
// a number as K different primes

// Prime vector
var prime = []; 

// Sieve array of prime
var isprime = Array(1000).fill(true);

// DP array
var dp = Array.from(Array(200), ()=>Array(20));
for(var i =0; i<200; i++)
        for(var j =0; j<20; j++)
            dp[i][j] = new Array(1000).fill(0);

function sieve()
{
    // Initialise all numbers
    // as prime

    // Sieve of Eratosthenes.
    for (var i = 2; i * i <= 1000;
        i++)
    {
        if (isprime[i])
        {
            for (var j = i * i;
                j <= 1000; j += i)
            {
                isprime[j] = false;
            }
        }
    }
    // Push all the primes into
    // prime vector
    for (var i = 2; i <= 1000; i++)
    {
        if (isprime[i])
        {
            prime.push(i);
        }
    }
}

// Function to get the number of
// distinct ways to get sum
// as K different primes
function CountWays(i,  j, sum, n, k)
{

    // If index went out of prime
    // array size or the sum became
    // larger than n return 0
    if (i > prime.length || sum > n)
    {
        return 0;
    }

    // If sum becomes equal to n and
    // j becomes exactly equal to k.
    // Return 1, else if j is still
    // not equal to k, return 0
    if (sum == n) {
        if (j == k) {
            return 1;
        }
        return 0;
    }

    // If sum!=n and still j as
    // exceeded, return 0
    if (j == k)
        return 0;

    // If that state is already
    // calculated, return directly
    // the ans
    if (dp[i][j][sum])
        return dp[i][j][sum];

    var inc = 0, exc = 0;
    // Include the current prime
    inc = CountWays(i + 1, j + 1,
                sum + prime[i],
                n, k);

    // Exclude the current prime
    exc = CountWays(i + 1, j, sum,
                n, k);

    // Return by memoizing the ans
    return dp[i][j][sum] = inc + exc;
}

// Driver code
// Precompute primes by sieve
sieve();
var N = 100, K = 5;
document.write( CountWays(0, 0, 0, N, K));

</script>
```

**Output:** 

```
55
```