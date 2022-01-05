# 查找下一个二进制表示中没有连续 1 的更大元素

> 原文:[https://www . geesforgeks . org/find-next-greater-element-with-no-continuous-in-1-its-binary-presentation/](https://www.geeksforgeeks.org/find-next-greater-element-with-no-consecutive-1-in-its-binary-representation/)

给定 **Q** 查询，其中每个查询由整数 **N** 组成，任务是找到大于 **N** 的最小整数，使得在其二进制表示中没有连续的 **1s** 。

**示例:**

> **输入:** Q[] = {4，6 }
> T3】输出:T5】5
> 8
> 
> **输入:** Q[] = {50，23，456 }
> T3】输出:T5】64
> 32
> 512

**方法:**将所有数字存储在一个列表中，该列表的二进制表示不包含固定限制的连续 1。现在对于每个给定的 **N** ，在之前使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)生成的列表中找到下一个更大的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;

// To store the pre-computed integers
vector<int> v;

// Function that returns true if the
// binary representation of x contains
// consecutive 1s
int consecutiveOnes(int x)
{

    // To store the previous bit
    int p = 0;
    while (x > 0) {

        // Check whether the previous bit
        // and the current bit are both 1
        if (x % 2 == 1 and p == 1)
            return true;

        // Update previous bit
        p = x % 2;

        // Go to the next bit
        x /= 2;
    }
    return false;
}

// Function to pre-compute the
// valid numbers from 0 to MAX
void preCompute()
{
    // Store all the numbers which do
    // not have consecutive 1s
    for (int i = 0; i <= MAX; i++) {
        if (!consecutiveOnes(i))
            v.push_back(i);
    }
}

// Function to return the minimum
// number greater than n which does
// not contain consecutive 1s
int nextValid(int n)
{
    // Search for the next greater element
    // with no consecutive 1s
    int it = upper_bound(v.begin(),
                         v.end(), n)
             - v.begin();
    int val = v[it];
    return val;
}

// Function to perform the queries
void performQueries(int queries[], int q)
{
    for (int i = 0; i < q; i++)
        cout << nextValid(queries[i]) << "\n";
}

// Driver code
int main()
{
    int queries[] = { 4, 6 };
    int q = sizeof(queries) / sizeof(int);

    // Pre-compute the numbers
    preCompute();

    // Perform the queries
    performQueries(queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

static int MAX = 100000;

// To store the pre-computed integers
static ArrayList<Integer> v = new ArrayList<Integer>();

public static int upper_bound(ArrayList<Integer> ar,
                              int k)
{
    int s = 0;
    int e = ar.size();

    while (s != e)
    {
        int mid = s + e >> 1;

        if (ar.get(mid) <= k)
        {
            s = mid + 1;
        }
        else
        {
            e = mid;
        }
    }

    if (s == ar.size())
    {
        return -1;
    }
    return s;
}

// Function that returns true if the
// binary representation of x contains
// consecutive 1s
static int consecutiveOnes(int x)
{

    // To store the previous bit
    int p = 0;

    while (x > 0)
    {

        // Check whether the previous bit
        // and the current bit are both 1
        if (x % 2 == 1 && p == 1)
        {
            return 1;
        }

        // Update previous bit
        p = x % 2;

        // Go to the next bit
        x /= 2;
    }
    return 0;
}

// Function to pre-compute the
// valid numbers from 0 to MAX
static void preCompute()
{

    // Store all the numbers which do
    // not have consecutive 1s
    for(int i = 0; i <= MAX; i++)
    {
        if (consecutiveOnes(i) == 0)
        {
            v.add(i);
        }
    }
}

// Function to return the minimum
// number greater than n which does
// not contain consecutive 1s
static int nextValid(int n)
{

    // Search for the next greater element
    // with no consecutive 1s
    int it = upper_bound(v,n);
    int val = v.get(it);
    return val;
}

// Function to perform the queries
static void performQueries(int queries[], int q)
{
    for(int i = 0; i < q; i++)
    {
        System.out.println(nextValid(queries[i]));
    }
}

// Driver code
public static void main(String[] args)
{
    int queries[] = { 4, 6 };
    int q = queries.length;

    // Pre-compute the numbers
    preCompute();

    // Perform the queries
    performQueries(queries, q);
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect_right as upper_bound

MAX = 100000

# To store the pre-computed integers
v = []

# Function that returns true if the
# binary representation of x contains
# consecutive 1s
def consecutiveOnes(x):

    # To store the previous bit
    p = 0
    while (x > 0):

        # Check whether the previous bit
        # and the current bit are both 1
        if (x % 2 == 1 and p == 1):
            return True

        # Update previous bit
        p = x % 2

        # Go to the next bit
        x //= 2

    return False

# Function to pre-compute the
# valid numbers from 0 to MAX
def preCompute():

    # Store all the numbers which do
    # not have consecutive 1s
    for i in range(MAX + 1):
        if (consecutiveOnes(i) == 0):
            v.append(i)

# Function to return the minimum
# number greater than n which does
# not contain consecutive 1s
def nextValid(n):

    # Search for the next greater element
    # with no consecutive 1s
    it = upper_bound(v, n)
    val = v[it]
    return val

# Function to perform the queries
def performQueries(queries, q):
    for i in range(q):
        print(nextValid(queries[i]))

# Driver code
queries = [4, 6]
q = len(queries)

# Pre-compute the numbers
preCompute()

# Perform the queries
performQueries(queries, q)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

static int MAX = 100000;

// To store the pre-computed integers
static List<int> v = new List<int>();

static int upper_bound(List<int> ar, int k)
{
    int s = 0;
    int e = ar.Count;

    while (s != e)
    {
        int mid = s + e >> 1;

        if (ar[mid] <= k)
        {
            s = mid + 1;
        }
        else
        {
            e = mid;
        }
    }

    if (s == ar.Count)
    {
        return -1;
    }
    return s;
}

// Function that returns true if the
// binary representation of x contains
// consecutive 1s
static int consecutiveOnes(int x)
{

    // To store the previous bit
    int p = 0;

    while (x > 0)
    {

        // Check whether the previous bit
        // and the current bit are both 1
        if (x % 2 == 1 && p == 1)
        {
            return 1;
        }

        // Update previous bit
        p = x % 2;

        // Go to the next bit
        x /= 2;
    }
    return 0;
}

// Function to pre-compute the
// valid numbers from 0 to MAX
static void preCompute()
{

    // Store all the numbers which do
    // not have consecutive 1s
    for(int i = 0; i <= MAX; i++)
    {
        if (consecutiveOnes(i) == 0)
        {
            v.Add(i);
        }
    }
}

// Function to return the minimum
// number greater than n which does
// not contain consecutive 1s
static int nextValid(int n)
{

    // Search for the next greater element
    // with no consecutive 1s
    int it = upper_bound(v, n);
    int val = v[it];
    return val;
}

// Function to perform the queries
static void performQueries(int[] queries, int q)
{
    for(int i = 0; i < q; i++)
    {
        Console.WriteLine(nextValid(queries[i]));
    }
}

// Driver code
static public void Main()
{
    int[] queries = { 4, 6 };
    int q = queries.Length;

    // Pre-compute the numbers
    preCompute();

    // Perform the queries
    performQueries(queries, q);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

const MAX = 100000;

// To store the pre-computed integers
let v = [];

function upper_bound(ar, k)
{
    let s = 0;
    let e = ar.length;

    while (s != e)
    {
        let mid = s + e >> 1;

        if (ar[mid] <= k)
        {
            s = mid + 1;
        }
        else
        {
            e = mid;
        }
    }

    if (s == ar.length)
    {
        return -1;
    }
    return s;
}

// Function that returns true if the
// binary representation of x contains
// consecutive 1s
function consecutiveOnes(x)
{

    // To store the previous bit
    let p = 0;
    while (x > 0) {

        // Check whether the previous bit
        // and the current bit are both 1
        if (x % 2 == 1 && p == 1)
            return true;

        // Update previous bit
        p = x % 2;

        // Go to the next bit
        x = parseInt(x / 2);
    }
    return false;
}

// Function to pre-compute the
// valid numbers from 0 to MAX
function preCompute()
{
    // Store all the numbers which do
    // not have consecutive 1s
    for (let i = 0; i <= MAX; i++) {
        if (!consecutiveOnes(i))
            v.push(i);
    }
}

// Function to return the minimum
// number greater than n which does
// not contain consecutive 1s
function nextValid(n)
{
    // Search for the next greater element
    // with no consecutive 1s
    let it = upper_bound(v, n);
    let val = v[it];
    return val;
}

// Function to perform the queries
function performQueries(queries, q)
{
    for (let i = 0; i < q; i++)
        document.write(nextValid(queries[i]) + "<br>");
}

// Driver code
    let queries = [ 4, 6 ];
    let q = queries.length;

    // Pre-compute the numbers
    preCompute();

    // Perform the queries
    performQueries(queries, q);

</script>
```

**Output:** 

```
5
8
```