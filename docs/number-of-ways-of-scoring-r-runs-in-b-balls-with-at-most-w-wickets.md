# 最多有 W 个检票口的 B 球 R 跑得分方式数

> 原文:[https://www . geeksforgeeks . org/得分方式数-r-run-in-b-balls-at-w-wickets/](https://www.geeksforgeeks.org/number-of-ways-of-scoring-r-runs-in-b-balls-with-at-most-w-wickets/)

给定三个整数 **R** 、 **B** 和 **W** ，表示**运行**、**球**和**检票口**的数量。在板球比赛中，一个人可以在单个球中得分 **0、1、2、3、4、6** 或**一个小门**。任务是计算一个团队可以精确得分的方式数量 **R 跑**在精确的 **B 球**中最多有 **W 个检票口**。由于途径数量较多，打印答案时取模 **1000000007** 。
**举例:**

> **输入:** R = 4，B = 2，W = 2
> **输出:**7
> 7 路为:
> 0，4
> 4，0
> Wicket，4
> 4，Wicket
> 1，3
> 3，1
> 2，2
> **输入:** R = 40，B = 10，W = 4
> **输出:**

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)可以解决问题。循环将有 6 种状态，我们最初从**运行= 0** 、**球= 0** 和**检票口= 0** 开始。状态将为:

*   如果一个队在一个球上得了 **1 分**，那么**跑=跑+ 1** 和**球=球+ 1** 。
*   如果一个队在一个球上得了 **2 分**，那么**跑=跑+ 2** 和**球=球+ 1** 。
*   如果一个队在一个球上得了 **3 分**，那么**跑=跑+ 3** 和**球=球+ 1** 。
*   如果一个队在一个球上得了 **4 分**，那么**跑=跑+ 4** 和**球=球+ 1** 。
*   如果一个队在一个球上得了 **6 分**，那么**跑=跑+ 6** 和**球=球+ 1** 。
*   如果一个队在一个球上得分**不跑**，那么**跑=跑**和**球=球+ 1** 。
*   如果一个队**在一个球**上失去了 1 个小门，那么**跑=跑**和**球=球+ 1 个**和**小门=小门+ 1 个**。

DP 将由三种状态组成，运行状态最大为 **6 *球**，因为这是最大可能。因此**DP【I】【j】【k】**表示 **i 跑**的次数可以精确地在 **j 球**中得分，同时失去 **k 个检票口**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007
#define RUNMAX 300
#define BALLMAX 50
#define WICKETMAX 10

// Function to return the number of ways
// to score R runs in B balls with
// at most W wickets
int CountWays(int r, int b, int l, int R, int B, int W,
              int dp[RUNMAX][BALLMAX][WICKETMAX])
{

    // If the wickets lost are more
    if (l > W)
        return 0;

    // If runs scored are more
    if (r > R)
        return 0;

    // If condition is met
    if (b == B && r == R)
        return 1;

    // If no run got scored
    if (b == B)
        return 0;

    // Already visited state
    if (dp[r][b][l] != -1)
        return dp[r][b][l];

    int ans = 0;

    // If scored 0 run
    ans += CountWays(r, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 1 run
    ans += CountWays(r + 1, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 2 runs
    ans += CountWays(r + 2, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 3 runs
    ans += CountWays(r + 3, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 4 runs
    ans += CountWays(r + 4, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 6 runs
    ans += CountWays(r + 6, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored no run and lost a wicket
    ans += CountWays(r, b + 1, l + 1, R, B, W, dp);
    ans = ans % mod;

    // Memoize and return
    return dp[r][b][l] = ans;
}

// Driver code
int main()
{
    int R = 40, B = 10, W = 4;

    int dp[RUNMAX][BALLMAX][WICKETMAX];
    memset(dp, -1, sizeof dp);

    cout << CountWays(0, 0, 0, R, B, W, dp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static int mod = 1000000007;
static int RUNMAX = 300;
static int BALLMAX = 50;
static int WICKETMAX = 10;

// Function to return the number of ways
// to score R runs in B balls with
// at most W wickets
static int CountWays(int r, int b, int l,
                    int R, int B, int W,
                            int [][][]dp)
{

    // If the wickets lost are more
    if (l > W)
        return 0;

    // If runs scored are more
    if (r > R)
        return 0;

    // If condition is met
    if (b == B && r == R)
        return 1;

    // If no run got scored
    if (b == B)
        return 0;

    // Already visited state
    if (dp[r][b][l] != -1)
        return dp[r][b][l];

    int ans = 0;

    // If scored 0 run
    ans += CountWays(r, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 1 run
    ans += CountWays(r + 1, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 2 runs
    ans += CountWays(r + 2, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 3 runs
    ans += CountWays(r + 3, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 4 runs
    ans += CountWays(r + 4, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 6 runs
    ans += CountWays(r + 6, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored no run and lost a wicket
    ans += CountWays(r, b + 1, l + 1, R, B, W, dp);
    ans = ans % mod;

    // Memoize and return
    return dp[r][b][l] = ans;
}

// Driver code
public static void main(String[] args)
{
    int R = 40, B = 10, W = 4;

    int[][][] dp = new int[RUNMAX][BALLMAX][WICKETMAX];
    for(int i = 0; i < RUNMAX;i++)
        for(int j = 0; j < BALLMAX; j++)
            for(int k = 0; k < WICKETMAX; k++)
    dp[i][j][k]=-1;

    System.out.println(CountWays(0, 0, 0, R, B, W, dp));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 1000000007
RUNMAX = 300
BALLMAX = 50
WICKETMAX = 10

# Function to return the number of ways
# to score R runs in B balls with
# at most W wickets
def CountWays(r, b, l, R, B, W, dp):

    # If the wickets lost are more
    if (l > W):
        return 0;

    # If runs scored are more
    if (r > R):
        return 0;

    # If condition is met
    if (b == B and r == R):
        return 1;

    # If no run got scored
    if (b == B):
        return 0;

    # Already visited state
    if (dp[r][b][l] != -1):
        return dp[r][b][l]

    ans = 0;

    # If scored 0 run
    ans += CountWays(r, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored 1 run
    ans += CountWays(r + 1, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored 2 runs
    ans += CountWays(r + 2, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored 3 runs
    ans += CountWays(r + 3, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored 4 runs
    ans += CountWays(r + 4, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored 6 runs
    ans += CountWays(r + 6, b + 1, l,
                     R, B, W, dp);
    ans = ans % mod;

    # If scored no run and lost a wicket
    ans += CountWays(r, b + 1, l + 1,
                     R, B, W, dp);
    ans = ans % mod;

    # Memoize and return
    dp[r][b][l] = ans

    return ans;

# Driver code   
if __name__=="__main__":

    R = 40
    B = 10
    W = 40

    dp = [[[-1 for k in range(WICKETMAX)]
               for j in range(BALLMAX)]
               for i in range(RUNMAX)]

    print(CountWays(0, 0, 0, R, B, W, dp))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

static int mod = 1000000007;
static int RUNMAX = 300;
static int BALLMAX = 50;
static int WICKETMAX = 10;

// Function to return the number of ways
// to score R runs in B balls with
// at most W wickets
static int CountWays(int r, int b, int l,
                    int R, int B, int W,
                            int [,,]dp)
{

    // If the wickets lost are more
    if (l > W)
        return 0;

    // If runs scored are more
    if (r > R)
        return 0;

    // If condition is met
    if (b == B && r == R)
        return 1;

    // If no run got scored
    if (b == B)
        return 0;

    // Already visited state
    if (dp[r, b, l] != -1)
        return dp[r, b, l];

    int ans = 0;

    // If scored 0 run
    ans += CountWays(r, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 1 run
    ans += CountWays(r + 1, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 2 runs
    ans += CountWays(r + 2, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 3 runs
    ans += CountWays(r + 3, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 4 runs
    ans += CountWays(r + 4, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored 6 runs
    ans += CountWays(r + 6, b + 1, l, R, B, W, dp);
    ans = ans % mod;

    // If scored no run and lost a wicket
    ans += CountWays(r, b + 1, l + 1, R, B, W, dp);
    ans = ans % mod;

    // Memoize and return
    return dp[r, b, l] = ans;
}

// Driver code
static void Main()
{
    int R = 40, B = 10, W = 4;

    int[,,] dp = new int[RUNMAX, BALLMAX, WICKETMAX];
    for(int i = 0; i < RUNMAX;i++)
        for(int j = 0; j < BALLMAX; j++)
            for(int k = 0; k < WICKETMAX; k++)
    dp[i, j, k]=-1;

    Console.WriteLine(CountWays(0, 0, 0, R, B, W, dp));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    var mod = 1000000007;
    var RUNMAX = 300;
    var BALLMAX = 50;
    var WICKETMAX = 10;

    // Function to return the number of ways
    // to score R runs in B balls with
    // at most W wickets
    function CountWays(r , b , l , R , B , W,  dp) {

        // If the wickets lost are more
        if (l > W)
            return 0;

        // If runs scored are more
        if (r > R)
            return 0;

        // If condition is met
        if (b == B && r == R)
            return 1;

        // If no run got scored
        if (b == B)
            return 0;

        // Already visited state
        if (dp[r][b][l] != -1)
            return dp[r][b][l];

        var ans = 0;

        // If scored 0 run
        ans += CountWays(r, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored 1 run
        ans += CountWays(r + 1, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored 2 runs
        ans += CountWays(r + 2, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored 3 runs
        ans += CountWays(r + 3, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored 4 runs
        ans += CountWays(r + 4, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored 6 runs
        ans += CountWays(r + 6, b + 1, l, R, B, W, dp);
        ans = ans % mod;

        // If scored no run and lost a wicket
        ans += CountWays(r, b + 1, l + 1, R, B, W, dp);
        ans = ans % mod;

        // Memoize and return
        return dp[r][b][l] = ans;
    }

    // Driver code   
        var R = 40, B = 10, W = 4;

        var dp = Array(RUNMAX).fill().map(()=>Array(BALLMAX).fill().map(()=>Array(WICKETMAX).fill(0)));
        for (i = 0; i < RUNMAX; i++)
            for (j = 0; j < BALLMAX; j++)
                for (k = 0; k < WICKETMAX; k++)
                    dp[i][j][k] = -1;

        document.write(CountWays(0, 0, 0, R, B, W, dp));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
653263
```