# 求 1 到 N 数的素因子的指数之和

> 原文:[https://www . geesforgeks . org/find-素数因子的指数和-1 到-n/](https://www.geeksforgeeks.org/find-sum-of-exponents-of-prime-factors-of-numbers-1-to-n/)

给定一个整数 **N** ，任务是求 1 到 **N** 数的素因子的指数之和。

**示例:**

> ***输入:** N = 4*
> ***输出:** 4*
> ***解释:***
> *最多 4 个数字是 1、2、3、4 其中*
> *1 的素分解中 1 的指数是 0 (2 <sup>0</sup> )，*
> *对于 2 它是 1 (2 <sup>1</sup>*
> *每个数直到 4 的素因子的指数之和为 0 + 1 + 1 + 2 = 4。*
> 
> ***输入:** N = 10*
> ***输出:** 15*
> ***解释:***
> 每个数的素因子指数之和最多为 10 为 15。

**方法:**思路是利用[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的概念及其威力。以下是步骤:

1.  对从 **2** 到 **N** 的每个数字进行迭代，并对每个数字执行以下操作:
    1.  求每个数的质因数的[次幂 **N**](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/) 。
    2.  求上述步骤中每个幂的总和
2.  打印 **N** 的质因数的所有幂的总和，并打印总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement sieve of
// erastosthenes
void sieveOfEratosthenes(int N, int s[])
{
    // Create a boolean array and
    // initialize all entries as false
    vector<bool> prime(N + 1, false);

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for (int i = 2; i <= N; i += 2)
        s[i] = 2;

    // Iterate for odd numbers
    // less then equal to n
    for (int i = 3; i <= N; i += 2) {

        if (prime[i] == false) {

            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for (int j = i;
                 j * i <= N; j += 2) {

                if (prime[i * j] == false) {
                    prime[i * j] = true;

                    // i is the smallest
                    // prime factor for
                    // number "i*j"
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
int generatePrimeFactors(int N)
{
    // s[i] is going to store
    // smallest prime factor of i
    int s[N + 1];
    int sum = 0;

    sieveOfEratosthenes(N, s);

    // Current prime factor of N
    int curr = s[N];

    // Power of current prime factor
    int cnt = 1;

    // Calculating prime factors
    // and their powers sum
    while (N > 1) {

        N /= s[N];

        if (curr == s[N]) {

            // Increment the count and
            // continue the process
            cnt++;
            continue;
        }

        // Add count to the sum
        sum = sum + cnt;

        curr = s[N];

        // Reinitialize count
        cnt = 1;
    }

    // Return the result
    return sum;
}

// Function to find the sum of all the
// power of prime factors of N
void findSum(int N)
{

    int sum = 0;

    // Iterate for in [2, N]
    for (int i = 2; i <= N; i++) {
        sum += generatePrimeFactors(i);
    }
    cout << sum << endl;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 4;

    // Function Call
    findSum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to implement sieve of
// erastosthenes
static void sieveOfEratosthenes(int N, int s[])
{
    // Create a boolean array and
    // initialize all entries as false
    boolean []prime = new boolean[N + 1];

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for(int i = 2; i <= N; i += 2)
        s[i] = 2;

    // Iterate for odd numbers
    // less then equal to n
    for(int i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {

            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for(int j = i;
                    j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest
                    // prime factor for
                    // number "i*j"
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
static int generatePrimeFactors(int N)
{
    // s[i] is going to store
    // smallest prime factor of i
    int []s = new int[N + 1];
    int sum = 0;

    sieveOfEratosthenes(N, s);

    // Current prime factor of N
    int curr = s[N];

    // Power of current prime factor
    int cnt = 1;

    // Calculating prime factors
    // and their powers sum
    while (N > 1)
    {
        N /= s[N];

        if (curr == s[N])
        {

            // Increment the count and
            // continue the process
            cnt++;
            continue;
        }

        // Add count to the sum
        sum = sum + cnt;

        curr = s[N];

        // Reinitialize count
        cnt = 1;
    }

    // Return the result
    return sum;
}

// Function to find the sum of all the
// power of prime factors of N
static void findSum(int N)
{
    int sum = 0;

    // Iterate for in [2, N]
    for(int i = 2; i <= N; i++)
    {
        sum += generatePrimeFactors(i);
    }
    System.out.print(sum + "\n");
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 4;

    // Function Call
    findSum(N);
}
}

// This code is contributed by Ajay Kumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to implement sieve of
# erastosthenes
def sieveOfEratosthenes(N, s):

    # Create a boolean array and
    # initialize all entries as false
    prime = [False] * (N + 1)

    # Initializing smallest
    # factor equal to 2
    # for all the even numbers
    for i in range(2, N + 1, 2):
        s[i] = 2

    # Iterate for odd numbers
    # less then equal to n
    for i in range(3, N + 1, 2):
        if (prime[i] == False):

            # s(i) for a prime is
            # the number itself
            s[i] = i

            # For all multiples of
            # current prime number
            j = i
            while (j * i <= N):
                if (prime[i * j] == False):
                    prime[i * j] = True

                    # i is the smallest
                    # prime factor for
                    # number "i*j"
                    s[i * j] = i

                j += 2

# Function to generate prime
# factors and its power
def generatePrimeFactors(N):

    # s[i] is going to store
    # smallest prime factor of i
    s = [0] * (N + 1)
    sum = 0

    sieveOfEratosthenes(N, s)

    # Current prime factor of N
    curr = s[N]

    # Power of current prime factor
    cnt = 1

    # Calculating prime factors
    # and their powers sum
    while (N > 1):
        N //= s[N]

        if (curr == s[N]):

            # Increment the count and
            # continue the process
            cnt += 1
            continue

        # Add count to the sum
        sum = sum + cnt

        curr = s[N]

        # Reinitialize count
        cnt = 1

    # Return the result
    return sum

# Function to find the sum of all the
# power of prime factors of N
def findSum (N):

    sum = 0

    # Iterate for in [2, N]
    for i in range(2, N + 1):
        sum += generatePrimeFactors(i)

    print(sum)

# Driver Code
if __name__ == '__main__':

    # Given number N
    N = 4

    # Function call
    findSum(N)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to implement sieve of
// erastosthenes
static void sieveOfEratosthenes(int N, int []s)
{

    // Create a bool array and
    // initialize all entries as false
    bool []prime = new bool[N + 1];

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for(int i = 2; i <= N; i += 2)
        s[i] = 2;

    // Iterate for odd numbers
    // less then equal to n
    for(int i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {

            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for(int j = i;
                    j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest
                    // prime factor for
                    // number "i*j"
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
static int generatePrimeFactors(int N)
{

    // s[i] is going to store
    // smallest prime factor of i
    int []s = new int[N + 1];
    int sum = 0;

    sieveOfEratosthenes(N, s);

    // Current prime factor of N
    int curr = s[N];

    // Power of current prime factor
    int cnt = 1;

    // Calculating prime factors
    // and their powers sum
    while (N > 1)
    {
        N /= s[N];

        if (curr == s[N])
        {

            // Increment the count and
            // continue the process
            cnt++;
            continue;
        }

        // Add count to the sum
        sum = sum + cnt;

        curr = s[N];

        // Reinitialize count
        cnt = 1;
    }

    // Return the result
    return sum;
}

// Function to find the sum of all the
// power of prime factors of N
static void findSum(int N)
{
    int sum = 0;

    // Iterate for in [2, N]
    for(int i = 2; i <= N; i++)
    {
        sum += generatePrimeFactors(i);
    }
    Console.Write(sum + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N
    int N = 4;

    // Function call
    findSum(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to implement sieve of
// erastosthenes
function sieveOfEratosthenes(N, s)
{
    // Create a boolean array and
    // initialize all entries as false
    let prime = Array.from({length: N+1}, (_, i) => 0);

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for(let i = 2; i <= N; i += 2)
        s[i] = 2;

    // Iterate for odd numbers
    // less then equal to n
    for(let i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {

            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for(let j = i;
                    j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest
                    // prime factor for
                    // number "i*j"
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
function generatePrimeFactors(N)
{
    // s[i] is going to store
    // smallest prime factor of i
    let s = Array.from({length: N+1}, (_, i) => 0);
    let sum = 0;

    sieveOfEratosthenes(N, s);

    // Current prime factor of N
    let curr = s[N];

    // Power of current prime factor
    let cnt = 1;

    // Calculating prime factors
    // and their powers sum
    while (N > 1)
    {
        N /= s[N];

        if (curr == s[N])
        {

            // Increment the count and
            // continue the process
            cnt++;
            continue;
        }

        // Add count to the sum
        sum = sum + cnt;

        curr = s[N];

        // Reinitialize count
        cnt = 1;
    }

    // Return the result
    return sum;
}

// Function to find the sum of all the
// power of prime factors of N
function findSum(N)
{
    let sum = 0;

    // Iterate for in [2, N]
    for(let i = 2; i <= N; i++)
    {
        sum += generatePrimeFactors(i);
    }
    document.write(sum + "\n");
}

// Driver Code

    // Given Number N
    let N = 4;

    // Function Call
    findSum(N);

</script>
```

**Output:** 

```
4
```

**时间复杂度:*****O(N * log<sub>2</sub>N)*** ****辅助空间:** *O(N)***