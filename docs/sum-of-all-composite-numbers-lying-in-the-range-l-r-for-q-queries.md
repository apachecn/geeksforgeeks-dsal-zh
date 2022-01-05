# Q 查询范围内所有组合数的总和

> 原文:[https://www . geeksforgeeks . org/所有复合数字的总和-范围内-l-r-for-q-query/](https://www.geeksforgeeks.org/sum-of-all-composite-numbers-lying-in-the-range-l-r-for-q-queries/)

给定以 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**形式的 **Q** 查询，其每行由表示范围【L，R】的两个数字 **L** 和 **R** 组成，任务是找到位于范围**【L，R】**中的所有[复合数字](https://www.geeksforgeeks.org/composite-number/)的总和。

> **输入:** arr[][] = {{10，13}，{12，21}}
> **输出:**
> 22
> 116
> **说明:**
> 从 10 到 13 只有 10 和 12 是复合数。
> 从 12 到 21 共有 7 个复合数
> 12+14+15+16+18+20+21 = 116
> **输入:** arr[][] = {{ 10，10 }，{ 258，785 }，{45，245 }，{ 1，1000}}
> **输出:**
> 10
> 233196

**进场:**
思路是使用[前缀和阵](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。直到特定索引所有[合成号](https://www.geeksforgeeks.org/composite-number/)的总和被预先计算并存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**pref【】**中，这样每个查询都可以在 **O(1)** 时间内被回答。

1.  初始化前缀数组 **pref[]** 。
2.  从 1 到 N 迭代[检查数字是否复合](https://www.geeksforgeeks.org/composite-number/):
    *   如果该号码是复合号码，则 **pref[]** 的当前索引将存储该号码与 **pref[]** 的先前索引处的号码之和。
    *   否则**pref【】**当前指数与**pref【】**前一指数值相同。
3.  对于 **Q** 查询范围**【L，R】**的所有[组合数](https://www.geeksforgeeks.org/generate-composite-numbers-less-n/)之和可以找到如下:

```
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the sum
// of all composite numbers
// in the given range

#include <bits/stdc++.h>

using namespace std;

// Prefix array to precompute
// the sum of all composite
// numbers
long long pref[100001];

// Function that return number
// num if num is composite
// else return 0
int isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return 0;
    if (n <= 3)
        return 0;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return n;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return n;

    return 0;
}

// Function to precompute the
// sum of all Composite numbers
// upto 10^5
void preCompute()
{
    for (int i = 1; i <= 100000; ++i) {

        // isComposite()
        // return the number i
        // if i is Composite
        // else return 0
        pref[i] = pref[i - 1]
                + isComposite(i);
    }
}

// Function to print the sum
// for each query
void printSum(int L, int R)
{
    cout << pref[R] - pref[L - 1]
        << endl;
}

// Function to print sum of all
// Composite numbers between
// [L, R]
void printSumComposite(int arr[][2],
                    int Q)
{

    // Function that pre computes
    // the sum of all Composite
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
int main()
{
    // Queries
    int Q = 2;
    int arr[][2] = { { 10, 13 },
                      { 12, 21 } };

    // Function that print the
    // the sum of all composite
    // number in Range [L, R]
    printSumComposite(arr, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum
// of all Composite numbers
// in the given range

import java.util.*;

class GFG {

    // Prefix array to precompute
    // the sum of all Composite
    // number
    static int[] pref = new int[100001];

    // Function that return number
    // num if num is Composite
    // else return 0
    static int isComposite(int n)
    {
        // Corner cases
        if (n <= 1)
            return 0;

        if (n <= 3)
            return 0;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return n;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return n;

        return 0;
    }

    // Function to precompute the
    // sum of all Composite numbers
    // upto 100000
    static void preCompute()
    {
        for (int i = 1; i <= 100000; ++i) {

            // checkComposite()
            // return the number i
            // if i is Composite
            // else return 0
            pref[i] = pref[i - 1]
                    + isComposite(i);
        }
    }

    // Function to print the sum
    // for each query
    static void printSum(int L, int R)
    {
        System.out.print(pref[R] - pref[L - 1]
                        + "\n");
    }

    // Function to print sum of all
    // Composite numbers between
    // [L, R]
    static void printSumComposite(int arr[][],
                                int Q)
    {

        // Function that pre computes
        // the sum of all Composite
        // numbers
        preCompute();

        // Iterate over all Queries
        // to print the sum
        for (int i = 0; i < Q; i++) {
            printSum(arr[i][0], arr[i][1]);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Queries
        int Q = 2;
        int arr[][] = { { 10, 13 },
                        { 12, 21 } };

        // Function that print the
        // the sum of all Composite
        // number in Range [L, R]
        printSumComposite(arr, Q);
    }
}
```

## 蟒蛇 3

```
# Python implementation to find the sum
# of all composite numbers
# in the given range

# Prefix array to precompute
# the sum of all composite
# number
pref =[0]*100001

# Function that return number
# num if num is composite
# else return 0
def isComposite(n):

    # Corner cases
    if (n <= 1):
        return 0
    if (n <= 3):
        return 0

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return n
    i = 5
    while(i * i <= n):

        if (n % i == 0 or n % (i + 2) == 0):
            return n
        i = i + 6

    return 0

# Function to precompute the
# sum of all composite numbers
# upto 100000
def preCompute():
    for i in range(1, 100001):
        # checkcomposite()
        # return the number i
        # if i is composite
        # else return 0
        pref[i] = pref[i - 1]+ isComposite(i)

# Function to print the sum
# for each query
def printSum(L, R):
    print(pref[R] - pref[L - 1])

# Function to prsum of all
# composite numbers between
def printSumcomposite(arr, Q):

    # Function that pre computes
    # the sum of all composite
    # numbers
    preCompute()

    # Iterate over all Queries
    # to print the sum
    for i in range(Q):
        printSum(arr[i][0], arr[i][1])

# Driver code
if __name__ == "__main__":
    Q = 2
    arr = [[10, 13 ], [ 12, 21 ]]

    # Function that print the
    # the sum of all composite
    # number in Range [L, R]
    printSumcomposite(arr, Q)
```

## C#

```
// C# implementation to find the sum
// of all Composite numbers
// in the given range
using System;

public class GFG{

// Prefix array to precompute
// the sum of all Composite
// number
static int[] pref = new int[100001];

// Function that return number
// num if num is Composite
// else return 0
static int isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return 0;

    if (n <= 3)
        return 0;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return n;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return n;

    return 0;
}

// Function to precompute the
// sum of all Composite numbers
// upto 100000
static void preCompute()
{
    for(int i = 1; i <= 100000; ++i)
    {
       // CheckComposite()
       // return the number i
       // if i is Composite
       // else return 0
       pref[i] = pref[i - 1] +
                 isComposite(i);
    }
}

// Function to print the sum
// for each query
static void printSum(int L, int R)
{
    Console.Write(pref[R] -
                  pref[L - 1] + "\n");
}

// Function to print sum of all
// Composite numbers between
// [L, R]
static void printSumComposite(int [,]arr,
                              int Q)
{

    // Function that pre computes
    // the sum of all Composite
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for(int i = 0; i < Q; i++)
    {
       printSum(arr[i, 0], arr[i, 1]);
    }
}

// Driver code
public static void Main(String[] args)
{

    // Queries
    int Q = 2;
    int [,]arr = { { 10, 13 },
                   { 12, 21 } };

    // Function that print the
    // the sum of all Composite
    // number in Range [L, R]
    printSumComposite(arr, Q);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to find the sum
// of all composite numbers
// in the given range

// Prefix array to precompute
// the sum of all composite
// numbers
var pref = Array(100001).fill(0);

// Function that return number
// num if num is composite
// else return 0
function isComposite( n)
{
    // Corner cases
    if (n <= 1)
        return 0;
    if (n <= 3)
        return 0;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return n;

    for (var i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return n;

    return 0;
}

// Function to precompute the
// sum of all Composite numbers
// upto 10^5
function preCompute()
{
    for (var i = 1; i <= 100000; ++i) {

        // isComposite()
        // return the number i
        // if i is Composite
        // else return 0
        pref[i] = pref[i - 1]
                + isComposite(i);
    }
}

// Function to print the sum
// for each query
function printSum(L, R)
{
    document.write( pref[R] - pref[L - 1] +"<br>");
}

// Function to print sum of all
// Composite numbers between
// [L, R]
function printSumComposite(arr, Q)
{

    // Function that pre computes
    // the sum of all Composite
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (var i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
// Queries
var Q = 2;
var arr = [ [ 10, 13 ],
                   [ 12, 21 ] ];
// Function that print the
// the sum of all composite
// number in Range [L, R]
printSumComposite(arr, Q);

</script>
```

**Output:** 

```
22 
116
```

时间复杂度:O(MAX <sup>3/2</sup> ，其中 MAX = 100000

辅助空间:0(1)