# 不能被前 N 个素数整除的最小合成数

> 原文:[https://www . geesforgeks . org/minist-composite-number-不能被第一个 n 个质数除尽/](https://www.geeksforgeeks.org/smallest-composite-number-not-divisible-by-first-n-prime-numbers/)

给定一个整数 **N** ，任务是找到不能被第一个**N**T6】素数整除的最小[合成数](https://www.geeksforgeeks.org/composite-number/)。

**示例:**

> **输入:** N = 3
> **输出:** 49
> **解释:**
> 前 3 个质数为{2，3，5}。不能被 2、3 或 5 整除的最小复合整数是 49。
> 
> **输入:** N = 2
> **输出:** 25
> **说明:**
> 前 2 个质数为{2，3}。不能被 2 或 3 整除的最小复合整数是 25。

**天真方法:**解决问题最简单的方法是从 2 开始检查每个数字的以下条件:

*   **条件 1:** 检查当前数字是否为质数。如果是质数，那么对下一个数重复这个过程。否则，如果数字是复合的，则检查以下条件:
*   **条件 2:** 求第一个 **N** 素数，检查这个合数是否不能被每个素数整除。
*   如果当前号码满足上述两个条件，则打印该号码作为所需答案。

**时间复杂度:** O(M <sup>3</sup> N)，其中 M 表示满足条件的合成数。
**辅助空间:** O(N)，存储 N 个质数。

**有效方法:**给定的问题可以通过以下观察来解决:

> 第一个不能被前 N 个质数中的任何一个整除的复合数= **((N + 1) <sup>第</sup>质数)<sup>2</sup>T5】**

插图:

> 对于 N = 2
> = >前 2 个质数为{2，3}
> = > (N + 1) <sup>第</sup>个质数为 5
> = >可以观察到，24 {4，6，8，9，10，12，14，15，16，18，20，21，22，24}以内的所有非质数都可以被 2 整除，或者被 3 整除，或者被两者整除。
> = >下一个复合数{25}只能被 5 整除。
> = >因此，可以得出第一个不能被前 N 个素数中任何一个整除的合成数是第(N + 1) <sup>个</sup>素数的平方。

想法是用厄拉多塞的[筛找到 **(N+1) <sup>第</sup>** 素数，打印 **(N+1) <sup>第</sup>T10】素数**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的[方块作为答案。](https://www.geeksforgeeks.org/calculate-square-of-a-number-without-using-and-pow/)

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Initializing the max value
#define MAX_SIZE 1000005

// Function to generate N prime numbers
// using Sieve of Eratosthenes
void SieveOfEratosthenes(
    vector<int>& StorePrimes)
{
    // Stores the primes
    bool IsPrime[MAX_SIZE];

    // Setting all numbers to be prime initially
    memset(IsPrime, true, sizeof(IsPrime));

    for (int p = 2; p * p < MAX_SIZE; p++) {

        // If a prime number is encountered
        if (IsPrime[p] == true) {

            // Set all its multiples as composites
            for (int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all the prime numbers
    for (int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            StorePrimes.push_back(p);
}

// Function to find the square of
// the (N + 1)-th prime number
int Smallest_non_Prime(
    vector<int> StorePrimes,
    int N)
{
    int x = StorePrimes[N];
    return x * x;
}

// Driver Code
int main()
{
    int N = 3;

    // Stores all prime numbers
    vector<int> StorePrimes;

    SieveOfEratosthenes(StorePrimes);

    cout << Smallest_non_Prime(StorePrimes, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;
import java.util.Vector;

class GFG{

// Initializing the max value
static final int MAX_SIZE = 1000005;

// Function to generate N prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(
    Vector<Integer> StorePrimes)
{

    // Stores the primes
    boolean []IsPrime = new boolean[MAX_SIZE];

    // Setting all numbers to be prime initially
    Arrays.fill(IsPrime, true);

    for(int p = 2; p * p < MAX_SIZE; p++)
    {

        // If a prime number is encountered
        if (IsPrime[p] == true)
        {

            // Set all its multiples as composites
            for(int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all the prime numbers
    for(int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            StorePrimes.add(p);
}

// Function to find the square of
// the (N + 1)-th prime number
static int Smallest_non_Prime(
    Vector<Integer> StorePrimes,
    int N)
{
    int x = StorePrimes.get(N);
    return x * x;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;

    // Stores all prime numbers
    Vector<Integer> StorePrimes = new Vector<Integer>();

    SieveOfEratosthenes(StorePrimes);

    System.out.print(Smallest_non_Prime(StorePrimes, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Initializing the max value
MAX_SIZE = 1000005

# Function to generate N prime numbers
# using Sieve of Eratosthenes
def SieveOfEratosthenes(StorePrimes):

    # Stores the primes
    IsPrime = [True for i in range(MAX_SIZE)]

    p = 2
    while (p * p < MAX_SIZE):

        # If a prime number is encountered
        if (IsPrime[p] == True):

            # Set all its multiples as composites
            for i in range(p * p, MAX_SIZE, p):
                IsPrime[i] = False

        p += 1

    # Store all the prime numbers
    for p in range(2, MAX_SIZE):
        if (IsPrime[p]):
            StorePrimes.append(p)

# Function to find the square of
# the (N + 1)-th prime number
def Smallest_non_Prime(StorePrimes, N):

    x = StorePrimes[N]

    return x * x

# Driver Code
if __name__ == '__main__':

    N = 3

    # Stores all prime numbers
    StorePrimes = []

    SieveOfEratosthenes(StorePrimes)

    print(Smallest_non_Prime(StorePrimes, N))

# This code is contributed by bgangwar59
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Initializing the max value
static readonly int MAX_SIZE = 1000005;

// Function to generate N prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(
    List<int> StorePrimes)
{

    // Stores the primes
    bool []IsPrime = new bool[MAX_SIZE];

    // Setting all numbers to be prime initially
    for(int i = 0; i < MAX_SIZE; i++)
        IsPrime[i] = true;

    for(int p = 2; p * p < MAX_SIZE; p++)
    {

        // If a prime number is encountered
        if (IsPrime[p] == true)
        {

            // Set all its multiples as composites
            for(int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all the prime numbers
    for(int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            StorePrimes.Add(p);
}

// Function to find the square of
// the (N + 1)-th prime number
static int Smallest_non_Prime(
    List<int> StorePrimes,
    int N)
{
    int x = StorePrimes[N];
    return x * x;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;

    // Stores all prime numbers
    List<int> StorePrimes = new List<int>();

    SieveOfEratosthenes(StorePrimes);

    Console.Write(Smallest_non_Prime(StorePrimes, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Initializing the max value
var MAX_SIZE = 1000005;

// Function to generate N prime numbers
// using Sieve of Eratosthenes
function SieveOfEratosthenes(StorePrimes)
{
    // Stores the primes
    var IsPrime = Array(MAX_SIZE).fill(true);

    var p,i;
    for(p = 2; p * p < MAX_SIZE; p++) {

        // If a prime number is encountered
        if (IsPrime[p] == true) {

            // Set all its multiples as composites
            for(i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all the prime numbers
    for (p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            StorePrimes.push(p);
}

// Function to find the square of
// the (N + 1)-th prime number
function Smallest_non_Prime(StorePrimes, N)
{
    var x = StorePrimes[N];
    return x * x;
}

// Driver Code
    N = 3;

    // Stores all prime numbers
    var StorePrimes = [];

    SieveOfEratosthenes(StorePrimes);

    document.write(Smallest_non_Prime(StorePrimes, N));

</script>
```

**Output:** 

```
49
```

***时间复杂度:** O(MAX_SIZE log (log MAX_SIZE))，其中 MAX_SIZE 表示生成 **N** 素数的上限。*
***辅助空间:** O(MAX_SIZE)*