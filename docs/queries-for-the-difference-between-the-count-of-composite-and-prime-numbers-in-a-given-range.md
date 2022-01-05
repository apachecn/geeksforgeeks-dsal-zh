# 查询给定范围内复合数和素数的计数之差

> 原文:[https://www . geeksforgeeks . org/查询给定范围内复合数和素数的计数之差/](https://www.geeksforgeeks.org/queries-for-the-difference-between-the-count-of-composite-and-prime-numbers-in-a-given-range/)

给定 **Q** 查询，其中每个查询由两个正整数 **L** 和 **R** 组成，任务是在范围**【L，R】**
**内找到素数计数和复合数计数之间的绝对差示例:**

> **输入:**查询[][] = {{1，10}}
> **输出:**
> 2
> 2、3、5、7 是给定范围内仅有的素数。
> 所以，剩下的 6 个整数是复合的。
> | 6–4 | = 2
> **输入:**查询[][] = {{4，10}，{5，30}}
> **输出:**
> 3
> 10

**进场:**

*   使用厄拉多塞的[筛，生成一个数组**prime【I】**，使得**prime【I】= 1**如果 **i** 是 **prime** 否则 **0** 。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在更新**质数[]** 数组，使得**质数[i]** 存储质数的计数，即 **≤ i** 。
*   对于每一个查询，范围**【L，R】**内素数的计数可以通过**素数【R】–素数【L–1】**求出，复合数的计数将是从元素总数中减去素数的计数。
*   打印素数计数和上一步中找到的合成数之间的绝对差值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000
int prime[MAX + 1];

// Function to update prime[]
// such prime[i] stores the
// count of prime numbers <= i
void updatePrimes()
{
    // prime[] marks all prime numbers as true
    // so prime[i] = 1 if ith number is a prime

    // Initialization
    for (int i = 2; i <= MAX; i++) {
        prime[i] = 1;
    }

    // 0 and 1 are not primes
    prime[0] = prime[1] = 0;

    // Mark composite numbers as false
    // and prime numbers as true
    for (int i = 2; i * i <= MAX; i++) {
        if (prime[i] == 1) {
            for (int j = i * i; j <= MAX; j += i) {
                prime[j] = 0;
            }
        }
    }

    // Update prime[] such that
    // prime[i] will store the count of
    // all the prime numbers <= i
    for (int i = 1; i <= MAX; i++) {
        prime[i] += prime[i - 1];
    }
}

// Function to return the absolute difference
// between the number of primes and the number
// of composite numbers in the range [l, r]
int getDifference(int l, int r)
{

    // Total elements in the range
    int total = r - l + 1;

    // Count of primes in the range [l, r]
    int primes = prime[r] - prime[l - 1];

    // Count of composite numbers
    // in the range [l, r]
    int composites = total - primes;

    // Return the sbsolute difference
    return (abs(primes - composites));
}

// Driver code
int main()
{
    int queries[][2] = { { 1, 10 }, { 5, 30 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    updatePrimes();

    // Perform queries
    for (int i = 0; i < q; i++)
        cout << getDifference(queries[i][0],
                              queries[i][1])
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
    static int MAX = 1000000;
    static int []prime = new int[MAX + 1];

    // Function to update prime[]
    // such prime[i] stores the
    // count of prime numbers <= i
    static void updatePrimes()
    {
        // prime[] marks all prime numbers as true
        // so prime[i] = 1 if ith number is a prime

        // Initialization
        for (int i = 2; i <= MAX; i++)
        {
            prime[i] = 1;
        }

        // 0 and 1 are not primes
        prime[0] = prime[1] = 0;

        // Mark composite numbers as false
        // and prime numbers as true
        for (int i = 2; i * i <= MAX; i++)
        {
            if (prime[i] == 1)
            {
                for (int j = i * i; j <= MAX; j += i)
                {
                    prime[j] = 0;
                }
            }
        }

        // Update prime[] such that
        // prime[i] will store the count of
        // all the prime numbers <= i
        for (int i = 1; i <= MAX; i++)
        {
            prime[i] += prime[i - 1];
        }
    }

    // Function to return the absolute difference
    // between the number of primes and the number
    // of composite numbers in the range [l, r]
    static int getDifference(int l, int r)
    {

        // Total elements in the range
        int total = r - l + 1;

        // Count of primes in the range [l, r]
        int primes = prime[r] - prime[l - 1];

        // Count of composite numbers
        // in the range [l, r]
        int composites = total - primes;

        // Return the sbsolute difference
        return (Math.abs(primes - composites));
    }

    // Driver code
    public static void main (String[] args)
    {

        int queries[][] = { { 1, 10 }, { 5, 30 } };
        int q = queries.length;
        updatePrimes();

        // Perform queries
        for (int i = 0; i < q; i++)
            System.out.println (getDifference(queries[i][0],
                                queries[i][1]));

    }
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

MAX = 1000000
prime = [0]*(MAX + 1);

# Function to update prime[]
# such prime[i] stores the
# count of prime numbers <= i
def updatePrimes() :

    # prime[] marks all prime numbers as true
    # so prime[i] = 1 if ith number is a prime

    # Initialization
    for i in range(2, MAX + 1) :
        prime[i] = 1;

    # 0 and 1 are not primes
    prime[0] = prime[1] = 0;

    # Mark composite numbers as false
    # and prime numbers as true
    for i in range(2, int(sqrt(MAX) + 1)) :
        if (prime[i] == 1) :
            for j in range(i*i, MAX, i) :
                prime[j] = 0;

    # Update prime[] such that
    # prime[i] will store the count of
    # all the prime numbers <= i
    for i in range(1, MAX) :
        prime[i] += prime[i - 1];

# Function to return the absolute difference
# between the number of primes and the number
# of composite numbers in the range [l, r]
def getDifference(l, r) :

    # Total elements in the range
    total = r - l + 1;

    # Count of primes in the range [l, r]
    primes = prime[r] - prime[l - 1];

    # Count of composite numbers
    # in the range [l, r]
    composites = total - primes;

    # Return the sbsolute difference
    return (abs(primes - composites));

# Driver code
if __name__ == "__main__" :

    queries = [ [ 1, 10 ],[ 5, 30 ] ];
    q = len(queries);

    updatePrimes();

    # Perform queries
    for i in range(q) :
        print(getDifference(queries[i][0],
                            queries[i][1]))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAX = 1000000;
    static int []prime = new int[MAX + 1];

    // Function to update prime[]
    // such prime[i] stores the
    // count of prime numbers <= i
    static void updatePrimes()
    {
        // prime[] marks all prime numbers as true
        // so prime[i] = 1 if ith number is a prime

        // Initialization
        for (int i = 2; i <= MAX; i++)
        {
            prime[i] = 1;
        }

        // 0 and 1 are not primes
        prime[0] = prime[1] = 0;

        // Mark composite numbers as false
        // and prime numbers as true
        for (int i = 2; i * i <= MAX; i++)
        {
            if (prime[i] == 1)
            {
                for (int j = i * i; j <= MAX; j += i)
                {
                    prime[j] = 0;
                }
            }
        }

        // Update prime[] such that
        // prime[i] will store the count of
        // all the prime numbers <= i
        for (int i = 1; i <= MAX; i++)
        {
            prime[i] += prime[i - 1];
        }
    }

    // Function to return the absolute difference
    // between the number of primes and the number
    // of composite numbers in the range [l, r]
    static int getDifference(int l, int r)
    {

        // Total elements in the range
        int total = r - l + 1;

        // Count of primes in the range [l, r]
        int primes = prime[r] - prime[l - 1];

        // Count of composite numbers
        // in the range [l, r]
        int composites = total - primes;

        // Return the sbsolute difference
        return (Math.Abs(primes - composites));
    }

    // Driver code
    public static void Main ()
    {

        int [,]queries = { { 1, 10 }, { 5, 30 } };
        int q = queries.GetLength(0);
        updatePrimes();

        // Perform queries
        for (int i = 0; i < q; i++)
            Console.WriteLine(getDifference(queries[i,0],
                                queries[i,1]));

    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MAX = 1000000;
let prime = new Array(MAX + 1);

// Function to update prime[]
// such prime[i] stores the
// count of prime numbers <= i
function updatePrimes()
{
    // prime[] marks all prime numbers as true
    // so prime[i] = 1 if ith number is a prime

    // Initialization
    for (let i = 2; i <= MAX; i++) {
        prime[i] = 1;
    }

    // 0 and 1 are not primes
    prime[0] = prime[1] = 0;

    // Mark composite numbers as false
    // and prime numbers as true
    for (let i = 2; i * i <= MAX; i++) {
        if (prime[i] == 1) {
            for (let j = i * i; j <= MAX; j += i)
            {
                prime[j] = 0;
            }
        }
    }

    // Update prime[] such that
    // prime[i] will store the count of
    // all the prime numbers <= i
    for (let i = 1; i <= MAX; i++) {
        prime[i] += prime[i - 1];
    }
}

// Function to return the absolute difference
// between the number of primes and the number
// of composite numbers in the range [l, r]
function getDifference(l, r)
{

    // Total elements in the range
    let total = r - l + 1;

    // Count of primes in the range [l, r]
    let primes = prime[r] - prime[l - 1];

    // Count of composite numbers
    // in the range [l, r]
    let composites = total - primes;

    // Return the sbsolute difference
    return (Math.abs(primes - composites));
}

// Driver code
    let queries = [ [ 1, 10 ], [ 5, 30 ] ];
    let q = queries.length;

    updatePrimes();

    // Perform queries
    for (let i = 0; i < q; i++)
        document.write(getDifference(queries[i][0],
                          queries[i][1]) + "<br>");

</script>
```

**Output:** 

```
2
10
```