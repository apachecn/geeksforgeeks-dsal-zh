# 爆气球最大化硬币

> 原文:[https://www . geesforgeks . org/burst-气球-最大化-硬币/](https://www.geeksforgeeks.org/burst-balloon-to-maximize-coins/)

我们得到了 N 个气球，每个气球都有一些与之相关的硬币。当气球 I 爆裂时，获得的硬币数量等于 A[i-1]*A[i]*A[i+1]。此外，气球 i-1 和 i+1 现在变得相邻。找到所有气球爆裂后可能获得的最大利润。假设每个边界都有一个额外的 1。
**例:**

```
Input : 5, 10
Output : 60
Explanation - First Burst 5, Coins = 1*5*10
              Then burst 10, Coins+= 1*10*1
              Total = 60

Input : 1, 2, 3, 4, 5
Output : 110
```

这里讨论的是递归解决方案。我们可以用动态规划来解决这个问题。
首先，考虑一个从左到右(含)的子数组。
如果我们假设索引 Last 处的气球是这个子数组中最后一个被爆开的气球，我们会说所获得的是-A[left-1]*A[last]*A[right+1]。
此外，获得的硬币总数将是这个值，加上 dp[左][最后–1]+DP[最后+1][右]，其中 dp[i][j]表示具有索引 I，j 的子阵列获得的最大硬币。因此，对于左和右的每个值，我们需要找到并选择获得最大硬币的最后值，并更新 DP 阵列。
我们的答案是 dp[1][N]处的值。

## C++

```
// C++ program burst balloon problem
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

int getMax(int A[], int N)
{
    // Add Bordering Balloons
    int B[N + 2];

    B[0] = 1;
    B[N + 1] = 1;

    for (int i = 1; i <= N; i++)
        B[i] = A[i - 1];

    // Declare DP Array
    int dp[N + 2][N + 2];
    memset(dp, 0, sizeof(dp));

    for (int length = 1; length < N + 1; length++)
    {
        for (int left = 1; left < N - length + 2; left++)
        {
            int right = left + length - 1;
            // For a sub-array from indices left, right
            // This innermost loop finds the last balloon burst
            for (int last = left; last < right + 1; last++)
            {
                dp[left][right] = max(dp[left][right],
                                      dp[left][last - 1] +
                                      B[left - 1] * B[last] * B[right + 1] +
                                      dp[last + 1][right]);
            }
        }
    }
    return dp[1][N];
}

// Driver code
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };

    // Size of the array
    int N = sizeof(A) / sizeof(A[0]);

    // Calling function
    cout << getMax(A, N) << endl;
}

// This code is contributed by ashutosh450
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate
// Burst balloon problem
import java.util.Arrays;

class GFG{

public static int getMax(int[] A, int N)
{

    // Add Bordering Balloons
    int[] B = new int[N + 2];
    B[0] = B[N + 1] = 1;

    for(int i = 1; i <= N; i++)
        B[i] = A[i - 1];

    // Declaring DP array
    int[][] dp = new int[N + 2][N + 2];

    for(int length = 1;
            length < N + 1; length++)
    {
        for(int left = 1;
                left < N - length + 2; left++)
        {
            int right = left + length -1;

            // For a sub-array from indices
            // left, right. This innermost
            // loop finds the last balloon burst
            for(int last = left;
                    last < right + 1; last++)
            {
                dp[left][right] = Math.max(
                                  dp[left][right],
                                  dp[left][last - 1] +
                                   B[left - 1] * B[last] *
                                   B[right + 1] +
                                  dp[last + 1][right]);
            }
        }
    }
    return dp[1][N];
}

// Driver code
public static void main(String args[])
{
    int[] A = { 1, 2, 3, 4, 5 };

    // Size of the array
    int N = A.length;

    // Calling function
    System.out.println(getMax(A, N));
}
}

// This code is contributed by dadi madhav
```

## 蟒蛇 3

```
# Python3 program burst balloon problem.

def getMax(A):
    N = len(A)
    A = [1] + A + [1]# Add Bordering Balloons
    dp = [[0 for x in range(N + 2)] for y in range(N + 2)]# Declare DP Array

    for length in range(1, N + 1):
        for left in range(1, N-length + 2):
            right = left + length -1

            # For a sub-array from indices left, right
            # This innermost loop finds the last balloon burst
            for last in range(left, right + 1):
                dp[left][right] = max(dp[left][right], \
                                      dp[left][last-1] + \
                                      A[left-1]*A[last]*A[right + 1] + \
                                      dp[last + 1][right])
    return(dp[1][N])

# Driver code
A = [1, 2, 3, 4, 5]
print(getMax(A))
```

## C#

```
// C# program to illustrate
// Burst balloon problem
using System;

class GFG{

public static int getMax(int[] A, int N)
{

    // Add Bordering Balloons
    int[] B = new int[N + 2];
    B[0] = B[N + 1] = 1;

    for(int i = 1; i <= N; i++)
        B[i] = A[i - 1];

    // Declaring DP array
    int[,] dp = new int[(N + 2), (N + 2)];

    for(int length = 1;
            length < N + 1; length++)
    {
        for(int left = 1;
                left < N - length + 2; left++)
        {
            int right = left + length -1;

            // For a sub-array from indices
            // left, right. This innermost
            // loop finds the last balloon burst
            for(int last = left;
                    last < right + 1; last++)
            {
                dp[left, right] = Math.Max(
                                  dp[left, right],
                                  dp[left, last - 1] +
                                   B[left - 1] * B[last] *
                                   B[right + 1] +
                                  dp[last + 1, right]);
            }
        }
    }
    return dp[1, N];
}

// Driver code
public static void Main()
{
    int[] A = new int[] { 1, 2, 3, 4, 5 };

    // Size of the array
    int N = A.Length;

    // Calling function
    Console.WriteLine(getMax(A, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program burst balloon problem

function getMax(A, N)
{
    // Add Bordering Balloons
    var B = new Array(N+2);

    B[0] = 1;
    B[N + 1] = 1;

    for (var i = 1; i <= N; i++)
        B[i] = A[i - 1];

    // Declare DP Array    
    var dp = new Array(N + 2);
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(N + 2).fill(0);
    }

    for (var length = 1; length < N + 1; length++)
    {
        for (var left = 1; left < N - length + 2; left++)
        {
            var right = left + length - 1;
            // For a sub-array from indices left, right
            // This innermost loop finds the last balloon burst
            for (var last = left; last < right + 1; last++)
            {
                dp[left][right] = Math.max(dp[left][right],
                                      dp[left][last - 1] +
                                      B[left - 1] * B[last] * B[right + 1] +
                                      dp[last + 1][right]);
            }
        }
    }
    return dp[1][N];
}

// Driver code
var A = [ 1, 2, 3, 4, 5 ];

// Size of the array
var N = A.length;

// Calling function
document.write(getMax(A, N));

// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
110
```