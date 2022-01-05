# 生成总和等于给定值的最小硬币组合

> 原文:[https://www . geeksforgeeks . org/生成最小硬币组合-结果-给定值/](https://www.geeksforgeeks.org/generate-a-combination-of-minimum-coins-that-results-to-a-given-value/)

给定一个代表可用面额的大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个整数 **X** 。任务是找到可用面额的最小硬币数量的任意组合，使得硬币的总和为 **X** 。如果可用面额无法获得给定金额，打印 **-1** 。

**示例:**

> **输入:** X = 21，arr[] = {2，3，4，5}
> **输出:** 2 4 5 5 5
> **解释:**
> 一种可能的解决方案是{2，4，5，5，5，5}，其中 2 + 4 + 5 + 5 + 5 = 21。
> 另一种可能的解决方案是{3，3，5，5，5}。
> 
> **输入:** X = 1，arr[] = {2，4，6，9}
> **输出:** -1
> **说明:**
> 所有硬币都大于 1。因此，不存在任何解决方案。

**天真方法:**最简单的方法是尝试给定面额的所有可能组合，使得在每个组合中，硬币的总和等于 **X** 。从这些组合中，选择硬币数量最少的一个并打印出来。如果任意组合之和不等于 **X** ，打印 **-1** 。
***时间复杂度:**O(X<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来优化[找到最小硬币数](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)。在找到最小硬币数的同时，可以使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来跟踪使其总和等于 **X** 所需的硬币。按照以下步骤解决问题:

1.  初始化一个辅助数组 **dp[]** ，其中 **dp[i]** 将存储[使总和](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)等于 **i** 所需的最小硬币数。
2.  使用[这篇](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)文章中讨论的方法，找出使它们的总和等于 **X** 所需的最小硬币数。
3.  找到最小硬币数后，使用[回溯技术](https://www.geeksforgeeks.org/backtracking-introduction/)追踪使用的硬币，使总和等于 **X** 。
4.  回溯时，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)选择一个小于当前和的硬币，使得 **dp【当前和】**等于 **dp【当前和–选择的硬币】+1** 。将所选硬币存储在一个数组中。
5.  完成上述步骤后，通过将**当前总和**作为**(当前总和–所选硬币值)**再次回溯。
6.  找到解决方案后，打印所选硬币的阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 100000

// dp array to memoize the results
int dp[MAX + 1];

// List to store the result
list<int> denomination;

// Function to find the minimum number of
// coins to make the sum equals to X
int countMinCoins(int n, int C[], int m)
{
    // Base case
    if (n == 0) {
        dp[0] = 0;
        return 0;
    }

    // If previously computed
    // subproblem occurred
    if (dp[n] != -1)
        return dp[n];

    // Initialize result
    int ret = INT_MAX;

    // Try every coin that has smaller
    // value than n
    for (int i = 0; i < m; i++) {

        if (C[i] <= n) {

            int x
                = countMinCoins(n - C[i],
                                C, m);

            // Check for INT_MAX to avoid
            // overflow and see if result
            // can be minimized
            if (x != INT_MAX)
                ret = min(ret, 1 + x);
        }
    }

    // Memoizing value of current state
    dp[n] = ret;
    return ret;
}

// Function to find the possible
// combination of coins to make
// the sum equal to X
void findSolution(int n, int C[], int m)
{
    // Base Case
    if (n == 0) {

        // Print Solutions
        for (auto it : denomination) {
            cout << it << ' ';
        }

        return;
    }

    for (int i = 0; i < m; i++) {

        // Try every coin that has
        // value smaller than n
        if (n - C[i] >= 0
            and dp[n - C[i]] + 1
                    == dp[n]) {

            // Add current denominations
            denomination.push_back(C[i]);

            // Backtrack
            findSolution(n - C[i], C, m);
            break;
        }
    }
}

// Function to find the minimum
// combinations of coins for value X
void countMinCoinsUtil(int X, int C[],
                       int N)
{

    // Initialize dp with -1
    memset(dp, -1, sizeof(dp));

    // Min coins
    int isPossible
        = countMinCoins(X, C,
                        N);

    // If no solution exists
    if (isPossible == INT_MAX) {
        cout << "-1";
    }

    // Backtrack to find the solution
    else {
        findSolution(X, C, N);
    }
}

// Driver code
int main()
{
    int X = 21;

    // Set of possible denominations
    int arr[] = { 2, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countMinCoinsUtil(X, arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

static final int MAX = 100000;

// dp array to memoize the results
static int []dp = new int[MAX + 1];

// List to store the result
static List<Integer> denomination =
            new LinkedList<Integer>();

// Function to find the minimum
// number of coins to make the
// sum equals to X
static int countMinCoins(int n,
                         int C[], int m)
{
  // Base case
  if (n == 0)
  {
    dp[0] = 0;
    return 0;
  }

  // If previously computed
  // subproblem occurred
  if (dp[n] != -1)
    return dp[n];

  // Initialize result
  int ret = Integer.MAX_VALUE;

  // Try every coin that has smaller
  // value than n
  for (int i = 0; i < m; i++)
  {
    if (C[i] <= n)
    {
      int x = countMinCoins(n - C[i],
                            C, m);

      // Check for Integer.MAX_VALUE to avoid
      // overflow and see if result
      // can be minimized
      if (x != Integer.MAX_VALUE)
        ret = Math.min(ret, 1 + x);
    }
  }

  // Memoizing value of current state
  dp[n] = ret;
  return ret;
}

// Function to find the possible
// combination of coins to make
// the sum equal to X
static void findSolution(int n,
                         int C[], int m)
{
  // Base Case
  if (n == 0)
  {
    // Print Solutions
    for (int it : denomination)
    {
      System.out.print(it + " ");
    }
    return;
  }

  for (int i = 0; i < m; i++)
  {
    // Try every coin that has
    // value smaller than n
    if (n - C[i] >= 0 &&
        dp[n - C[i]] + 1 ==
        dp[n])
    {
      // Add current denominations
      denomination.add(C[i]);

      // Backtrack
      findSolution(n - C[i], C, m);
      break;
    }
  }
}

// Function to find the minimum
// combinations of coins for value X
static void countMinCoinsUtil(int X,
                              int C[], int N)
{
  // Initialize dp with -1
  for (int i = 0; i < dp.length; i++)
    dp[i] = -1;

  // Min coins
  int isPossible = countMinCoins(X, C, N);

  // If no solution exists
  if (isPossible == Integer.MAX_VALUE)
  {
    System.out.print("-1");
  }

  // Backtrack to find the solution
  else
  {
    findSolution(X, C, N);
  }
}

// Driver code
public static void main(String[] args)
{
  int X = 21;

  // Set of possible denominations
  int arr[] = {2, 3, 4, 5};

  int N = arr.length;

  // Function Call
  countMinCoinsUtil(X, arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

MAX = 100000

# dp array to memoize the results
dp = [-1] * (MAX + 1)

# List to store the result
denomination = []

# Function to find the minimum number of
# coins to make the sum equals to X
def countMinCoins(n, C, m):

    # Base case
    if (n == 0):
        dp[0] = 0
        return 0

    # If previously computed
    # subproblem occurred
    if (dp[n] != -1):
        return dp[n]

    # Initialize result
    ret = sys.maxsize

    # Try every coin that has smaller
    # value than n
    for i in range(m):
        if (C[i] <= n):
            x = countMinCoins(n - C[i], C, m)

            # Check for INT_MAX to avoid
            # overflow and see if result
            #. an be minimized
            if (x != sys.maxsize):
                ret = min(ret, 1 + x)

    # Memoizing value of current state
    dp[n] = ret
    return ret

# Function to find the possible
# combination of coins to make
# the sum equal to X
def findSolution(n, C, m):

    # Base Case
    if (n == 0):

        # Print Solutions
        for it in denomination:
            print(it, end = " ")

        return

    for i in range(m):

        # Try every coin that has
        # value smaller than n
        if (n - C[i] >= 0 and
         dp[n - C[i]] + 1 == dp[n]):

            # Add current denominations
            denomination.append(C[i])

            # Backtrack
            findSolution(n - C[i], C, m)
            break

# Function to find the minimum
# combinations of coins for value X
def countMinCoinsUtil(X, C,N):

    # Initialize dp with -1
    # memset(dp, -1, sizeof(dp))

    # Min coins
    isPossible = countMinCoins(X, C,N)

    # If no solution exists
    if (isPossible == sys.maxsize):
        print("-1")

    # Backtrack to find the solution
    else:
        findSolution(X, C, N)

# Driver code
if __name__ == '__main__':

    X = 21

    # Set of possible denominations
    arr = [ 2, 3, 4, 5 ]

    N = len(arr)

    # Function call
    countMinCoinsUtil(X, arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static readonly int MAX = 100000;

// dp array to memoize the results
static int []dp = new int[MAX + 1];

// List to store the result
static List<int> denomination =
            new List<int>();

// Function to find the minimum
// number of coins to make the
// sum equals to X
static int countMinCoins(int n,
                         int []C,
                         int m)
{
  // Base case
  if (n == 0)
  {
    dp[0] = 0;
    return 0;
  }

  // If previously computed
  // subproblem occurred
  if (dp[n] != -1)
    return dp[n];

  // Initialize result
  int ret = int.MaxValue;

  // Try every coin that has smaller
  // value than n
  for (int i = 0; i < m; i++)
  {
    if (C[i] <= n)
    {
      int x = countMinCoins(n - C[i],
                            C, m);

      // Check for int.MaxValue to avoid
      // overflow and see if result
      // can be minimized
      if (x != int.MaxValue)
        ret = Math.Min(ret, 1 + x);
    }
  }

  // Memoizing value of current state
  dp[n] = ret;
  return ret;
}

// Function to find the possible
// combination of coins to make
// the sum equal to X
static void findSolution(int n,
                         int []C,
                         int m)
{
  // Base Case
  if (n == 0)
  {
    // Print Solutions
    foreach (int it in denomination)
    {
      Console.Write(it + " ");
    }
    return;
  }

  for (int i = 0; i < m; i++)
  {
    // Try every coin that has
    // value smaller than n
    if (n - C[i] >= 0 &&
        dp[n - C[i]] + 1 ==
        dp[n])
    {
      // Add current denominations
      denomination.Add(C[i]);

      // Backtrack
      findSolution(n - C[i], C, m);
      break;
    }
  }
}

// Function to find the minimum
// combinations of coins for value X
static void countMinCoinsUtil(int X,
                              int []C,
                              int N)
{
  // Initialize dp with -1
  for (int i = 0; i < dp.Length; i++)
    dp[i] = -1;

  // Min coins
  int isPossible = countMinCoins(X, C, N);

  // If no solution exists
  if (isPossible == int.MaxValue)
  {
    Console.Write("-1");
  }

  // Backtrack to find the solution
  else
  {
    findSolution(X, C, N);
  }
}

// Driver code
public static void Main(String[] args)
{
  int X = 21;

  // Set of possible denominations
  int []arr = {2, 3, 4, 5};

  int N = arr.Length;

  // Function Call
  countMinCoinsUtil(X, arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var MAX = 100000;

// dp array to memoize the results
var dp = Array(MAX+1);

// List to store the result
var denomination = [];

// Function to find the minimum number of
// coins to make the sum equals to X
function countMinCoins(n, C, m)
{
    // Base case
    if (n == 0) {
        dp[0] = 0;
        return 0;
    }

    // If previously computed
    // subproblem occurred
    if (dp[n] != -1)
        return dp[n];

    // Initialize result
    var ret = 1000000000;

    // Try every coin that has smaller
    // value than n
    for (var i = 0; i < m; i++) {

        if (C[i] <= n) {

            var x
                = countMinCoins(n - C[i],
                                C, m);

            // Check for INT_MAX to avoid
            // overflow and see if result
            // can be minimized
            if (x != 1000000000)
                ret = Math.min(ret, 1 + x);
        }
    }

    // Memoizing value of current state
    dp[n] = ret;
    return ret;
}

// Function to find the possible
// combination of coins to make
// the sum equal to X
function findSolution(n, C, m)
{
    // Base Case
    if (n == 0) {

        denomination.forEach(it => {

            document.write( it + ' ');
        });

        return;
    }

    for (var i = 0; i < m; i++) {

        // Try every coin that has
        // value smaller than n
        if (n - C[i] >= 0
            && dp[n - C[i]] + 1
                    == dp[n]) {

            // Add current denominations
            denomination.push(C[i]);

            // Backtrack
            findSolution(n - C[i], C, m);
            break;
        }
    }
}

// Function to find the minimum
// combinations of coins for value X
function countMinCoinsUtil(X, C, N)
{

    // Initialize dp with -1
    dp = Array(MAX+1).fill(-1);

    // Min coins
    var isPossible
        = countMinCoins(X, C,
                        N);

    // If no solution exists
    if (isPossible == 1000000000) {
        document.write( "-1");
    }

    // Backtrack to find the solution
    else {
        findSolution(X, C, N);
    }
}

// Driver code
var X = 21;
// Set of possible denominations
var arr = [2, 3, 4, 5];
var N = arr.length;
// Function Call
countMinCoinsUtil(X, arr, N);

</script>
```

**Output:** 

```
2 4 5 5 5
```

***时间复杂度:** O(N*X)，其中 N 为给定数组的长度，X 为给定整数。*
***辅助空间:** O(N)*