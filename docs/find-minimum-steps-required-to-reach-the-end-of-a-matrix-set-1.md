# 找到到达矩阵末尾所需的最小步数| Set–1

> 原文:[https://www . geesforgeks . org/find-到达矩阵集末尾所需的最少步骤-1/](https://www.geeksforgeeks.org/find-minimum-steps-required-to-reach-the-end-of-a-matrix-set-1/)

给定一个由正整数组成的 2d 矩阵，任务是找到到达矩阵末端(最左边的底部单元格)所需的最小步数。如果我们在细胞(I，j)，我们可以去细胞(I，j+arr[i][j])或(i+arr[i][j]，j)。我们不能出界。如果不存在路径，打印-1。

**示例:**

```
Input : 
mat[][] = {{2, 1, 2},
           {1, 1, 1},
           {1, 1, 1}}
Output : 2
Explanation : The path will be {0, 0} -> {0, 2} -> {2, 2}
Thus, we are reaching end in two steps.

Input :
mat[][] = {{1, 1, 2},
           {1, 1, 1},
           {2, 1, 1}}
Output : 3
```

一个**简单的解决方案**就是探索所有可能的解决方案。这需要指数级的时间。
**更好的做法:**我们可以用动态规划在多项式时间内解决这个问题。
我们来决定一下‘DP’的状态。我们将在 2d DP 上构建我们的解决方案。
假设我们在{i，j}号牢房。我们将尝试找到从该单元到达该单元(n-1，n-1)所需的最小步数。
我们只有两条可能的路径，即到达细胞{i，j+arr[i][j]}或{i+arr[i][j]，j}。
一个简单的递归关系是:

```
dp[i][j] = 1 + min(dp[i+arr[i]][j], dp[i][j+arr[i][j]])
```

下面是上述想法的实现:

## C++

```
// C++ program to implement above approach

#include <bits/stdc++.h>
#define n 3
using namespace std;

// 2d array to store
// states of dp
int dp[n][n];

// array to determine whether
// a state has been solved before
int v[n][n];

// Function to find the minimum number of
// steps to reach the end of matrix
int minSteps(int i, int j, int arr[][n])
{
    // base cases
    if (i == n - 1 and j == n - 1)
        return 0;

    if (i > n - 1 || j > n - 1)
        return 9999999;

    // if a state has been solved before
    // it won't be evaluated again.
    if (v[i][j])
        return dp[i][j];

    v[i][j] = 1;

    // recurrence relation
    dp[i][j] = 1 + min(minSteps(i + arr[i][j], j, arr),
                       minSteps(i, j + arr[i][j], arr));

    return dp[i][j];
}

// Driver Code
int main()
{
    int arr[n][n] = { { 2, 1, 2 },
                      { 1, 1, 1 },
                      { 1, 1, 1 } };

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
// Java program to implement above approach
class GFG {

    static int n = 3;

    // 2d array to store
    // states of dp
    static int dp[][] = new int[n][n];

    // array to determine whether
    // a state has been solved before
    static int[][] v = new int[n][n];

    // Function to find the minimum number of
    // steps to reach the end of matrix
    static int minSteps(int i, int j, int arr[][])
    {
        // base cases
        if (i == n - 1 && j == n - 1) {
            return 0;
        }

        if (i > n - 1 || j > n - 1) {
            return 9999999;
        }

        // if a state has been solved before
        // it won't be evaluated again.
        if (v[i][j] == 1) {
            return dp[i][j];
        }

        v[i][j] = 1;

        // recurrence relation
        dp[i][j] = 1 + Math.min(minSteps(i + arr[i][j], j, arr), minSteps(i, j + arr[i][j], arr));

        return dp[i][j];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[][] = { { 2, 1, 2 },
                        { 1, 1, 1 },
                        { 1, 1, 1 } };

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
# Python3 program to implement above approach
import numpy as np;

n = 3

# 2d array to store
# states of dp
dp = np.zeros((n, n));

# array to determine whether
# a state has been solved before
v = np.zeros((n, n));

# Function to find the minimum number of
# steps to reach the end of matrix
def minSteps(i, j, arr) :

    # base cases
    if (i == n - 1 and j == n - 1) :
        return 0;

    if (i > n - 1 or j > n - 1) :
        return 9999999;

    # if a state has been solved before
    # it won't be evaluated again.
    if (v[i][j]) :
        return dp[i][j];

    v[i][j] = 1;

    # recurrence relation
    dp[i][j] = 1 + min(minSteps(i + arr[i][j], j, arr),
                    minSteps(i, j + arr[i][j], arr));

    return dp[i][j];

# Driver Code
arr = [ [ 2, 1, 2 ],
            [ 1, 1, 1 ],
            [ 1, 1, 1 ]
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
// C# program to implement above approach
using System;

class GFG
{

    static int n = 3;

    // 2d array to store
    // states of dp
    static int [,]dp = new int[n, n];

    // array to determine whether
    // a state has been solved before
    static int[,] v = new int[n, n];

    // Function to find the minimum number of
    // steps to reach the end of matrix
    static int minSteps(int i, int j, int [,]arr)
    {
        // base cases
        if (i == n - 1 && j == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || j > n - 1)
        {
            return 9999999;
        }

        // if a state has been solved before
        // it won't be evaluated again.
        if (v[i, j] == 1)
        {
            return dp[i, j];
        }

        v[i, j] = 1;

        // recurrence relation
        dp[i, j] = 1 + Math.Min(minSteps(i + arr[i,j], j, arr),
                            minSteps(i, j + arr[i,j], arr));

        return dp[i, j];
    }

    // Driver Code
    static public void Main ()
    {
        int [,]arr = { { 2, 1, 2 },
                        { 1, 1, 1 },
                        { 1, 1, 1 } };

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

    // Javascript program to implement
    // above approach

    let n = 3;

    // 2d array to store
    // states of dp
    let dp = new Array(n);
    for(let i = 0; i < n; i++)
    {
        dp[i] = new Array(n);
    }

    // array to determine whether
    // a state has been solved before
    let v = new Array(n);
    for(let i = 0; i < n; i++)
    {
        v[i] = new Array(n);
    }

    // Function to find the minimum number of
    // steps to reach the end of matrix
    function minSteps(i, j, arr)
    {
        // base cases
        if (i == n - 1 && j == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || j > n - 1)
        {
            return 9999999;
        }

        // if a state has been solved before
        // it won't be evaluated again.
        if (v[i][j] == 1) {
            return dp[i][j];
        }

        v[i][j] = 1;

        // recurrence relation
        dp[i][j] = 1 + Math.min(minSteps(i +
        arr[i][j], j, arr), minSteps(i, j + arr[i][j], arr));

        return dp[i][j];
    }

    let arr = [ [ 2, 1, 2 ],
               [ 1, 1, 1 ],
               [ 1, 1, 1 ] ];

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
2
```

**时间复杂度** : O(N <sup>2</sup> )。