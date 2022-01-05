# 0-1 背包查询

> 原文:[https://www.geeksforgeeks.org/0-1-knapsack-queries/](https://www.geeksforgeeks.org/0-1-knapsack-queries/)

给定一个由项目权重组成的整数数组**W【】**和一些由背包容量 **C** 组成的查询，对于每个查询找到我们可以放入背包的最大权重。 **C** 的值不超过某个整数 **C_MAX** 。

**示例:**

> **输入:** W[] = {3，8，9} q = {11，10，4}
> **输出:**T5】11
> 9
> 3
> 如果 C = 11:选择 3 + 8 = 11
> 如果 C = 10:选择 9
> 如果 C = 4:选择 3
> 
> **输入:** W[] = {1，5，10} q = {6，14 }
> T3】输出:T5】6
> 11

建议你在尝试这个问题之前先看完这篇关于 [0-1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)的文章。

**天真的方法:**对于每个查询，我们可以生成所有可能的权重子集，并在所有适合背包的子集中选择权重最大的子集。因此，回答每个查询将花费指数级的时间。

**高效方法:**我们将使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)优化每个查询的回答。
0-1 背包使用二维动态规划求解，一个状态' I '表示当前索引(即选择或拒绝)，一个状态表示剩余容量' R '。
递归关系为

> DP[I][r]= max(arr[I]+DP[I+1][r–arr[I]、DP[I+1][r])t 0]

我们将为 0(C_MAX * I)中 1 到 C _ MAX 之间的每个可能的“C”值预先计算二维数组 dp[i][C]。
利用这个，预计算我们可以在 O(1)时间内回答每个查询。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define C_MAX 30
#define max_arr_len 10
using namespace std;

// To store states of DP
int dp[max_arr_len][C_MAX + 1];

// To check if a state has
// been solved
bool v[max_arr_len][C_MAX + 1];

// Function to compute the states
int findMax(int i, int r, int w[], int n)
{

    // Base case
    if (r < 0)
        return INT_MIN;
    if (i == n)
        return 0;

    // Check if a state has
    // been solved
    if (v[i][r])
        return dp[i][r];

    // Setting a state as solved
    v[i][r] = 1;
    dp[i][r] = max(w[i] + findMax(i + 1, r - w[i], w, n),
                   findMax(i + 1, r, w, n));

    // Returning the solved state
    return dp[i][r];
}

// Function to pre-compute the states
// dp[0][0], dp[0][1], .., dp[0][C_MAX]
void preCompute(int w[], int n)
{
    for (int i = C_MAX; i >= 0; i--)
        findMax(0, i, w, n);
}

// Function to answer a query in O(1)
int ansQuery(int w)
{
    return dp[0][w];
}

// Driver code
int main()
{
    int w[] = { 3, 8, 9 };
    int n = sizeof(w) / sizeof(int);

    // Performing required
    // pre-computation
    preCompute(w, n);

    int queries[] = { 11, 10, 4 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++)
        cout << ansQuery(queries[i]) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int C_MAX = 30;
    static int max_arr_len = 10;

    // To store states of DP
    static int dp [][] = new int [max_arr_len][C_MAX + 1];

    // To check if a state has
    // been solved
    static boolean v[][]= new boolean [max_arr_len][C_MAX + 1];

    // Function to compute the states
    static int findMax(int i, int r, int w[], int n)
    {

        // Base case
        if (r < 0)
            return Integer.MIN_VALUE;
        if (i == n)
            return 0;

        // Check if a state has
        // been solved
        if (v[i][r])
            return dp[i][r];

        // Setting a state as solved
        v[i][r] = true;
        dp[i][r] = Math.max(w[i] + findMax(i + 1, r - w[i], w, n),
                                        findMax(i + 1, r, w, n));

        // Returning the solved state
        return dp[i][r];
    }

    // Function to pre-compute the states
    // dp[0][0], dp[0][1], .., dp[0][C_MAX]
    static void preCompute(int w[], int n)
    {
        for (int i = C_MAX; i >= 0; i--)
            findMax(0, i, w, n);
    }

    // Function to answer a query in O(1)
    static int ansQuery(int w)
    {
        return dp[0][w];
    }

    // Driver code
    public static void main (String[] args)
    {

        int w[] = new int []{ 3, 8, 9 };
        int n = w.length;

        // Performing required
        // pre-computation
        preCompute(w, n);

        int queries[] = new int [] { 11, 10, 4 };
        int q = queries.length;

        // Perform queries
        for (int i = 0; i < q; i++)
            System.out.println(ansQuery(queries[i]));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import numpy as np
import sys

C_MAX = 30
max_arr_len = 10

# To store states of DP
dp = np.zeros((max_arr_len,C_MAX + 1));

# To check if a state has
# been solved
v = np.zeros((max_arr_len,C_MAX + 1));

INT_MIN = -(sys.maxsize) + 1

# Function to compute the states
def findMax(i, r, w, n) :

    # Base case
    if (r < 0) :
        return INT_MIN;

    if (i == n) :
        return 0;

    # Check if a state has
    # been solved
    if (v[i][r]) :
        return dp[i][r];

    # Setting a state as solved
    v[i][r] = 1;
    dp[i][r] = max(w[i] + findMax(i + 1, r - w[i], w, n),
                findMax(i + 1, r, w, n));

    # Returning the solved state
    return dp[i][r];

# Function to pre-compute the states
# dp[0][0], dp[0][1], .., dp[0][C_MAX]
def preCompute(w, n) :

    for i in range(C_MAX, -1, -1) :
        findMax(0, i, w, n);

# Function to answer a query in O(1)
def ansQuery(w) :

    return dp[0][w];

# Driver code
if __name__ == "__main__" :

    w = [ 3, 8, 9 ];
    n = len(w)

    # Performing required
    # pre-computation
    preCompute(w, n);

    queries = [ 11, 10, 4 ];
    q = len(queries)

    # Perform queries
    for i in range(q) :
        print(ansQuery(queries[i]));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int C_MAX = 30;
    static int max_arr_len = 10;

    // To store states of DP
    static int[,] dp  = new int [max_arr_len, C_MAX + 1];

    // To check if a state has
    // been solved
    static bool[,] v = new bool [max_arr_len, C_MAX + 1];

    // Function to compute the states
    static int findMax(int i, int r, int[] w, int n)
    {

        // Base case
        if (r < 0)
            return Int32.MaxValue;
        if (i == n)
            return 0;

        // Check if a state has
        // been solved
        if (v[i, r])
            return dp[i, r];

        // Setting a state as solved
        v[i, r] = true;
        dp[i, r] = Math.Max(w[i] + findMax(i + 1, r - w[i], w, n),
                                        findMax(i + 1, r, w, n));

        // Returning the solved state
        return dp[i, r];
    }

    // Function to pre-compute the states
    // dp[0][0], dp[0][1], .., dp[0][C_MAX]
    static void preCompute(int[] w, int n)
    {
        for (int i = C_MAX; i >= 0; i--)
            findMax(0, i, w, n);
    }

    // Function to answer a query in O(1)
    static int ansQuery(int w)
    {
        return dp[0, w];
    }

    // Driver code
    public static void Main()
    {
        int[] w= { 3, 8, 9 };
        int n = w.Length;

        // Performing required
        // pre-computation
        preCompute(w, n);

        int[] queries = { 11, 10, 4 };
        int q = queries.Length;

        // Perform queries
        for (int i = 0; i < q; i++)
            Console.WriteLine(ansQuery(queries[i]));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var C_MAX = 30
var max_arr_len = 10

// To store states of DP
var dp = Array.from(Array(max_arr_len), ()=>Array(C_MAX+1));

// To check if a state has
// been solved
var v = Array.from(Array(max_arr_len), ()=>Array(C_MAX+1));

// Function to compute the states
function findMax(i, r, w, n)
{

    // Base case
    if (r < 0)
        return -1000000000;
    if (i == n)
        return 0;

    // Check if a state has
    // been solved
    if (v[i][r])
        return dp[i][r];

    // Setting a state as solved
    v[i][r] = 1;
    dp[i][r] = Math.max(w[i] + findMax(i + 1, r - w[i], w, n),
                   findMax(i + 1, r, w, n));

    // Returning the solved state
    return dp[i][r];
}

// Function to pre-compute the states
// dp[0][0], dp[0][1], .., dp[0][C_MAX]
function preCompute(w, n)
{
    for (var i = C_MAX; i >= 0; i--)
        findMax(0, i, w, n);
}

// Function to answer a query in O(1)
function ansQuery(w)
{
    return dp[0][w];
}

// Driver code
var w = [3, 8, 9];
var n = w.length;
// Performing required
// pre-computation
preCompute(w, n);
var queries = [11, 10, 4];
var q = queries.length;
// Perform queries
for (var i = 0; i < q; i++)
    document.write( ansQuery(queries[i])+ "<br>");

</script>
```

**Output:** 

```
11
9
3
```