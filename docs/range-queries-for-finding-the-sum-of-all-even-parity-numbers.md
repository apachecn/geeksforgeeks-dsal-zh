# 查找所有偶数奇偶数之和的范围查询

> 原文:[https://www . geesforgeks . org/range-query-for-find-all-sum-of-even-奇偶数/](https://www.geeksforgeeks.org/range-queries-for-finding-the-sum-of-all-even-parity-numbers/)

给定 **Q** 查询，其中每个查询包含两个数字 **L** 和 **R** ，表示一个范围**【L，R】**。任务是找出位于给定范围**【L，R】内的所有[偶宇称数](https://www.geeksforgeeks.org/finding-the-parity-of-a-number-efficiently/)的和。**

> [**一个数的奇偶性**](https://www.geeksforgeeks.org/program-to-find-parity/) 是指它是包含奇数还是偶数的 1 位数。如果该数字包含偶数个 1 位，则它具有**偶校验**。

**例:**

> **输入:** Q = [ [1，10]，[121，211] ]
> **输出:**T5】33
> 7493
> T8】说明:T10】二进制(1) = 01，奇偶校验= 1
> 二进制(2) = 10，奇偶校验= 1
> 二进制(3) = 11，奇偶校验= 2
> 二进制(4) = 100，奇偶校验= 1
> 二进制( 奇偶性= 1
> 二进制(9) = 1001，奇偶性= 2
> 二进制(10) = 1010，奇偶性= 2
> 从 1 到 10，3，5，6，9 和 10 是偶数奇偶性数。 因此总和是 33。
> 从 121 到 211 所有偶数奇偶数之和为 7493。
> **输入:** Q = [ [ 10，10 ]，[ 258，785 ]，[45，245]，[ 1，1000]]
> **输出:**
> 10
> 137676
> 14595
> 250750

**方法:**
思路是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。所有偶校验数的和直到特定的索引被预先计算并存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **pref[]** 中，这样每个查询都可以在 **O(1)** 时间内被回答。

1.  初始化前缀数组 **pref[]** 。
2.  从 1 迭代到 N，检查数字是否具有偶数奇偶校验:
    *   如果该数是偶数奇偶数，那么 **pref[]** 的当前索引将存储到目前为止找到的偶数奇偶数的总和。

    *   否则**pref【】**当前指数与**pref【】**前一指数值相同。
3.  对于 **Q** 查询范围**【L，R】**的所有偶数奇偶数之和可以计算如下:

```
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实施

## C++

```
// C++ program to find the sum
// of all Even Parity numbers
// in the given range

#include <bits/stdc++.h>
using namespace std;

// pref[] array to precompute
// the sum of all Even
// Parity Numbers
int pref[100001] = { 0 };

// Function that returns true
// if count of set bits in
// x is even
int isEvenParity(int num)
{
    // Parity will store the
    // count of set bits
    int parity = 0;
    int x = num;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return num;
    else
        return 0;
}

// Function to precompute the
// sum of all even parity
// numbers upto 100000
void preCompute()
{
    for (int i = 1; i < 100001; i++) {

        // isEvenParity()
        // return the number i
        // if i has even parity
        // else return 0
        pref[i] = pref[i - 1]
                  + isEvenParity(i);
    }
}

// Function to print sum
// for each query
void printSum(int L, int R)
{
    cout << (pref[R] - pref[L - 1])
         << endl;
}

// Function to print sum of all
// even parity numbers between
// [L, R]
void printSum(int arr[2][2], int Q)
{

    // Function that pre computes
    // the sum of all even parity
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0],
                 arr[i][1]);
    }
}
// Driver code
int main()
{
    // Queries
    int N = 2;
    int Q[2][2] = { { 1, 10 },
                    { 121, 211 } };

    // Function that print
    // the sum of all even parity
    // numbers in Range [L, R]
    printSum(Q, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of all Even Parity numbers
// in the given range
import java.io.*;
import java.util.*;

class GFG {

// pref[] array to precompute
// the sum of all Even
// Parity Numbers
static int[] pref = new int[100001];

// Function that returns true
// if count of set bits in
// x is even
static int isEvenParity(int num)
{

    // Parity will store the
    // count of set bits
    int parity = 0;
    int x = num;

    while (x != 0)
    {
        if ((x & 1) == 1)
            parity++;

        x = x >> 1;
    }

    if (parity % 2 == 0)
        return num;
    else
        return 0;
}

// Function to precompute the
// sum of all even parity
// numbers upto 100000
static void preCompute()
{
    for(int i = 1; i < 100001; i++)
    {

       // isEvenParity()
       // return the number i
       // if i has even parity
       // else return 0
       pref[i] = pref[i - 1] + isEvenParity(i);
    }
}

// Function to print sum
// for each query
static void printSum(int L, int R)
{
    System.out.println(pref[R] - pref[L - 1]);
}

// Function to print sum of all
// even parity numbers between
// [L, R]
static void printSum(int arr[][], int Q)
{

    // Function that pre computes
    // the sum of all even parity
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print sum
    for(int i = 0; i < Q; i++)
    {
       printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
public static void main(String[] args)
{

    // Queries
    int N = 2;
    int[][] Q = { { 1, 10 },
                  { 121, 211 } };

    // Function that print
    // the sum of all even parity
    // numbers in Range [L, R]
    printSum(Q, N);
}
}

// This code is contributed by coder001
```

## C#

```
// C# program to find the sum
// of all Even Parity numbers
// in the given range
using System;

class GFG {

// pref[] array to precompute
// the sum of all Even
// Parity Numbers
static int[] pref = new int[100001];

// Function that returns true
// if count of set bits in
// x is even
static int isEvenParity(int num)
{

    // Parity will store the
    // count of set bits
    int parity = 0;
    int x = num;

    while (x != 0)
    {
        if ((x & 1) == 1)
            parity++;

        x = x >> 1;
    }

    if (parity % 2 == 0)
        return num;
    else
        return 0;
}

// Function to precompute the
// sum of all even parity
// numbers upto 100000
static void preCompute()
{
    for(int i = 1; i < 100001; i++)
    {

       // isEvenParity()
       // return the number i
       // if i has even parity
       // else return 0
       pref[i] = pref[i - 1] + isEvenParity(i);
    }
}

// Function to print sum
// for each query
static void printSum(int L, int R)
{
    Console.WriteLine(pref[R] - pref[L - 1]);
}

// Function to print sum of all
// even parity numbers between
// [L, R]
static void printSum(int[,] arr, int Q)
{

    // Function that pre computes
    // the sum of all even parity
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print sum
    for(int i = 0; i < Q; i++)
    {
       printSum(arr[i, 0], arr[i, 1]);
    }
}

// Driver code
public static void Main()
{

    // Queries
    int N = 2;
    int[,] Q = { { 1, 10 },
                 { 121, 211 } };

    // Function that print
    // the sum of all even parity
    // numbers in Range [L, R]
    printSum(Q, N);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>
// Javascript program to find the sum
// of all Even Parity numbers
// in the given range

// pref[] array to precompute
// the sum of all Even
// Parity Numbers
let pref = new Array(100001).fill(0);

// Function that returns true
// if count of set bits in
// x is even
function isEvenParity(num)
{

    // Parity will store the
    // count of set bits
    let parity = 0;
    let x = num;
    while (x != 0) {
        if (x & 1 == 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return num;
    else
        return 0;
}

// Function to precompute the
// sum of all even parity
// numbers upto 100000
function preCompute() {
    for (let i = 1; i < 100001; i++) {

        // isEvenParity()
        // return the number i
        // if i has even parity
        // else return 0
        pref[i] = pref[i - 1] + isEvenParity(i);
    }
}

// Function to print sum
// for each query
function printSum2(L, R) {
    document.write(pref[R] - pref[L - 1] + "<br>");
}

// Function to print sum of all
// even parity numbers between
// [L, R]
function printSum(arr, Q) {

    // Function that pre computes
    // the sum of all even parity
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print sum
    for (let i = 0; i < Q; i++) {
        printSum2(arr[i][0], arr[i][1]);
    }
}

// Driver code

// Queries
let N = 2;
let Q = [[1, 10],
[121, 211]];

// Function that print
// the sum of all even parity
// numbers in Range [L, R]
printSum(Q, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
33
7493
```

***时间复杂度:** O(N)* ，其中 N 是查询中最大的元素。