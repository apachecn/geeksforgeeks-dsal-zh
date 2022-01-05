# N 根连续绳问题

> 原文:[https://www.geeksforgeeks.org/n-consecutive-ropes-problem/](https://www.geeksforgeeks.org/n-consecutive-ropes-problem/)

给定 **N** 根绳子，每根绳子都有一个相关的长度。一次，只有两个连续的小绳子末端绑在一起形成一个大绳子，形成它们长度的总和的成本。当所有的绳子都绑在一起形成一根绳子时，找到最小的成本。

**示例:**

> **输入:** arr[] = {7，6，8，6，1，1}
> **输出:** 68
> {7，6，8，6， **1，1**}–{ 7，6，8，6，2}，成本= 2
> {7，6，8， **6，2**}–{ 7，6，8，8}，成本= 8
> { **7，6** 成本= 16
> { **13，16**}–{ 29 }，成本= 29
> 2 + 8 + 13 + 16 + 29 = 68
> 
> **输入:** arr[] = {10，20，30，40 }
> T3】输出: 190

**方法:**在[这篇](https://www.geeksforgeeks.org/connect-n-ropes-minimum-cost/)文章中已经讨论过类似的问题，其中任何两条绳索都可以连接，但是在这个问题中，只有连续的绳索可以连接。这个问题可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的[矩阵链乘法](https://www.geeksforgeeks.org/matrix-chain-multiplication-dp-8/)技术来解决。

**最优子结构:**在第二个例子中，绳索可以连接为(((10 + 20) + 30) + 40)
连接 10 和 20；成本= 30；表达式变为((30 + 30) + 40)
连接 30 和 30；成本= 90；表达式变成(60 + 40)
连接 60 和 40；成本= 190，我们得到一根绳子
一个简单的解决方案是在所有可能的地方放置括号，然后计算每个部分的成本，并合计总成本。对于所有有效的括号序列都可以这样做，最小值就是答案。

> 给定长度为 r1、r2、r3 和 r4 的绳索。
> 连接可以通过以下方式形成:
> ((R1+R2)+R3+R4)或
> ((r1 + (r2 + r3)) + r4)或
> ((R1+R2)+(R3+R4))……
> 第一种方式的总成本为= r4 + 2 * r3 + 3 * (r2 + r1)

所以当括号集合被放置时，问题被分成更小规模的子问题。因此，该问题具有最优子结构性质，易于用递归方法求解。

**重叠子问题**

> (((r1 + r2) + r3) + r4)
> 和
> ((r1 + r2) + (r3 + r4))
> 都有一个共同的部分，即(r1 + r2)

所以解决方案如下:

*   预计算不同区间的和，节省计算时间。
*   如果我们希望连接{arr[i] arr[i+1] …arr[k]}和{arr[k+1] arr[k+2] …arr[j]}的两个部分，那么我们的成本将是

> MinCost(i，k) + MinCost(k + 1，j) + sum(arr[i]到 arr[j])

*   其中，MinCost(i，k) =范围(I，k)内的最小成本和总和(arr[i]至 arr[j]) =连接(I，k)和(k + 1，j)的绳索段的成本。我们可以将子问题存储在 dp 表中，以节省计算时间。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
// to connect the given ropes
int MinCost(int arr[], int n)
{

    // dp[i][j] = minimum cost in range (i, j)
    // sum[i][j] = sum of range (i, j)
    int dp[n + 5][n + 5], sum[n + 5][n + 5];

    // Initializing the sum table
    memset(sum, 0, sizeof(0));
    for (int i = 0; i < n; i++) {
        int k = arr[i];
        for (int j = i; j < n; j++) {
            if (i == j)
                sum[i][j] = k;
            else {
                k += arr[j];
                sum[i][j] = k;
            }
        }
    }

    // Computing minimum cost for all
    // the possible interval (i, j)
    // Left range
    for (int i = n - 1; i >= 0; i--) {

        // Right range
        for (int j = i; j < n; j++) {
            dp[i][j] = INT_MAX;

            // No cost for a single rope
            if (i == j)
                dp[i][j] = 0;
            else {
                for (int k = i; k < j; k++) {
                    dp[i][j] = min(dp[i][j],
                                   dp[i][k] + dp[k + 1][j]
                                       + sum[i][j]);
                }
            }
        }
    }

    return dp[0][n - 1];
}

// Driver code
int main()
{
    int arr[] = { 7, 6, 8, 6, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << MinCost(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum cost
// to connect the given ropes
static int MinCost(int arr[], int n)
{

    // dp[i][j] = minimum cost in range (i, j)
    // sum[i][j] = sum of range (i, j)
    int [][]dp = new int[n + 5][n + 5];
    int [][]sum = new int[n + 5][n + 5];

    // Initializing the sum table
    //memset(sum, 0, sizeof(0));
    for (int i = 0; i < n; i++)
    {
        int k = arr[i];
        for (int j = i; j < n; j++)
        {
            if (i == j)
                sum[i][j] = k;
            else
            {
                k += arr[j];
                sum[i][j] = k;
            }
        }
    }

    // Computing minimum cost for all
    // the possible interval (i, j)
    // Left range
    for (int i = n - 1; i >= 0; i--)
    {

        // Right range
        for (int j = i; j < n; j++)
        {
            dp[i][j] = Integer.MAX_VALUE;

            // No cost for a single rope
            if (i == j)
                dp[i][j] = 0;
            else
            {
                for (int k = i; k < j; k++)
                {
                    dp[i][j] = Math.min(dp[i][j],
                                        dp[i][k] +
                                        dp[k + 1][j] +
                                        sum[i][j]);
                }
            }
        }
    }
    return dp[0][n - 1];
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 7, 6, 8, 6, 1, 1 };
    int n = arr.length;

    System.out.println(MinCost(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cost
# to connect the given ropes
def MinCost(arr, n):

    # dp[i][j] = minimum cost in range (i, j)
    # sum[i][j] = sum of range (i, j)
    dp = [[0 for i in range(n + 5)]
             for i in range(n + 5)]
    sum = [[0 for i in range(n + 5)]
              for i in range(n + 5)]

    for i in range(n):
        k = arr[i]
        for j in range(i, n):
            if (i == j):
                sum[i][j] = k
            else:
                k += arr[j]
                sum[i][j] = k

    # Computing minimum cost for all
    # the possible interval (i, j)
    # Left range
    for i in range(n - 1, -1, -1):

        # Right range
        for j in range(i, n):
            dp[i][j] = 10**9

            # No cost for a single rope
            if (i == j):
                dp[i][j] = 0
            else :
                for k in range(i, j):
                    dp[i][j] = min(dp[i][j], dp[i][k] +    
                                   dp[k + 1][j] + sum[i][j])

    return dp[0][n - 1]

# Driver code
arr = [7, 6, 8, 6, 1, 1]
n = len(arr)

print(MinCost(arr, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum cost
// to connect the given ropes
static int MinCost(int []arr, int n)
{

    // dp[i,j] = minimum cost in range (i, j)
    // sum[i,j] = sum of range (i, j)
    int [,]dp = new int[n + 5, n + 5];
    int [,]sum = new int[n + 5, n + 5];

    // Initializing the sum table
    //memset(sum, 0, sizeof(0));
    for (int i = 0; i < n; i++)
    {
        int k = arr[i];
        for (int j = i; j < n; j++)
        {
            if (i == j)
                sum[i, j] = k;
            else
            {
                k += arr[j];
                sum[i, j] = k;
            }
        }
    }

    // Computing minimum cost for all
    // the possible interval (i, j)
    // Left range
    for (int i = n - 1; i >= 0; i--)
    {

        // Right range
        for (int j = i; j < n; j++)
        {
            dp[i, j] = int.MaxValue;

            // No cost for a single rope
            if (i == j)
                dp[i, j] = 0;
            else
            {
                for (int k = i; k < j; k++)
                {
                    dp[i, j] = Math.Min(dp[i, j],
                                        dp[i, k] +
                                        dp[k + 1, j] +
                                        sum[i, j]);
                }
            }
        }
    }
    return dp[0, n - 1];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 7, 6, 8, 6, 1, 1 };
    int n = arr.Length;

    Console.WriteLine(MinCost(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum cost
// to connect the given ropes
function MinCost(arr, n) {

    // dp[i][j] = minimum cost in range (i, j)
    // sum[i][j] = sum of range (i, j)
    let dp = new Array(n + 5);
    let sum = new Array(n + 5);

    for (let i = 0; i < n + 5; i++) {
        dp[i] = [];
        sum[i] = [];
        for (let j = 0; j < n + 5; j++) {
            dp[i].push(0)
            sum[i].push(0)
        }

    }

console.log(dp)
    for (let i = 0; i < n; i++)
    {
        let k = arr[i];
        for (let j = i; j < n; j++)
        {
            if (i == j)
                sum[i][j] = k;
            else
            {
                k += arr[j];
                sum[i][j] = k;
            }
        }
    }

    // Computing minimum cost for all
    // the possible interval (i, j)
    // Left range
    for (let i = n - 1; i >= 0; i--)
    {

        // Right range
        for (let j = i; j < n; j++)
        {
            dp[i][j] = Number.MAX_SAFE_INTEGER;

            // No cost for a single rope
            if (i == j)
                dp[i][j] = 0;
            else
            {
                for (let k = i; k < j; k++)
                {
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + 
                    dp[k + 1][j] +  sum[i][j]);
                }
            }
        }
    }
    return dp[0][n - 1];
}

// Driver code

let arr = [7, 6, 8, 6, 1, 1];
let n = arr.length;

document.write(MinCost(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
68
```