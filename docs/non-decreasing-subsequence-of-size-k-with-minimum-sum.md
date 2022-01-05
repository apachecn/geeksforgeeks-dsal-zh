# 具有最小和的大小为 k 的非递减子序列

> 原文:[https://www . geesforgeks . org/非递减子序列最小和 k/](https://www.geeksforgeeks.org/non-decreasing-subsequence-of-size-k-with-minimum-sum/)

给定 n 个整数的序列，你必须找出长度为 k 且和最小的非减子序列。如果不存在序列，输出-1。
**例:**

```
Input : [58 12 11 12 82 30 20 77 16 86], 
        k = 3
Output : 39
{11 + 12 + 16}

Input : [58 12 11 12 82 30 20 77 16 86], 
        k = 4
Output : 120
{11 + 12 + 20 + 77}

Input : [58 12 11 12 82 30 20 77 16 86], 
        k = 5
Output : 206
```

设解出(I，k)是以索引 I 结束的大小为 k 的子序列的最小和，那么将有两种状态:
1。包括当前元素。{solve(j，k-1) + a[i]}
2。排除当前元素。{solve(j，k)}
我们的循环状态是:

```

dp[i][k] = min(solve(j, k-1) + a[i], solve(j, k)) 
  if a[i] >= a[j] for all 0 <= j <= i.
```

## C++

```
// C++ program to find Non-decreasing sequence
// of size k with minimum sum
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;
const int inf = 2e9;

// Global table used for memoization
int dp[MAX][MAX];

void initialize()
{
    for (int i = 0; i < MAX; i++)
        for (int j = 0; j < MAX; j++)
            dp[i][j] = -1;
}

int solve(int arr[], int i, int k)
{
    // If already computed
    if (dp[i][k] != -1)
        return dp[i][k];

    // Corner cases
    if (i < 0)
        return inf;
    if (k == 1) {
        int ans = inf;
        for (int j = 0; j <= i; j++)
            ans = min(ans, arr[j]);
        return ans;
    }

    // Recursive computation.
    int ans = inf;
    for (int j = 0; j < i; j++)
        if (arr[i] >= arr[j])
            ans = min(ans, min(solve(arr, j, k),
                               solve(arr, j, k - 1) + arr[i]));
        else {
            ans = min(ans, solve(arr, j, k));
        }

    dp[i][k] = ans;
    return dp[i][k];
}

// Driver code
int main()
{
    initialize();
    int a[] = { 58, 12, 11, 12, 82, 30,
                20, 77, 16, 86 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;
    cout << solve(a, n - 1, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Non-decreasing sequence
// of size k with minimum sum
import java.io.*;
import java.util.*;

class GFG {
    public static int MAX = 100;
    public static int inf = 1000000;

    // Table used for memoization
    public static int[][] dp = new int[MAX][MAX];

    // initialize
    static void initialize()
    {
        for (int i = 0; i < MAX; i++)
            for (int j = 0; j < MAX; j++)
                dp[i][j] = -1;
    }

    // Function to find non-decreasing sequence
    // of size k with minimum sum
    static int solve(int arr[], int i, int k)
    {
        // If already computed
        if (dp[i][k] != -1)
            return dp[i][k];

        // Corner cases
        if (i < 0)
            return inf;
        if (k == 1) {
            int ans = inf;
            for (int j = 0; j <= i; j++)
                ans = Math.min(ans, arr[j]);
            return ans;
        }

        // Recursive computation
        int ans = inf;
        for (int j = 0; j < i; j++)
            if (arr[i] >= arr[j])
                ans = Math.min(ans, Math.min(solve(arr, j, k), solve(arr, j, k - 1) + arr[i]));
            else
                ans = Math.min(ans, solve(arr, j, k));

        dp[i][k] = ans;

        return dp[i][k];
    }

    // driver program
    public static void main(String[] args)
    {
        initialize();
        int a[] = { 58, 12, 11, 12, 82, 30,
                    20, 77, 16, 86 };
        int n = a.length;
        int k = 4;
        System.out.println(solve(a, n - 1, k));
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to find Non-decreasing sequence
# of size k with minimum sum

# Global table used for memoization
dp = []
for i in xrange(10**2 + 1):
    temp = [-1]*(10**2 + 1)
    dp.append(temp)

def solve(a, i, k):
    if dp[i][k] != -1:  # Memoization
        return dp[i][k]
    elif i < 0: # out of bounds
        return float('inf')

    # when there is only one element
    elif k == 1:   
        return min(a[: i + 1])

    # Else two cases
    # 1 include current element
    # solve(a, j, k-1) + a[i]
    # 2 ignore current element
    # solve(a, j, k)
    else: 
        ans = float('inf')
        for j in xrange(i):
            if a[i] >= a[j]:
                ans = min(ans, solve(a, j, k), solve(a, j, k-1) + a[i])
            else:
                ans = min(ans, solve(a, j, k))
        dp[i][k] = ans
        return dp[i][k]

# Driver code
a = [58, 12, 11, 12, 82, 30, 20, 77, 16, 86]       
print solve(a, len(a)-1, 4)
```

## C#

```
// C# program to find Non-decreasing sequence
// of size k with minimum sum
using System;

class GFG {

    public static int MAX = 100;
    public static int inf = 1000000;

    // Table used for memoization
    public static int[, ] dp = new int[MAX, MAX];

    // initialize
    static void initialize()
    {
        for (int i = 0; i < MAX; i++)
          for (int j = 0; j < MAX; j++)
            dp[i, j] = -1;
    }

    // Function to find non-decreasing
    // sequence of size k with minimum sum
    static int solve(int[] arr, int i, int k)
    {
        int ans = 0;

        // If already computed
        if (dp[i, k] != -1)
            return dp[i, k];

        // Corner cases
        if (i < 0)
            return inf;
        if (k == 1)
        {
            ans = inf;
            for (int j = 0; j <= i; j++)
            ans = Math.Min(ans, arr[i]);
            return ans;
        }

        // Recursive computation
        ans = inf;
        for (int j = 0; j < i; j++)
            if (arr[i] >= arr[j])
                ans = Math.Min(ans, Math.Min(solve(arr, j, k),
                               solve(arr, j, k - 1) + arr[i]));
            else
                ans = Math.Min(ans, solve(arr, j, k));

        dp[i, k] = ans;

        return dp[i, k];
    }

    // driver program
    public static void Main()
    {
        initialize();
        int[] a = { 58, 12, 11, 12, 82, 30,
                          20, 77, 16, 86 };
        int n = a.Length;
        int k = 4;
        Console.WriteLine(solve(a, n - 1, k));
    }
}

// This code is contributed by vt_m
```

## java 描述语言

```
<script>

    // Javascript program to find
    // Non-decreasing sequence
    // of size k with minimum sum

    let MAX = 100;
    let inf = 1000000;

    // Table used for memoization
    let dp = new Array(MAX);
    for (let i = 0; i < MAX; i++)
    {
      dp[i] = new Array(MAX);
      for (let j = 0; j < MAX; j++)
      {
            dp[i][j] = 0;
      }
    }

    // initialize
    function initialize()
    {
        for (let i = 0; i < MAX; i++)
            for (let j = 0; j < MAX; j++)
                dp[i][j] = -1;
    }

    // Function to find non-decreasing sequence
    // of size k with minimum sum
    function solve(arr, i, k)
    {
        // If already computed
        if (dp[i][k] != -1)
            return dp[i][k];

        // Corner cases
        if (i < 0)
            return inf;
        if (k == 1) {
            let ans = inf;
            for (let j = 0; j <= i; j++)
                ans = Math.min(ans, arr[j]);
            return ans;
        }

        // Recursive computation
        let ans = inf;
        for (let j = 0; j < i; j++)
            if (arr[i] >= arr[j])
                ans = Math.min(ans, Math.min(solve(arr, j, k),
                solve(arr, j, k - 1) + arr[i]));
            else
                ans = Math.min(ans, solve(arr, j, k));

        dp[i][k] = ans;

        return dp[i][k];
    }

    initialize();
    let a = [ 58, 12, 11, 12, 82, 30, 20, 77, 16, 86 ];
    let n = a.length;
    let k = 4;
    document.write(solve(a, n - 1, k));

</script>
```

**输出:**

```
 120
```

本文由 [Anuj Shah](https://www.linkedin.com/in/anuj-shah-a7186480/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。