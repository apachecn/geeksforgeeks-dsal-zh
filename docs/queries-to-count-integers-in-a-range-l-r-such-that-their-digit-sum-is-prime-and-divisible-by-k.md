# 查询对范围[L，R]内的整数进行计数，使它们的数字和为质数并可被 K 整除

> 原文:[https://www . geesforgeks . org/query-to-count-in-a-range-l-r-so-它们的数字和是质数和可被 k 整除/](https://www.geeksforgeeks.org/queries-to-count-integers-in-a-range-l-r-such-that-their-digit-sum-is-prime-and-divisible-by-k/)

给定 **Q** 个查询和一个整数 **K** ，其中每个查询由一个范围**【L，R】**组成，任务是找出给定范围内数字和为素数且可被 **K** 整除的整数个数。
**例:**

```
Input: Q = { {1, 11},
      {5, 15},
      {2, 24} } 
K = 2
Output: 
2
1
3
Explanation:
Query 1: 2 and 11 are the only 
numbers in the given range whose 
digit sum is prime and divisible by K.
Query 2: 11 is the only number.
Query 3: 2, 11 and 20.

Input: Q = { {2, 17},
             {3, 24} }
K = 3
Output:
2
3
```

**进场:**

*   首先，使用厄拉多塞的[筛，预先计算所有素数，直到所有给定范围中 R 的最大可能值为 **maxVal** 。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   然后标记从 **1** 到 **maxVal** 所有可被 **K** 整除且为质数的整数。
*   取标记数组的前缀和。
*   通过**前缀【右】–前缀【左–1】**回答给定的查询。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int maxSize = 1e5 + 1;
bool isPrime[maxSize];
int prefix[maxSize];

// Function to return the
// digit sum of num
int digitSum(int num)
{
    int s = 0;
    while (num != 0) {
        s = s + num % 10;
        num = num / 10;
    }
    return s;
}

// Sieve Function to generate
// all primes opto maxSize
void sieveOfEratosthenes()
{
    for (int i = 2; i < maxSize; i++) {
        isPrime[i] = true;
    }

    for (int i = 2; i * i <= maxSize; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j < maxSize; j += i) {
                isPrime[j] = false;
            }
        }
    }
}

// Pre-Computation till maxSize
// and for a given K
void precompute(int k)
{
    sieveOfEratosthenes();
    for (int i = 1; i < maxSize; i++) {
        // Getting Digit Sum
        int sum = digitSum(i);
        // Check if the digit sum
        // is prime and divisible by k
        if (isPrime[sum] == true && sum % k == 0) {
            prefix[i]++;
        }
    }

    // Taking Prefix Sum
    for (int i = 1; i < maxSize; i++) {
        prefix[i] = prefix[i] + prefix[i - 1];
    }
}

// Function to perform the queries
void performQueries(int k, int q,
                    vector<vector<int> >& query)
{
    // Precompute the results
    precompute(k);

    vector<int> ans;
    for (int i = 0; i < q; i++) {
        int l = query[i][0], r = query[i][1];

        // Getting count of range in range [L, R]
        int cnt = prefix[r] - prefix[l - 1];
        cout << cnt << endl;
    }
}

// Driver code
int main()
{
    vector<vector<int> > query = { { 1, 11 },
                                   { 5, 15 },
                                   { 2, 24 } };
    int k = 2, q = query.size();
    performQueries(k, q, query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int maxSize = (int)1e5 + 1;
    static boolean isPrime[] = new boolean[maxSize];
    static int prefix[] = new int[maxSize];

    // Function to return the
    // digit sum of num
    static int digitSum(int num)
    {
        int s = 0;
        while (num != 0)
        {
            s = s + num % 10;
            num = num / 10;
        }
        return s;
    }

    // Sieve Function to generate
    // all primes opto maxSize
    static void sieveOfEratosthenes()
    {
        for (int i = 2; i < maxSize; i++)
        {
            isPrime[i] = true;
        }

        for (int i = 2; i * i <= maxSize; i++)
        {
            if (isPrime[i])
            {
                for (int j = i * i;
                         j < maxSize; j += i)
                {
                    isPrime[j] = false;
                }
            }
        }
    }

    // Pre-Computation till maxSize
    // and for a given K
    static void precompute(int k)
    {
        sieveOfEratosthenes();

        for (int i = 1; i < maxSize; i++)
        {

            // Getting Digit Sum
            int sum = digitSum(i);

            // Check if the digit sum
            // is prime and divisible by k
            if (isPrime[sum] == true &&
                        sum % k == 0)
            {
                prefix[i]++;
            }
        }

        // Taking Prefix Sum
        for (int i = 1; i < maxSize; i++)
        {
            prefix[i] = prefix[i] +
                        prefix[i - 1];
        }
    }

    // Function to perform the queries
    static void performQueries(int k, int q,
                               int query[][])
    {
        // Precompute the results
        precompute(k);

        for (int i = 0; i < q; i++)
        {
            int l = query[i][0], r = query[i][1];

            // Getting count of range in range [L, R]
            int cnt = prefix[r] - prefix[l - 1];

            System.out.println(cnt);
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int query[][] = { { 1, 11 },
                          { 5, 15 },
                          { 2, 24 } };
        int k = 2, q = query.length;
        performQueries(k, q, query);
    }
}

// This Code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

maxSize = 10 ** 5 + 1;
isPrime = [0] * maxSize;
prefix = [0] * maxSize;

# Function to return the
# digit sum of num
def digitSum(num) :

    s = 0;
    while (num != 0) :
        s = s + num % 10;
        num = num // 10;

    return s;

# Sieve Function to generate
# all primes opto maxSize
def sieveOfEratosthenes() :

    for i in range(2, maxSize) :
        isPrime[i] = True;

    for i in range(2, int(sqrt(maxSize)) + 1) :
        if (isPrime[i]) :
            for j in range(i * i, maxSize, i) :
                isPrime[j] = False;

# Pre-Computation till maxSize
# and for a given K
def precompute(k) :

    sieveOfEratosthenes();

    for i in range(1, maxSize) :

        # Getting Digit Sum
        sum = digitSum(i);

        # Check if the digit sum
        # is prime and divisible by k
        if (isPrime[sum] == True and
                    sum % k == 0) :
            prefix[i] += 1;

    # Taking Prefix Sum
    for i in range(1, maxSize) :
        prefix[i] = prefix[i] + prefix[i - 1];

# Function to perform the queries
def performQueries(k, q, query) :

    # Precompute the results
    precompute(k);

    for i in range(q) :
        l = query[i][0]; r = query[i][1];

        # Getting count of range in range [L, R]
        cnt = prefix[r] - prefix[l - 1];
        print(cnt);

# Driver code
if __name__ == "__main__" :

    query = [ [ 1, 11 ],
              [ 5, 15 ],
              [ 2, 24 ] ];

    k = 2; q = len(query);
    performQueries(k, q, query);

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static readonly int maxSize = (int)1e5 + 1;
    static Boolean []isPrime = new Boolean[maxSize];
    static int []prefix = new int[maxSize];

    // Function to return the
    // digit sum of num
    static int digitSum(int num)
    {
        int s = 0;
        while (num != 0)
        {
            s = s + num % 10;
            num = num / 10;
        }
        return s;
    }

    // Sieve Function to generate
    // all primes opto maxSize
    static void sieveOfEratosthenes()
    {
        for (int i = 2; i < maxSize; i++)
        {
            isPrime[i] = true;
        }

        for (int i = 2; i * i <= maxSize; i++)
        {
            if (isPrime[i])
            {
                for (int j = i * i;
                         j < maxSize; j += i)
                {
                    isPrime[j] = false;
                }
            }
        }
    }

    // Pre-Computation till maxSize
    // and for a given K
    static void precompute(int k)
    {
        sieveOfEratosthenes();

        for (int i = 1; i < maxSize; i++)
        {

            // Getting Digit Sum
            int sum = digitSum(i);

            // Check if the digit sum
            // is prime and divisible by k
            if (isPrime[sum] == true &&
                        sum % k == 0)
            {
                prefix[i]++;
            }
        }

        // Taking Prefix Sum
        for (int i = 1; i < maxSize; i++)
        {
            prefix[i] = prefix[i] +
                        prefix[i - 1];
        }
    }

    // Function to perform the queries
    static void performQueries(int k, int q,
                               int [,]query)
    {
        // Precompute the results
        precompute(k);

        for (int i = 0; i < q; i++)
        {
            int l = query[i, 0], r = query[i, 1];

            // Getting count of range in range [L, R]
            int cnt = prefix[r] - prefix[l - 1];

            Console.WriteLine(cnt);
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int [,]query = {{ 1, 11 },
                        { 5, 15 },
                        { 2, 24 }};
        int k = 2, q = query.GetLength(0);
        performQueries(k, q, query);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var maxSize = parseInt(1e5 + 1);
var isPrime = Array.from({length: maxSize},
(_, i) => false);
var prefix = Array.from({length: maxSize},
(_, i) => 0);

// Function to return the
// digit sum of num
function digitSum(num)
{
    var s = 0;
    while (num != 0)
    {
        s = s + num % 10;
        num = parseInt(num / 10);
    }
    return s;
}

// Sieve Function to generate
// all primes opto maxSize
function sieveOfEratosthenes()
{
    for (i = 2; i < maxSize; i++)
    {
        isPrime[i] = true;
    }

    for (i = 2; i * i <= maxSize; i++)
    {
        if (isPrime[i])
        {
            for (j = i * i;
                     j < maxSize; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Pre-Computation till maxSize
// and for a given K
function precompute(k)
{
    sieveOfEratosthenes();

    for (i = 1; i < maxSize; i++)
    {

        // Getting Digit Sum
        var sum = digitSum(i);

        // Check if the digit sum
        // is prime and divisible by k
        if (isPrime[sum] == true &&
                    sum % k == 0)
        {
            prefix[i]++;
        }
    }

    // Taking Prefix Sum
    for (i = 1; i < maxSize; i++)
    {
        prefix[i] = prefix[i] +
                    prefix[i - 1];
    }
}

// Function to perform the queries
function performQueries(k , q, query)
{
    // Precompute the results
    precompute(k);

    for (i = 0; i < q; i++)
    {
        var l = query[i][0], r = query[i][1];

        // Getting count of range in range [L, R]
        var cnt = prefix[r] - prefix[l - 1];

        document.write(cnt+"<br>");
    }
}

// Driver code
var query = [ [ 1, 11 ],
              [ 5, 15 ],
              [ 2, 24 ] ];
var k = 2, q = query.length;
performQueries(k, q, query);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
2
1
3
```