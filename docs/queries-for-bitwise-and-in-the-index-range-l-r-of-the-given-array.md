# 查询给定数组的索引范围[L，R]中的按位“与”

> 原文:[https://www . geeksforgeeks . org/按位查询给定数组的索引范围 l-r/](https://www.geeksforgeeks.org/queries-for-bitwise-and-in-the-index-range-l-r-of-the-given-array/)

给定由范围**【L，R】**组成的 **N** 和 **Q** 查询的数组 **arr[]** 。任务是找到该索引范围内所有元素的位与。
**举例:**

> **输入:** arr[] = {1，3，1，2，3，4}，q[] = {{0，1}，{3，5}}
> **输出:**
> 1
> 0
> 1 AND 3 = 1
> 2 AND 3 AND 4 = 0
> **输入:** arr[] = {1，2，3，4，5}，q[] = {{0，4}，{1，3}}

**天真的方法:**遍历该范围，找到该范围内所有数字的逐位“与”。对于每个查询，这将花费 O(n)个时间。
**高效方法:**如果我们把整数看成二进制数，我们很容易看出，我们的答案中 **i <sup>第</sup>T8】位需要设置的条件是**【L，R】**范围内所有整数的 **i <sup>第</sup>T12】位都要设置。
因此，我们将计算每个位的前缀计数。我们将使用它来查找设置了 **i <sup>th</sup>** 位的范围内的整数数量。如果它等于范围的大小，那么我们的答案的 **i <sup>第</sup>** 位也将被设置。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MAX 100000
#define bitscount 32
using namespace std;

// Array to store bit-wise
// prefix count
int prefix_count[bitscount][MAX];

// Function to find the prefix sum
void findPrefixCount(int arr[], int n)
{

    // Loop for each bit
    for (int i = 0; i < bitscount; i++) {

        // Loop to find prefix count
        prefix_count[i][0] = ((arr[0] >> i) & 1);
        for (int j = 1; j < n; j++) {
            prefix_count[i][j] = ((arr[j] >> i) & 1);
            prefix_count[i][j] += prefix_count[i][j - 1];
        }
    }
}

// Function to answer query
int rangeAnd(int l, int r)
{

    // To store the answer
    int ans = 0;

    // Loop for each bit
    for (int i = 0; i < bitscount; i++) {
        // To store the number of variables
        // with ith bit set
        int x;
        if (l == 0)
            x = prefix_count[i][r];
        else
            x = prefix_count[i][r]
                - prefix_count[i][l - 1];

        // Condition for ith bit
        // of answer to be set
        if (x == r - l + 1)
            ans = (ans | (1 << i));
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 7, 5, 3, 5, 2, 3 };
    int n = sizeof(arr) / sizeof(int);

    findPrefixCount(arr, n);

    int queries[][2] = { { 1, 3 }, { 4, 5 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    for (int i = 0; i < q; i++)
        cout << rangeAnd(queries[i][0],
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

static int MAX = 100000;
static int bitscount =32;

// Array to store bit-wise
// prefix count
static int [][]prefix_count = new int [bitscount][MAX];

// Function to find the prefix sum
static void findPrefixCount(int arr[], int n)
{

    // Loop for each bit
    for (int i = 0; i < bitscount; i++)
    {

        // Loop to find prefix count
        prefix_count[i][0] = ((arr[0] >> i) & 1);
        for (int j = 1; j < n; j++)
        {
            prefix_count[i][j] = ((arr[j] >> i) & 1);
            prefix_count[i][j] += prefix_count[i][j - 1];
        }
    }
}

// Function to answer query
static int rangeAnd(int l, int r)
{

    // To store the answer
    int ans = 0;

    // Loop for each bit
    for (int i = 0; i < bitscount; i++)
    {
        // To store the number of variables
        // with ith bit set
        int x;
        if (l == 0)
            x = prefix_count[i][r];
        else
            x = prefix_count[i][r]
                - prefix_count[i][l - 1];

        // Condition for ith bit
        // of answer to be set
        if (x == r - l + 1)
            ans = (ans | (1 << i));
    }

    return ans;
}

// Driver code
public static void main (String[] args)
{

    int arr[] = { 7, 5, 3, 5, 2, 3 };
    int n = arr.length;

    findPrefixCount(arr, n);

    int queries[][] = { { 1, 3 }, { 4, 5 } };
    int q = queries.length;

    for (int i = 0; i < q; i++)
                System.out.println (rangeAnd(queries[i][0],queries[i][1]));

}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import numpy as np

MAX = 100000
bitscount = 32

# Array to store bit-wise
# prefix count
prefix_count = np.zeros((bitscount,MAX));

# Function to find the prefix sum
def findPrefixCount(arr, n) :

    # Loop for each bit
    for i in range(0, bitscount) :

        # Loop to find prefix count
        prefix_count[i][0] = ((arr[0] >> i) & 1);

        for j in range(1, n) :
            prefix_count[i][j] = ((arr[j] >> i) & 1);
            prefix_count[i][j] += prefix_count[i][j - 1];

# Function to answer query
def rangeOr(l, r) :

    # To store the answer
    ans = 0;

    # Loop for each bit
    for i in range(bitscount) :

        # To store the number of variables
        # with ith bit set
        x = 0;

        if (l == 0) :
            x = prefix_count[i][r];
        else :
            x = prefix_count[i][r] - prefix_count[i][l - 1];

        # Condition for ith bit
        # of answer to be set
        if (x == r - l + 1) :
            ans = (ans | (1 << i));

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 7, 5, 3, 5, 2, 3 ];
    n = len(arr);

    findPrefixCount(arr, n);

    queries = [ [ 1, 3 ], [ 4, 5 ] ];

    q = len(queries);

    for i in range(q) :
        print(rangeOr(queries[i][0], queries[i][1]));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 100000;
static int bitscount =32;

// Array to store bit-wise
// prefix count
static int [,]prefix_count = new int [bitscount,MAX];

// Function to find the prefix sum
static void findPrefixCount(int []arr, int n)
{

    // Loop for each bit
    for (int i = 0; i < bitscount; i++)
    {

        // Loop to find prefix count
        prefix_count[i,0] = ((arr[0] >> i) & 1);
        for (int j = 1; j < n; j++)
        {
            prefix_count[i,j] = ((arr[j] >> i) & 1);
            prefix_count[i,j] += prefix_count[i,j - 1];
        }
    }
}

// Function to answer query
static int rangeAnd(int l, int r)
{

    // To store the answer
    int ans = 0;

    // Loop for each bit
    for (int i = 0; i < bitscount; i++)
    {
        // To store the number of variables
        // with ith bit set
        int x;
        if (l == 0)
            x = prefix_count[i,r];
        else
            x = prefix_count[i,r]
                - prefix_count[i,l - 1];

        // Condition for ith bit
        // of answer to be set
        if (x == r - l + 1)
            ans = (ans | (1 << i));
    }

    return ans;
}

// Driver code
public static void Main (String[] args)
{

    int []arr = { 7, 5, 3, 5, 2, 3 };
    int n = arr.Length;

    findPrefixCount(arr, n);

    int [,]queries = { { 1, 3 }, { 4, 5 } };
    int q = queries.GetLength(0);

    for (int i = 0; i < q; i++)
            Console.WriteLine(rangeAnd(queries[i,0],queries[i,1]));

}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    let MAX = 100000;
    let bitscount =32;

    // Array to store bit-wise
    // prefix count
    let prefix_count = new Array(bitscount);

    for (let i = 0; i < bitscount; i++)
    {
        prefix_count[i] = new Array(MAX);
        for (let j = 0; j < MAX; j++)
        {
            prefix_count[i][j] = 0;
        }
    }

    // Function to find the prefix sum
    function findPrefixCount(arr, n)
    {
        // Loop for each bit
        for (let i = 0; i < bitscount; i++)
        {

            // Loop to find prefix count
            prefix_count[i][0] = ((arr[0] >> i) & 1);
            for (let j = 1; j < n; j++)
            {
                prefix_count[i][j] = ((arr[j] >> i) & 1);
                prefix_count[i][j] += prefix_count[i][j - 1];
            }
        }
    }

    // Function to answer query
    function rangeAnd(l, r)
    {

        // To store the answer
        let ans = 0;

        // Loop for each bit
        for (let i = 0; i < bitscount; i++)
        {
            // To store the number of variables
            // with ith bit set
            let x;
            if (l == 0)
                x = prefix_count[i][r];
            else
                x = prefix_count[i][r]
                    - prefix_count[i][l - 1];

            // Condition for ith bit
            // of answer to be set
            if (x == r - l + 1)
                ans = (ans | (1 << i));
        }

        return ans;
    }

    let arr = [ 7, 5, 3, 5, 2, 3 ];
    let n = arr.length;

    findPrefixCount(arr, n);

    let queries = [ [ 1, 3 ], [ 4, 5 ] ];
    let q = queries.length;

    for (let i = 0; i < q; i++)
          document.write(rangeAnd(queries[i][0],queries[i][1]) + "</br>");
</script>
```

**Output:** 

```
1
2
```

预计算的时间复杂度为 O(n)，每个查询都可以用 O(1)来回答

辅助空间:0(位数*最大值)