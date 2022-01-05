# Q 查询范围内所有非斐波那契数的总和

> 原文:[https://www . geeksforgeeks . org/q 查询范围内所有非斐波那契数之和/](https://www.geeksforgeeks.org/sum-of-all-non-fibonacci-numbers-in-a-range-for-q-queries/)

给定包含以**【L，R】**形式的范围的 **Q** 查询，任务是找到给定查询中每个范围的所有非斐波那契数的和。
**例:**

> **输入:** arr[][] = {{1，5}，{6，10}}
> **输出:** 4 32
> **解释:**
> 查询 1:在[1，5]范围内，只有 4 是非斐波那契数。
> 查询 2:在[6，10]范围内，6，7，9，10 是非斐波那契数。
> 因此，6 + 7 + 9 + 10 = 32。
> **输入:** arr[][] = {{10，20}，{20，50}}
> **输出:** 152 10792

**方法:**思路是使用一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。所有[非斐波那契数](https://www.geeksforgeeks.org/nth-non-fibonacci-number/)的总和被预先计算并存储在一个数组中。以便每个查询都能在 O(1)时间内得到回答。数组的每个索引都存储从 1 到该索引的所有非斐波那契数的总和。因此，为了找到一个范围内所有非斐波那契数的和，可以计算为:

```
Let the precomputed array is stored in pref[] array
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// sum of all non-fibonacci numbers
// in a range from L to R

#include <bits/stdc++.h>
#define ll int
using namespace std;

// Array to precompute the sum of
// non-fibonacci numbers
long long pref[100010];

// Function to find if a number
// is a perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function that returns N
// if N is non-fibonacci number
int isNonFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 0;
    else
        return n;
}

// Function to precompute sum of
// non-fibonacci Numbers
void compute()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isNonFibonacci(i);
    }
}

// Function to find the sum of all
// non-fibonacci numbers in a range
void printSum(int L, int R)
{
    int sum = pref[R] - pref[L - 1];
    cout << sum << " ";
}

// Driver Code
int main()
{
    // Pre-computation
    compute();

    int Q = 2;
    int arr[][2] = { { 1, 5 },
                     { 6, 10 } };
    // Loop to find the sum for
    // each query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// sum of all non-fibonacci numbers
// in a range from L to R
import java.util.*;

// Array to precompute the sum of
// non-fibonacci numbers

class GFG
{
static long pref[] = new long[100010];

// Function to find if a number
// is a perfect square
static boolean isPerfectSquare(int x)
{
    int s =(int)Math.sqrt(x);
    return (s * s == x);
}

// Function that returns N
// if N is non-fibonacci number
static int isNonFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 0;
    else
        return n;
}

// Function to precompute sum of
// non-fibonacci Numbers
static void compute()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isNonFibonacci(i);
    }
}

// Function to find the sum of all
// non-fibonacci numbers in a range
static void printSum(int L, int R)
{
    int sum = (int)(pref[R] - pref[L - 1]);
    System.out.print(sum + " ");
}

// Driver Code
public static void main(String []args)
{
    // Pre-computation
    compute();

    int Q = 2;
    int arr[][] = { { 1, 5 },
                     { 6, 10 } };
    // Loop to find the sum for
    // each query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# sum of all non-fibonacci numbers
# in a range from L to R
from math import sqrt

# Array to precompute the sum of
# non-fibonacci numbers
pref = [0]*100010

# Function to find if a number
# is a perfect square
def isPerfectSquare(x):

    s = int(sqrt(x))
    if (s * s == x):
        return True
    return False

# Function that returns N
# if N is non-fibonacci number
def isNonFibonacci(n):

    # N is Fibinacci if one of
    # 5*n*n + 4 or 5*n*n - 4 or both
    # are perferct square
    x = 5 * n * n
    if (isPerfectSquare(x + 4) or isPerfectSquare(x - 4)):
        return 0
    else:
        return n

# Function to precompute sum of
# non-fibonacci Numbers
def compute():

    for i in range(1,100001):
        pref[i] = pref[i - 1] + isNonFibonacci(i)

# Function to find the sum of all
# non-fibonacci numbers in a range
def printSum(L, R):

    sum = pref[R] - pref[L-1]
    print(sum, end=" ")

# Driver Code
# Pre-computation
compute()

Q = 2
arr = [[1, 5],[6, 10]]
# Loop to find the sum for
# each query

for i in range(Q):
    printSum(arr[i][0], arr[i][1])

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find the
// sum of all non-fibonacci numbers
// in a range from L to R
using System;

// Array to precompute the sum of
// non-fibonacci numbers
class GFG
{
static long []pref = new long[100010];

// Function to find if a number
// is a perfect square
static bool isPerfectSquare(int x)
{
    int s =(int)Math.Sqrt(x);
    return (s * s == x);
}

// Function that returns N
// if N is non-fibonacci number
static int isNonFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 0;
    else
        return n;
}

// Function to precompute sum of
// non-fibonacci Numbers
static void compute()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isNonFibonacci(i);
    }
}

// Function to find the sum of all
// non-fibonacci numbers in a range
static void printSum(int L, int R)
{
    int sum = (int)(pref[R] - pref[L - 1]);
    Console.Write(sum + " ");
}

// Driver Code
public static void Main(String []args)
{
    // Pre-computation
    compute();

    int Q = 2;
    int [,]arr = { { 1, 5 },
                     { 6, 10 } };
    // Loop to find the sum for
    // each query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i,0], arr[i,1]);
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// sum of all non-fibonacci numbers
// in a range from L to R

// Array to precompute the sum of
// non-fibonacci numbers
var pref = Array(100010).fill(0);

// Function to find if a number
// is a perfect square
function isPerfectSquare(x)
{
    var s = parseInt(Math.sqrt(x));
    return (s * s == x);
}

// Function that returns N
// if N is non-fibonacci number
function isNonFibonacci(n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 0;
    else
        return n;
}

// Function to precompute sum of
// non-fibonacci Numbers
function compute()
{
    for (var i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isNonFibonacci(i);
    }
}

// Function to find the sum of all
// non-fibonacci numbers in a range
function printSum(L, R)
{
    var sum = pref[R] - pref[L - 1];
    document.write(sum + " ");
}

// Driver Code
// Pre-computation
compute();
var Q = 2;
var arr = [ [ 1, 5 ],
                 [ 6, 10 ] ];
// Loop to find the sum for
// each query
for (var i = 0; i < Q; i++) {
    printSum(arr[i][0], arr[i][1]);
}

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4 32
```

**业绩分析:**

*   **时间复杂度:**与上面的方法一样，存在花费 O(N)时间的预计算，并且回答每个查询花费 **O(1)** 时间。
*   **辅助空间复杂度:**和上面的方法一样，有额外的空间用于预计算所有非斐波那契数的和。因此辅助空间的复杂性将是 **O(N)** 。