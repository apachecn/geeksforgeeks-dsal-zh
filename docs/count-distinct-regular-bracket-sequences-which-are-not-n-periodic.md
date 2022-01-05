# 计算非周期性的不同规则括号序列

> 原文:[https://www . geesforgeks . org/count-distinct-正则-括号-sequence-哪些不是-n-periodic/](https://www.geeksforgeeks.org/count-distinct-regular-bracket-sequences-which-are-not-n-periodic/)

给定一个整数 **N** ，任务是找到可以使用 **2 * N** 括号形成的不同括号序列的数量，使得该序列不是 **N 周期的**。

> 长度为 **2 * N** 的括号序列**字符串**被称为 **N 周期**，如果该序列可以被分成两个具有相同**常规括号序列**的相等子串。
> A **规则括号顺序**是以下方式的顺序:
> 
> *   空字符串是常规的括号序列。
> *   如果 s & t 是正则括号序列，那么 s + t 就是正则括号序列。

**示例:**

> **输入:** N = 3
> **输出:** 5
> **解释:**
> 将有 5 个长度为 2 * N =()()())、((()))())、((()))、((((())))
> 的截然不同的规则括号序列现在，没有一个序列是 N 周期的。因此，输出为 5。
> 
> **输入:** N = 4
> **输出:** 12
> **解释:**
> 将有 14 个长度为 2*N 的截然不同的规则括号序列，它们分别是
> ()()()()())())()()()()()())()())())()())()())())()())())())())())())())())()))()它们有一个周期 N.
> 因此，长度为 2 * N 的不同规则括号序列是非 N 周期的是 14–2 = 12。

**方法:**想法是计算长度为 **2 * N** 的可能的规则括号序列的总数，然后从中减去 **N 周期**的括号序列的数量。以下是步骤:

1.  要找到长度为 **2*N** 的常规括号序列的数量，请使用[加泰罗尼亚数字](https://www.geeksforgeeks.org/find-number-valid-parentheses-expressions-given-length/)公式。
2.  对于长度为 **2*N** 的序列是 N 周期的，N 应该是偶数，因为如果 N 是奇数，那么长度为 **2*N** 的序列不能是一个规则序列，同时具有一个 N 周期。
3.  由于两个相似的非正则括号序列的连接不能使序列规则，因此长度为 **N** 的两个子序列都应该是规则的。
4.  从长度为 **2*N** 的常规括号序列的数量中减少长度为 **N** 的常规括号序列的数量(如果 N 为偶数)，以获得所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the value of
// Binomial Coefficient C(n, k)
unsigned long int
binomialCoeff(unsigned int n,
              unsigned int k)
{
    unsigned long int res = 1;

    // Since C(n, k) = C(n, n - k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n - 1)*---*(n - k + 1)] /
    // [k*(k - 1)*---*1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    // Return the C(n, k)
    return res;
}

// Binomial coefficient based function to
// find nth catalan number in O(n) time
unsigned long int catalan(unsigned int n)
{
    // Calculate value of 2nCn
    unsigned long int c
        = binomialCoeff(2 * n, n);

    // Return C(2n, n)/(n+1)
    return c / (n + 1);
}

// Function to find possible ways to
// put balanced  parenthesis in an
// expression of length n
unsigned long int findWays(unsigned n)
{
    // If n is odd, not possible to
    // create any valid parentheses
    if (n & 1)
        return 0;

    // Otherwise return n/2th
    // Catalan Number
    return catalan(n / 2);
}

void countNonNPeriodic(int N)
{

    // Difference between counting ways
    // of 2*N and N is the result
    cout << findWays(2 * N)
                - findWays(N);
}

// Driver Code
int main()
{
    // Given value of N
    int N = 4;

    // Function Call
    countNonNPeriodic(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG{

// Function that finds the value of
// Binomial Coefficient C(n, k)
static long binomialCoeff(int n, int k)
{
    long res = 1;

    // Since C(n, k) = C(n, n - k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n - 1)*---*(n - k + 1)] /
    // [k*(k - 1)*---*1]
    for(int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    // Return the C(n, k)
    return res;
}

// Binomial coefficient based function to
// find nth catalan number in O(n) time
static long catalan(int n)
{

    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // Return C(2n, n)/(n+1)
    return c / (n + 1);
}

// Function to find possible ways to
// put balanced parenthesis in an
// expression of length n
static long findWays(int n)
{

    // If n is odd, not possible to
    // create any valid parentheses
    if ((n & 1) == 1)
        return 0;

    // Otherwise return n/2th
    // Catalan Number
    return catalan(n / 2);
}

static void countNonNPeriodic(int N)
{

    // Difference between counting ways
    // of 2*N and N is the result
    System.out.println(findWays(2 * N) -
                       findWays(N));
}

// Driver code
public static void main (String[] args)
{

    // Given value of N
    int N = 4;

    // Function call
    countNonNPeriodic(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function that finds the value of
# Binomial Coefficient C(n, k)
def binomialCoeff(n, k):
    res = 1

    # Since C(n, k) = C(n, n - k)
    if (k > n - k):
        k = n - k

    # Calculate the value of
    # [n*(n - 1)*---*(n - k + 1)] /
    # [k*(k - 1)*---*1]
    for i in range(k):

        res = res * (n - i)
        res = res // (i + 1)

    # Return the C(n, k)
    return res

# Binomial coefficient based function to
# find nth catalan number in O(n) time
def catalan(n):

    # Calculate value of 2nCn
    c = binomialCoeff(2 * n, n)

    # Return C(2n, n)/(n+1)
    return c // (n + 1)

# Function to find possible ways to
# put balanced parenthesis in an
# expression of length n
def findWays(n):

    # If n is odd, not possible to
    # create any valid parentheses
    if ((n & 1) == 1):
        return 0

    # Otherwise return n/2th
    # Catalan Number
    return catalan(n // 2)

def countNonNPeriodic(N):

    # Difference between counting ways
    # of 2*N and N is the result
    print(findWays(2 * N) - findWays(N))

# Driver code
# Given value of N
N = 4

# Function call
countNonNPeriodic(N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function that finds the value of
// Binomial Coefficient C(n, k)
static long binomialCoeff(int n, int k)
{
    long res = 1;

    // Since C(n, k) = C(n, n - k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n - 1)*---*(n - k + 1)] /
    // [k*(k - 1)*---*1]
    for(int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    // Return the C(n, k)
    return res;
}

// Binomial coefficient based function to
// find nth catalan number in O(n) time
static long catalan(int n)
{

    // Calculate value of 2nCn
    long c = binomialCoeff(2 * n, n);

    // Return C(2n, n)/(n+1)
    return c / (n + 1);
}

// Function to find possible ways to
// put balanced parenthesis in an
// expression of length n
static long findWays(int n)
{

    // If n is odd, not possible to
    // create any valid parentheses
    if ((n & 1) == 1)
        return 0;

    // Otherwise return n/2th
    // Catalan Number
    return catalan(n / 2);
}

static void countNonNPeriodic(int N)
{

    // Difference between counting ways
    // of 2*N and N is the result
    Console.Write(findWays(2 * N) -
                  findWays(N));
}

// Driver Code
public static void Main(string[] args)
{

    // Given value of N
    int N = 4;

    // Function call
    countNonNPeriodic(N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds the value of
// Binomial Coefficient C(n, k)
function binomialCoeff(n, k)
{
    let res = 1;

    // Since C(n, k) = C(n, n - k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n - 1)*---*(n - k + 1)] /
    // [k*(k - 1)*---*1]
    for (let i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    // Return the C(n, k)
    return res;
}

// Binomial coefficient based function to
// find nth catalan number in O(n) time
function catalan(n)
{
    // Calculate value of 2nCn
    let c = binomialCoeff(2 * n, n);

    // Return C(2n, n)/(n+1)
    return c / (n + 1);
}

// Function to find possible ways to
// put balanced parenthesis in an
// expression of length n
function findWays(n)
{
    // If n is odd, not possible to
    // create any valid parentheses
    if (n & 1)
        return 0;

    // Otherwise return n/2th
    // Catalan Number
    return catalan(n / 2);
}

function countNonNPeriodic(N)
{

    // Difference between counting ways
    // of 2*N and N is the result
    document.write(findWays(2 * N)
                - findWays(N));
}

// Driver Code

    // Given value of N
    let N = 4;

    // Function Call
    countNonNPeriodic(N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)