# 所有顶点度数之和为 L 的树的个数

> 原文:[https://www . geesforgeks . org/树的数量-其所有顶点的度数之和为-l/](https://www.geeksforgeeks.org/number-of-trees-whose-sum-of-degrees-of-all-the-vertices-is-l/)

给定一个整数 **L** ，它是某棵树所有顶点的度数之和。任务是找到所有这些不同的树(标记树)的计数。如果两棵树至少有一条不同的边，它们就是不同的。
**例:**

> **输入:** L = 2
> **输出:** 1
> **输入:** L = 6
> **输出:** 16

**简单解法**:简单解法就是求所有顶点度数之和为 **L** 的树的节点数。这种树的节点数为 **n = (L / 2 + 1)** ，如[这篇](https://www.geeksforgeeks.org/sum-of-degrees-of-all-nodes-of-a-undirected-graph/)文章所述。
现在的解决方案是形成所有可以使用 n 个节点形成的标记树。这种方法相当复杂，对于较大的 n 值，使用这种方法不可能找出树的数量。
**高效解**:高效解是利用[凯莱公式](https://en.wikipedia.org/wiki/Cayley%27s_formula)求节点数，该公式说明有**n<sup>(n–2)</sup>**棵树有 n 个标记顶点。所以现在代码的时间复杂度降低到 **O(n)** ，使用模幂运算可以进一步降低到 **O(logn)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;
#define ll long long int

// Iterative Function to calculate (x^y) in O(log y)
ll power(int x, ll y)
{

    // Initialize result
    ll res = 1;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x);

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x);
    }
    return res;
}

// Function to return the count
// of required trees
ll solve(int L)
{
    // number of nodes
    int n = L / 2 + 1;

    ll ans = power(n, n - 2);

    // Return the result
    return ans;
}

// Driver code
int main()
{
    int L = 6;

    cout << solve(L);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Iterative Function to calculate (x^y) in O(log y)
static long power(int x, long y)
{

    // Initialize result
    long res = 1;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y==1)
            res = (res * x);

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x);
    }
    return res;
}

// Function to return the count
// of required trees
static long solve(int L)
{
    // number of nodes
    int n = L / 2 + 1;

    long ans = power(n, n - 2);

    // Return the result
    return ans;
}

// Driver code
public static void main (String[] args)
{

    int L = 6;
    System.out.println (solve(L));
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```

# Python implementation of the approach

# Iterative Function to calculate (x^y) in O(log y)
def power(x, y):

    # Initialize result
    res = 1;

    while (y > 0):

        # If y is odd, multiply x with result
        if (y %2== 1):
            res = (res * x);

        # y must be even now
        #y = y / 2
        y = int(y) >> 1;
        x = (x * x);
    return res;

# Function to return the count
# of required trees
def solve(L):

    # number of nodes
    n = L / 2 + 1;

    ans = power(n, n - 2);

    # Return the result
    return int(ans);

L = 6;
print(solve(L));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Iterative Function to calculate (x^y) in O(log y)
static long power(int x, long y)
{

    // Initialize result
    long res = 1;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y == 1)
            res = (res * x);

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x);
    }
    return res;
}

// Function to return the count
// of required trees
static long solve(int L)
{
    // number of nodes
    int n = L / 2 + 1;

    long ans = power(n, n - 2);

    // Return the result
    return ans;
}

// Driver code
static public void Main ()
{
    int L = 6;
    Console.WriteLine(solve(L));
}
}

// This code is contributed by Tushil.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Iterative Function to calculate (x^y) in O(log y)
function power(x, y)
{

    // Initialize result
    var res = 1;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x);

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x);
    }
    return res;
}

// Function to return the count
// of required trees
function solve(L)
{
    // number of nodes
    var n = L / 2 + 1;

    var ans = power(n, n - 2);

    // Return the result
    return ans;
}

// Driver code
var L = 6;
document.write( solve(L));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
16
```