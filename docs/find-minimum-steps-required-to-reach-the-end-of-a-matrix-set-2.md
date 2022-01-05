# 找到到达矩阵末端所需的最小步数|设置 2

> 原文:[https://www . geesforgeks . org/find-到达矩阵集末尾所需的最少步骤-2/](https://www.geeksforgeeks.org/find-minimum-steps-required-to-reach-the-end-of-a-matrix-set-2/)

给定一个由正整数组成的 2d 矩阵，任务是找到到达矩阵末端所需的最小步数。如果我们在单元格 **(i，j)** 处，那么我们可以转到由 **(i + X，j + Y)** 表示的所有单元格，使得 **X ≥ 0** 、 **Y ≥ 0** 和 **X + Y = arr[i][j]** 。如果没有路径，则打印 **-1** 。
**示例:**

> **输入:** arr[][] = {
> {4，1，1}，
> {1，1，1}，
> {1，1，1}}
> **输出:** 1
> 路径将从{0，0} - > {2，2}作为曼哈顿两者之间的距离
> 为 4。
> 因此，我们一步到位。
> **输入:** arr[][] = {
> {1，1，2}，
> {1，1，1}，
> {2，1，1}}
> **输出:** 3

一个简单的解决方案是探索所有可能的解决方案，这需要指数时间。
一个**高效的解决方案**就是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)在多项式时间内解决这个问题。让我们决定 dp 的状态。
假设我们在细胞 **(i，j)** 。我们将尝试找到从该单元格到达单元格**(n–1，n–1)**所需的最小步数。
我们有 **arr[i][j] + 1** 条可能的路径。
递归关系为

> DP[I][j]= 1+min(DP[I][j+arr[I][j]]DP[I+1][j+arr[I][j]-1]，……。，DP[I+arr[I][j]][j]]

为了减少递归关系中的项数，我们可以对 **X** 和 **Y** 的值设置一个上限。怎么做？
我们知道 **i + X < N** 。因此，**X<N–I**否则他们会出界。
同样，**Y<N–j**

> **0≤Y<N–j**……(1)
> **X+Y = arr[I][j]**……(2)
> 将 **Y** 的值从第二位代入第一位，我们得到
> **X≥arr[I][j]+j–N+1**

由此我们得到了另一个关于 **X** 约束的下界，即**X≥arr[I][j]+j–N+1**。
于是， **X** 上的新下界变为 **X ≥ max(0，arr[I][j]+j–N+1)**。
同样 **X ≤ min(arr[i][j]，N–I–1)**。
我们的复发关系优化至

> dp[i][j] = 1 + min(dp[i + max(0，arr[I][j]+j-n+1)][j+arr[I][j]-max(0，arr[I][j]+j-n+1)]，……。，dp[i + min(arr[i][j]，n-I–1)][j+arr[I][j]-min(arr[I][j]，n-I–1)]]t0]

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define n 3
using namespace std;

// 2d array to store
// states of dp
int dp[n][n];

// Array to determine whether
// a state has been solved before
int v[n][n];

// Function to return the minimum steps required
int minSteps(int i, int j, int arr[][n])
{

    // Base cases
    if (i == n - 1 and j == n - 1)
        return 0;

    if (i > n - 1 || j > n - 1)
        return 9999999;

    // If a state has been solved before
    // it won't be evaluated again
    if (v[i][j])
        return dp[i][j];

    v[i][j] = 1;
    dp[i][j] = 9999999;

    // Recurrence relation
    for (int k = max(0, arr[i][j] + j - n + 1);
         k <= min(n - i - 1, arr[i][j]); k++) {
        dp[i][j] = min(dp[i][j], minSteps(i + k, j + arr[i][j] - k, arr));
    }

    dp[i][j]++;

    return dp[i][j];
}

// Driver code
int main()
{
    int arr[n][n] = { { 4, 1, 2 },
                      { 1, 1, 1 },
                      { 2, 1, 1 } };

    int ans = minSteps(0, 0, arr);
    if (ans >= 9999999)
        cout << -1;
    else
        cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int n = 3;

    // 2d array to store
    // states of dp
    static int[][] dp = new int[n][n];

    // Array to determine whether
    // a state has been solved before
    static int[][] v = new int[n][n];

    // Function to return the minimum steps required
    static int minSteps(int i, int j, int arr[][])
    {

        // Base cases
        if (i == n - 1 && j == n - 1) {
            return 0;
        }

        if (i > n - 1 || j > n - 1) {
            return 9999999;
        }

        // If a state has been solved before
        // it won't be evaluated again
        if (v[i][j] == 1) {
            return dp[i][j];
        }

        v[i][j] = 1;
        dp[i][j] = 9999999;

        // Recurrence relation
        for (int k = Math.max(0, arr[i][j] + j - n + 1);
             k <= Math.min(n - i - 1, arr[i][j]); k++) {
            dp[i][j] = Math.min(dp[i][j],
                                minSteps(i + k, j + arr[i][j] - k, arr));
        }

        dp[i][j]++;

        return dp[i][j];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[][] = { { 4, 1, 2 },
                        { 1, 1, 1 },
                        { 2, 1, 1 } };

        int ans = minSteps(0, 0, arr);
        if (ans >= 9999999) {
            System.out.println(-1);
        }
        else {
            System.out.println(ans);
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import numpy as np
n = 3

# 2d array to store
# states of dp
dp = np.zeros((n,n))

# Array to determine whether
# a state has been solved before
v = np.zeros((n,n));

# Function to return the minimum steps required
def minSteps(i, j, arr) :

    # Base cases
    if (i == n - 1 and j == n - 1) :
        return 0;

    if (i > n - 1 or j > n - 1) :
        return 9999999;

    # If a state has been solved before
    # it won't be evaluated again
    if (v[i][j]) :
        return dp[i][j];

    v[i][j] = 1;
    dp[i][j] = 9999999;

    # Recurrence relation
    for k in range(max(0, arr[i][j] + j - n + 1),min(n - i - 1, arr[i][j]) + 1) :
        dp[i][j] = min(dp[i][j], minSteps(i + k, j + arr[i][j] - k, arr));

    dp[i][j] += 1;

    return dp[i][j];

# Driver code
if __name__ == "__main__" :

    arr = [
            [ 4, 1, 2 ],
            [ 1, 1, 1 ],
            [ 2, 1, 1 ]
            ];

    ans = minSteps(0, 0, arr);
    if (ans >= 9999999) :
        print(-1);
    else :
        print(ans);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int n = 3;

    // 2d array to store
    // states of dp
    static int[,] dp = new int[n, n];

    // Array to determine whether
    // a state has been solved before
    static int[,] v = new int[n, n];

    // Function to return the minimum steps required
    static int minSteps(int i, int j, int [,]arr)
    {

        // Base cases
        if (i == n - 1 && j == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || j > n - 1)
        {
            return 9999999;
        }

        // If a state has been solved before
        // it won't be evaluated again
        if (v[i, j] == 1)
        {
            return dp[i, j];
        }

        v[i, j] = 1;
        dp[i, j] = 9999999;

        // Recurrence relation
        for (int k = Math.Max(0, arr[i,j] + j - n + 1);
            k <= Math.Min(n - i - 1, arr[i,j]); k++)
        {
            dp[i,j] = Math.Min(dp[i,j],
                                minSteps(i + k, j + arr[i,j] - k, arr));
        }

        dp[i,j]++;

        return dp[i,j];
    }

    // Driver code
    static public void Main ()
    {
        int [,]arr = { { 4, 1, 2 },
                        { 1, 1, 1 },
                        { 2, 1, 1 } };

        int ans = minSteps(0, 0, arr);
        if (ans >= 9999999)
        {
            Console.WriteLine(-1);
        }
        else
        {
            Console.WriteLine(ans);
        }
    }
}

// This code contributed by ajit.
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    let n = 3;

    // 2d array to store
    // states of dp
    let dp = new Array(n);

    // Array to determine whether
    // a state has been solved before
    let v = new Array(n);
    for(let i = 0; i < n; i++)
    {
        dp[i] = new Array(n);
        v[i] = new Array(n);
        for(let j = 0; j < n; j++)
        {
            dp[i][j] = 0;
            v[i][j] = 0;
        }
    }

    // Function to return the minimum steps required
    function minSteps(i, j, arr)
    {

        // Base cases
        if (i == n - 1 && j == n - 1) {
            return 0;
        }

        if (i > n - 1 || j > n - 1) {
            return 9999999;
        }

        // If a state has been solved before
        // it won't be evaluated again
        if (v[i][j] == 1) {
            return dp[i][j];
        }

        v[i][j] = 1;
        dp[i][j] = 9999999;

        // Recurrence relation
        for (let k = Math.max(0, arr[i][j] + j - n + 1);
             k <= Math.min(n - i - 1, arr[i][j]); k++) {
            dp[i][j] = Math.min(dp[i][j],
                                minSteps(i + k, j + arr[i][j] - k, arr));
        }

        dp[i][j]++;

        return dp[i][j];
    }

    let arr = [ [ 4, 1, 2 ],
               [ 1, 1, 1 ],
               [ 2, 1, 1 ] ];

    let ans = minSteps(0, 0, arr);
    if (ans >= 9999999) {
      document.write(-1);
    }
    else {
      document.write(ans);
    }

</script>
```

**Output:** 

```
1
```

上述方法的时间复杂度为 O(n <sup>3</sup> )。在最坏的情况下，每个状态都需要 O(n)个时间来解决。