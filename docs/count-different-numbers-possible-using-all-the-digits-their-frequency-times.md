# 使用所有数字的频率次数来计算可能的不同数字

> 原文:[https://www . geesforgeks . org/count-异数-可能-使用所有数字-它们的频率-时间/](https://www.geeksforgeeks.org/count-different-numbers-possible-using-all-the-digits-their-frequency-times/)

给定一个包含数字频率(0-9)的数组 **arr[]** ，任务是使用每个数字的频率次数找到可能的数字计数。也就是说，生成的最终数字应该包含其频率时间的所有数字。因为，计数可能非常大，以 10^9+7.为模返回答案

**先决条件:** [一个数的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)、[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)
**示例:**

```
Input : arr[] = {0, 1, 1, 0, 0, 0, 0, 0, 0, 0}
Output : 2
Frequency of 1 and 2 is 1 and all the rest is 0\. 
Therefore, 2 possible numbers are 12 and 21.

Input : arr[] = {0, 5, 2, 0, 0, 0, 4, 0, 1, 1}
Output : 1081080

```

**逼近**:使用排列组合可以轻松解决问题。数组**arr【】**的*带*索引给出了带数字的*的频率。这个问题可以认为是求 *X* 对象的全排列，其中 *X0* 对象是一种类型， *X1* 对象是另一种类型，依此类推。那么可能的数字计数由下式给出:*

> 总计数= X！/ (X0！* X1！*…..* X9！)

其中 *X* =所有数字的频率之和， *Xi* =第一个数字的频率。

以下是上述方法的实施

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define MAXN 100000
#define MOD 1000000007

// Initialize an array to store factorial values
ll fact[MAXN];

// Function to calculate and store X! values
void factorial()
{
    fact[0] = 1;
    for (int i = 1; i < MAXN; i++)
        fact[i] = (fact[i - 1] * i) % MOD;
}

// Iterative Function to calculate (x^y)%p in O(log y)
ll power(ll x, ll y, ll p)
{
    ll res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function that return modular
// inverse of x under modulo p
ll modInverse(ll x, ll p)
{
    return power(x, p - 2, p);
}

// Function that returns the count of
// different number possible by using
// all the digits its frequency times
ll countDifferentNumbers(ll arr[], ll P)
{
    // Preprocess factorial values
    factorial();

    // Initialize the result and sum
    // of aint the frequencies
    ll res = 0, X = 0;

    // Calculate the sum of frequencies
    for (int i = 0; i < 10; i++)
        X += arr[i];

    // Putting res equal to x!
    res = fact[X];

    // Multiplying res with modular
    // inverse of X0!, X1!, .., X9!
    for (int i = 0; i < 10; i++) {
        if (arr[i] > 1)
            res = (res * modInverse(fact[arr[i]], P)) % P;
    }

    return res;
}

// Driver Code
int main()
{
    ll arr[] = { 1, 0, 2, 0, 0, 7, 4, 0, 0, 3 };
    cout << countDifferentNumbers(arr, MOD);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

static int MAXN = 100000;
static int MOD = 1000000007;

// Initialize an array to store factorial values
static long fact[] = new long[MAXN];

// Function to calculate and store X! values
static void factorial()
{
    fact[0] = 1;
    for (int i = 1; i < MAXN; i++)
        fact[i] = (fact[i - 1] * i) % MOD;
}

// Iterative Function to calculate (x^y)%p in O(log y)
static long power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y % 2== 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function that return modular
// inverse of x under modulo p
static long modInverse(long x, long p)
{
    return power(x, p - 2, p);
}

// Function that returns the count of
// different number possible by using
// along the digits its frequency times
static long countDifferentNumbers(long arr[], long P)
{
    // Preprocess factorial values
    factorial();

    // Initialize the result and sum
    // of aint the frequencies
    long res = 0, X = 0;

    // Calculate the sum of frequencies
    for (int i = 0; i < 10; i++)
        X += arr[i];

    // Putting res equal to x!
    res = fact[(int)X];

    // Multiplying res with modular
    // inverse of X0!, X1!, .., X9!
    for (int i = 0; i < 10; i++)
    {
        if (arr[i] > 1)
            res = (res * modInverse(fact[(int)arr[i]], P)) % P;
    }

    return res;
}

// Driver Code
public static void main(String[] args) 
{
    long arr[] = { 1, 0, 2, 0, 0, 7, 4, 0, 0, 3 };
    System.out.println(countDifferentNumbers(arr, MOD));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the above approach 
MAXN = 100000
MOD = 1000000007

# Initialize an array to store
# factorial values 
fact = [0] * MAXN; 

# Function to calculate and store X! values 
def factorial() :
    fact[0] = 1
    for i in range(1, MAXN) :
        fact[i] = (fact[i - 1] * i) % MOD

# Iterative Function to calculate
# (x^y)%p in O(log y) 
def power(x, y, p) : 

    res = 1 # Initialize result 

    x = x % p # Update x if it is more than  
              # or equal to p 

    while (y > 0) :

        # If y is odd, multiply x with result 
        if (y & 1) :
            res = (res * x) % p 

        # y must be even now 
        y = y >> 1; # y = y/2 
        x = (x * x) % p

    return res

# Function that return modular 
# inverse of x under modulo p 
def modInverse(x, p) : 
    return power(x, p - 2, p) 

# Function that returns the count of 
# different number possible by using 
# all the digits its frequency times 
def countDifferentNumbers(arr, P) : 

    # Preprocess factorial values 
    factorial(); 

    # Initialize the result and sum 
    # of aint the frequencies 
    res = 0; X = 0; 

    # Calculate the sum of frequencies 
    for i in range(10) :
        X += arr[i] 

    # Putting res equal to x! 
    res = fact[X] 

    # Multiplying res with modular 
    # inverse of X0!, X1!, .., X9! 
    for i in range(10) :
        if (arr[i] > 1) :
            res = (res * modInverse(fact[arr[i]], P)) % P; 

    return res; 

# Driver Code 
if __name__ == "__main__" : 

    arr = [1, 0, 2, 0, 0, 7, 4, 0, 0, 3 ]
    print(countDifferentNumbers(arr, MOD)) 

# This code is contributed by Ryuga
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    static int MAXN = 100000;
    static int MOD = 1000000007;

    // Initialize an array to store factorial values
    static long []fact = new long[MAXN];

    // Function to calculate and store X! values
    static void factorial()
    {
        fact[0] = 1;
        for (int i = 1; i < MAXN; i++)
            fact[i] = (fact[i - 1] * i) % MOD;
    }

    // Iterative Function to calculate (x^y)%p in O(log y)
    static long power(long x, long y, long p)
    {
        long res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2== 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function that return modular
    // inverse of x under modulo p
    static long modInverse(long x, long p)
    {
        return power(x, p - 2, p);
    }

    // Function that returns the count of
    // different number possible by using
    // along the digits its frequency times
    static long countDifferentNumbers(long []arr, long P)
    {
        // Preprocess factorial values
        factorial();

        // Initialize the result and sum
        // of aint the frequencies
        long res = 0, X = 0;

        // Calculate the sum of frequencies
        for (int i = 0; i < 10; i++)
            X += arr[i];

        // Putting res equal to x!
        res = fact[(int)X];

        // Multiplying res with modular
        // inverse of X0!, X1!, .., X9!
        for (int i = 0; i < 10; i++)
        {
            if (arr[i] > 1)
                res = (res * modInverse(fact[(int)arr[i]], P)) % P;
        }

        return res;
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        long []arr = { 1, 0, 2, 0, 0, 7, 4, 0, 0, 3 };
        Console.WriteLine(countDifferentNumbers(arr, MOD));
    }
}

// This code has been contributed by 29AjayKumar
```

**Output:**

```
245044800

```