# 位于 Q 查询的[L，R]范围内的所有完美平方的和

> 原文:[https://www . geeksforgeeks . org/all-sum-of-perfect-squares-in-range-l-r-for-q-query/](https://www.geeksforgeeks.org/sum-of-all-perfect-squares-lying-in-the-range-l-r-for-q-queries/)

给定以 2D 数组**arr【】【】**形式的 **Q** 查询，其每一行由两个数字 **L** 和表示范围【L，R】的 **R** 组成，任务是找到位于该范围内的所有完美正方形的和。
**举例:**

> **输入:** Q = 2，arr[][] = {{4，9}，{4，16}}
> **输出:** 13 29
> **说明:**
> 从 4 到 9:只有 4 和 9 是完美方块。因此，4 + 9 = 13。
> 从 4 到 16: 4、9、16 是最完美的方块。因此，4 + 9 + 16 = 29。
> **输入:** Q = 4，arr[][] = {{1，10}，{1，100}，{2，25}，{4，50}}
> **输出:** 14 385 54 139

**方法:**思路是使用一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。所有平方之和被预先计算并存储在一个数组中 **pref[]** 这样每个查询都可以在 O(1)时间内得到回答。pref[]数组中的每个第 I 个索引代表从 1 到该数字的完美平方之和。因此，从给定范围‘L’到‘R’的完美平方之和可以如下求:

```
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the sum of all
// perfect squares in the given range

#include <bits/stdc++.h>
#define ll int
using namespace std;

// Array to precompute the sum of squares
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
long long pref[100010];

// Function to check if a number is
// a perfect square or not
int isPerfectSquare(long long int x)
{
    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0) ? x : 0;
}

// Function to precompute the perfect
// squares upto 100000.
void compute()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isPerfectSquare(i);
    }
}

// Function to print the sum for each query
void printSum(int L, int R)
{
    int sum = pref[R] - pref[L - 1];
    cout << sum << " ";
}

// Driver code
int main()
{
    // To calculate the precompute function
    compute();

    int Q = 4;
    int arr[][2] = { { 1, 10 },
                     { 1, 100 },
                     { 2, 25 },
                     { 4, 50 } };

    // Calling the printSum function
    // for every query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// perfect squares in the given range
class GFG
{

// Array to precompute the sum of squares
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
static int []pref = new int[100010];

// Function to check if a number is
// a perfect square or not
static int isPerfectSquare(int x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0) ? x : 0;
}

// Function to precompute the perfect
// squares upto 100000.
static void compute()
{
    for (int i = 1; i <= 100000; ++i)
    {
        pref[i] = pref[i - 1]
                + isPerfectSquare(i);
    }
}

// Function to print the sum for each query
static void printSum(int L, int R)
{
    int sum = pref[R] - pref[L - 1];
    System.out.print(sum+ " ");
}

// Driver code
public static void main(String[] args)
{
    // To calculate the precompute function
    compute();

    int Q = 4;
    int arr[][] = { { 1, 10 },
                    { 1, 100 },
                    { 2, 25 },
                    { 4, 50 } };

    // Calling the printSum function
    // for every query
    for (int i = 0; i < Q; i++)
    {
        printSum(arr[i][0], arr[i][1]);
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the sum of all
# perfect squares in the given range
from math import sqrt, floor

# Array to precompute the sum of squares
# from 1 to 100010 so that for every
# query, the answer can be returned in O(1).
pref = [0]*100010;

# Function to check if a number is
# a perfect square or not
def isPerfectSquare(x) :

    # Find floating point value of
    # square root of x.
    sr = sqrt(x);

    # If square root is an integer
    rslt = x if (sr - floor(sr) == 0) else 0;
    return rslt;

# Function to precompute the perfect
# squares upto 100000.
def compute() :

    for i in range(1 , 100001) :
        pref[i] = pref[i - 1] + isPerfectSquare(i);

# Function to print the sum for each query
def printSum( L, R) :

    sum = pref[R] - pref[L - 1];
    print(sum ,end= " ");

# Driver code
if __name__ == "__main__" :

    # To calculate the precompute function
    compute();

    Q = 4;
    arr = [ [ 1, 10 ],
            [ 1, 100 ],
            [ 2, 25 ],
            [ 4, 50 ] ];

    # Calling the printSum function
    # for every query
    for i in range(Q) :
        printSum(arr[i][0], arr[i][1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the sum of all
// perfect squares in the given range
using System;

class GFG
{

// Array to precompute the sum of squares
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
static int []pref = new int[100010];

// Function to check if a number is
// a perfect square or not
static int isPerfectSquare(int x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0) ? x : 0;
}

// Function to precompute the perfect
// squares upto 100000.
static void compute()
{
    for (int i = 1; i <= 100000; ++i)
    {
        pref[i] = pref[i - 1]
                + isPerfectSquare(i);
    }
}

// Function to print the sum for each query
static void printSum(int L, int R)
{
    int sum = pref[R] - pref[L - 1];
    Console.Write(sum+ " ");
}

// Driver code
public static void Main(String[] args)
{
    // To calculate the precompute function
    compute();

    int Q = 4;
    int [,]arr = { { 1, 10 },
                    { 1, 100 },
                    { 2, 25 },
                    { 4, 50 } };

    // Calling the printSum function
    // for every query
    for (int i = 0; i < Q; i++)
    {
        printSum(arr[i, 0], arr[i, 1]);
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the sum of all
// perfect squares in the given range

// Array to precompute the sum of squares
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
var pref= Array(100010).fill(0);

// Function to check if a number is
// a perfect square or not
function isPerfectSquare(x)
{
    // Find floating point value of
    // square root of x.
    var sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0) ? x : 0;
}

// Function to precompute the perfect
// squares upto 100000.
function compute()
{
    for (var i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isPerfectSquare(i);
    }
}

// Function to print the sum for each query
function printSum(L, R)
{
    var sum = pref[R] - pref[L - 1];
    document.write(sum + " ");
}

// Driver code

// To calculate the precompute function
compute();
var Q = 4;
arr = [ [ 1, 10 ],
                 [ 1, 100 ],
                 [ 2, 25 ],
                 [ 4, 50 ] ];

// Calling the printSum function
// for every query
for(var i = 0; i < Q; i++)
    printSum(arr[i][0], arr[i][1]);

</script>
```

**Output:** 

```
14 385 54 139
```