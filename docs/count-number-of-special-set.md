# 统计特殊设置的数量

> 原文:[https://www.geeksforgeeks.org/count-number-of-special-set/](https://www.geeksforgeeks.org/count-number-of-special-set/)

如果对于集合 **X** 的每个元素，该集合不包含元素 **X + 1** ，则有序整数集合被称为特殊集合。给定一个整数 **N** ，任务是找出最大元素不大于 **N** 的特殊集合的个数。既然，特殊集的数量可以很大，打印答案模 **10 <sup>9 + 7</sup>** 。

**示例:**

> **输入:** N = 3
> **输出:** 5
> {1}、{2}、{3}、{1，3}和{3，1}是
> 唯一可能的特殊设置。
> 
> **输入:**N = 4
> T3】输出: 10

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。创建一个数组 **dp[][]** ，其中 **dp[i][j]** 存储以 **j** 结尾的特殊长度组 **i** 的数量。现在，循环关系将是:

> DP[I][j]= DP[I–1][1]+DP[I–1][2]+…+DP[I–1][j–2]
> DP[I][j]可以在 O(1)中通过取前一个 DP[I–1]的前缀和一次来计算。

现在尺寸 **i** 的总特殊组可以通过将**DP【I】【n】**乘以**阶乘(i)** 来计算。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

const int MAX = 2 * 1000 + 10;
const int MOD = 1e9 + 7;

// To store the states of the dp
ll dp[MAX][MAX];

// Function to return (a + b) % MOD
ll sum(ll a, ll b)
{
    return ((a % MOD) + (b % MOD)) % MOD;
}

// Function to return (a * b) % MOD
ll mul(ll a, ll b)
{
    return ((a % MOD) * (b % MOD)) % MOD;
}

// Function to return the count
// of special sets
int cntSpecialSet(int n)
{

    // Fill the dp[][] array with the answer
    // for the special sets of size 1
    for (int i = 1; i <= n; i++) {
        dp[1][i] = 1;

        // Take prefix sum of the current row which
        // will be used to fill the next row
        dp[1][i] += dp[1][i - 1];
    }

    // Fill the rest of the dp[][] array
    for (int i = 2; i <= n; i++) {

        // Recurrence relation
        for (int j = 2; j <= n; j++) {
            dp[i][j] = dp[i - 1][j - 2];
        }

        // Calculate the prefix sum
        for (int j = 1; j <= n; j++) {
            dp[i][j] = sum(dp[i][j], dp[i][j - 1]);
        }
    }

    ll ways(1), ans(0);

    for (int i = 1; i <= n; i++) {

        // To find special set of size i
        ways = mul(ways, i);

        // Addition of special sets of all sizes
        ans = sum(ans, mul(ways, dp[i][n]));
    }

    return ans;
}

// Driver code
int main()
{
    int n = 3;

    cout << cntSpecialSet(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG 
{
static int MAX = 2 * 1000 + 10;
static int MOD = (int) (1e9 + 7);

// To store the states of the dp
static long [][]dp = new long[MAX][MAX];

// Function to return (a + b) % MOD
static long sum(long a, long b)
{
    return ((a % MOD) + (b % MOD)) % MOD;
}

// Function to return (a * b) % MOD
static long mul(long a, long b)
{
    return ((a % MOD) * (b % MOD)) % MOD;
}

// Function to return the count
// of special sets
static long cntSpecialSet(int n)
{

    // Fill the dp[][] array with the answer
    // for the special sets of size 1
    for (int i = 1; i <= n; i++) 
    {
        dp[1][i] = 1;

        // Take prefix sum of the current row which
        // will be used to fill the next row
        dp[1][i] += dp[1][i - 1];
    }

    // Fill the rest of the dp[][] array
    for (int i = 2; i <= n; i++) 
    {

        // Recurrence relation
        for (int j = 2; j <= n; j++) 
        {
            dp[i][j] = dp[i - 1][j - 2];
        }

        // Calculate the prefix sum
        for (int j = 1; j <= n; j++) 
        {
            dp[i][j] = sum(dp[i][j], dp[i][j - 1]);
        }
    }

    long ways = 1, ans = 0;

    for (int i = 1; i <= n; i++) 
    {

        // To find special set of size i
        ways = mul(ways, i);

        // Addition of special sets of all sizes
        ans = sum(ans, mul(ways, dp[i][n]));
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(cntSpecialSet(n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the nodes having 
# maximum and minimum degree 
def minMax(edges, leng, n) : 

    # Map to store the degrees of every node 
    m = {};

    for i in range(leng) :
        m[edges[i][0]] = 0;
        m[edges[i][1]] = 0;

    for i in range(leng) :

        # Storing the degree for each node
        m[edges[i][0]] += 1;
        m[edges[i][1]] += 1; 

    # maxi and mini variables to store 
    # the maximum and minimum degree 
    maxi = 0; 
    mini = n; 

    for i in range(1, n + 1) :
        maxi = max(maxi, m[i]); 
        mini = min(mini, m[i]); 

    # Printing all the nodes 
    # with maximum degree 
    print("Nodes with maximum degree : ", 
                                end = "")

    for i in range(1, n + 1) :
        if (m[i] == maxi) :
            print(i, end = " "); 

    print()

    # Printing all the nodes 
    # with minimum degree 
    print("Nodes with minimum degree : ", 
                                end = "")

    for i in range(1, n + 1) :
        if (m[i] == mini) :
            print(i, end = " "); 

# Driver code 
if __name__ == "__main__" : 

    # Count of nodes and edges 
    n = 4; m = 6; 

    # The edge list 
    edges = [[ 1, 2 ], [ 1, 3 ], 
             [ 1, 4 ], [ 2, 3 ], 
             [ 2, 4 ], [ 3, 4 ]]; 

    minMax(edges, m, 4); 

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG 
{

static int MAX = 2 * 1000 + 10;
static int MOD = (int) (1e9 + 7);

// To store the states of the dp
static long [,]dp = new long[MAX, MAX];

// Function to return (a + b) % MOD
static long sum(long a, long b)
{
    return ((a % MOD) + (b % MOD)) % MOD;
}

// Function to return (a * b) % MOD
static long mul(long a, long b)
{
    return ((a % MOD) * (b % MOD)) % MOD;
}

// Function to return the count
// of special sets
static long cntSpecialSet(int n)
{

    // Fill the dp[,] array with the answer
    // for the special sets of size 1
    for (int i = 1; i <= n; i++) 
    {
        dp[1, i] = 1;

        // Take prefix sum of the current row which
        // will be used to fill the next row
        dp[1, i] += dp[1, i - 1];
    }

    // Fill the rest of the dp[,] array
    for (int i = 2; i <= n; i++) 
    {

        // Recurrence relation
        for (int j = 2; j <= n; j++) 
        {
            dp[i, j] = dp[i - 1, j - 2];
        }

        // Calculate the prefix sum
        for (int j = 1; j <= n; j++) 
        {
            dp[i, j] = sum(dp[i, j], dp[i, j - 1]);
        } 
    }

    long ways = 1, ans = 0;

    for (int i = 1; i <= n; i++) 
    {

        // To find special set of size i
        ways = mul(ways, i);

        // Addition of special sets of all sizes
        ans = sum(ans, mul(ways, dp[i, n]));
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(cntSpecialSet(n));
}
}

// This code is contributed by Princi Singh
```

**Output:**

```
5

```