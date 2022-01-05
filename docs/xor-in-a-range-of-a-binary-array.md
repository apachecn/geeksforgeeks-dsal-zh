# 二进制数组范围内的异或运算

> 原文:[https://www . geeksforgeeks . org/二进制数组范围内的 xor/](https://www.geeksforgeeks.org/xor-in-a-range-of-a-binary-array/)

给定大小为 **N** 的二进制数组 **arr[]** 和一些查询。每个查询代表一个索引范围**【l，r】**。任务是为每个查询找到给定索引范围内元素的**异或**，即 **arr[l] ^ arr[l + 1] ^ … ^ arr[r]** 。
**举例:**

> **输入:** arr[] = {1，0，1，1，0，1，1}，q[][] = {{0，3}，{0，2}}
> **输出:**t5】1
> 0
> 查询 1:arr[0]^ arr[1]^ arr[2]^ arr[3]= 1 ^ 0 ^ 1 ^ 1 = 1
> 查询 1:arr[0]^ arr[1]^ arr[2]= 1 0 1 = 0【T9

**进场:**主要观察的是，要求的答案总是要么 **0** 要么 **1** 。如果给定范围内的 1 的数量是奇数，那么答案将是 **1** 。否则 **0** 。要在恒定时间内回答多个查询，请使用前缀和数组 **pre[]** ，其中 **pre[i]** 将原始数组中的 1 的数量存储在索引范围**【0，I】**中，该数组可用于查找给定数组的任何索引范围中的 1 的数量。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Xor in a range
// of a binary array
int xorRange(int pre[], int l, int r)
{

    // To store the count of 1s
    int cntOnes = pre[r];
    if (l - 1 >= 0)
        cntOnes -= pre[l - 1];

    // If number of ones are even
    if (cntOnes % 2 == 0)
        return 0;

    // If number of ones are odd
    else
        return 1;
}

// Function to perform the queries
void performQueries(int queries[][2], int q,
                    int a[], int n)
{
    // To store prefix sum
    int pre[n];

    // pre[i] stores the number of
    // 1s from pre[0] to pre[i]
    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + a[i];

    // Perform queries
    for (int i = 0; i < q; i++)
        cout << xorRange(pre, queries[i][0],
                         queries[i][1])
             << endl;
}

// Driver code
int main()
{
    int a[] = { 1, 0, 1, 1, 0, 1, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    // Given queries
    int queries[][2] = { { 0, 3 }, { 0, 2 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    performQueries(queries, q, a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return Xor in a range
// of a binary array
static int xorRange(int pre[], int l, int r)
{

    // To store the count of 1s
    int cntOnes = pre[r];
    if (l - 1 >= 0)
        cntOnes -= pre[l - 1];

    // If number of ones are even
    if (cntOnes % 2 == 0)
        return 0;

    // If number of ones are odd
    else
        return 1;
}

// Function to perform the queries
static void performQueries(int queries[][], int q,
                           int a[], int n)
{
    // To store prefix sum
    int []pre = new int[n];

    // pre[i] stores the number of
    // 1s from pre[0] to pre[i]
    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + a[i];

    // Perform queries
    for (int i = 0; i < q; i++)
        System.out.println(xorRange(pre, queries[i][0],
                                         queries[i][1]));
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 0, 1, 1, 0, 1, 1 };
    int n = a.length;

    // Given queries
    int queries[][] = { { 0, 3 }, { 0, 2 } };
    int q = queries.length;

    performQueries(queries, q, a, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return Xor in a range
# of a binary array
def xorRange(pre, l, r):

    # To store the count of 1s
    cntOnes = pre[r]
    if (l - 1 >= 0):
        cntOnes -= pre[l - 1]

    # If number of ones are even
    if (cntOnes % 2 == 0):
        return 0

    # If number of ones are odd
    else:
        return 1

# Function to perform the queries
def performQueries(queries, q, a, n):

    # To store prefix sum
    pre = [0 for i in range(n)]

    # pre[i] stores the number of
    # 1s from pre[0] to pre[i]
    pre[0] = a[0]
    for i in range(1, n):
        pre[i] = pre[i - 1] + a[i]

    # Perform queries
    for i in range(q):
        print(xorRange(pre, queries[i][0],
                            queries[i][1]))

# Driver code
a = [ 1, 0, 1, 1, 0, 1, 1 ]
n = len(a)

# Given queries
queries = [[ 0, 3 ], [ 0, 2 ]]
q = len(queries)

performQueries(queries, q, a, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return Xor in a range
// of a binary array
static int xorRange(int []pre, int l, int r)
{

    // To store the count of 1s
    int cntOnes = pre[r];
    if (l - 1 >= 0)
        cntOnes -= pre[l - 1];

    // If number of ones are even
    if (cntOnes % 2 == 0)
        return 0;

    // If number of ones are odd
    else
        return 1;
}

// Function to perform the queries
static void performQueries(int [,]queries, int q,
                           int []a, int n)
{
    // To store prefix sum
    int []pre = new int[n];

    // pre[i] stores the number of
    // 1s from pre[0] to pre[i]
    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + a[i];

    // Perform queries
    for (int i = 0; i < q; i++)
        Console.WriteLine(xorRange(pre, queries[i, 0],
                                        queries[i, 1]));
}

// Driver code
public static void Main()
{
    int []a = { 1, 0, 1, 1, 0, 1, 1 };
    int n = a.Length;

    // Given queries
    int [,]queries = { { 0, 3 }, { 0, 2 } };
    int q = queries.Length;

    performQueries(queries, q, a, n);
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return Xor in a range
// of a binary array
function xorRange(pre, l, r)
{

    // To store the count of 1s
    let cntOnes = pre[r];
    if (l - 1 >= 0)
        cntOnes -= pre[l - 1];

    // If number of ones are even
    if (cntOnes % 2 == 0)
        return 0;

    // If number of ones are odd
    else
        return 1;
}

// Function to perform the queries
function performQueries(queries, q, a, n)
{
    // To store prefix sum
    let pre = new Array(n);

    // pre[i] stores the number of
    // 1s from pre[0] to pre[i]
    pre[0] = a[0];
    for (let i = 1; i < n; i++)
        pre[i] = pre[i - 1] + a[i];

    // Perform queries
    for (let i = 0; i < q; i++)
        document.write(xorRange(pre, queries[i][0],
                         queries[i][1]) + "<br>");
}

// Driver code
    let a = [ 1, 0, 1, 1, 0, 1, 1 ];
    let n = a.length;

    // Given queries
    let queries = [ [ 0, 3 ], [ 0, 2 ] ];
    let q = queries.length;

    performQueries(queries, q, a, n);

</script>
```

**Output:** 

```
1
0
```