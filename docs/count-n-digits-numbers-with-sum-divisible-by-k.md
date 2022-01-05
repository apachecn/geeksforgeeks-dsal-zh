# 用可被 K 整除的和数计算 N 位数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-with-sum-除尽-k/](https://www.geeksforgeeks.org/count-n-digits-numbers-with-sum-divisible-by-k/)

给定两个整数 **N** 和 **K** ，任务是统计所有 **N** 位数，其位数之和可被 **K** 整除。

**示例:**

> **输入:** N = 2，K = 7
> **输出:** 12
> **说明:** 2 位数的和可被 7 整除的数字为:{16，25，34，43，52，59，61，68，70，77，86，95}。
> 因此，要求的输出是 12。
> 
> **输入:** N = 1，K = 2
> T3】输出: 4

**天真方法:**最简单的方法是遍历范围**【10<sup>(N–1)</sup>、10<sup>N</sup>–1】**中的所有数字，并检查位于该范围内的数字的所有数字的[和是否可被 **K** 整除。对于每一个条件为真的数字，增加**计数**。最后，打印**计数**。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)

***时间复杂度:**O(10<sup>N</sup>–10<sup>N–1</sup>–1)*
***辅助空间:** O(1)*

**高效途径:**思路是利用[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) 技术优化上述途径。下面是循环关系:

> ![CountNum(N, sum, st) = \sum^{9}_{i=0} countNum(N - 1, (sum + i)\mod K, st)              ](img/0a58a8ba8790db972b7a216d02438ea6.png "Rendered by QuickLaTeX.com")
> 
> **sum:** 代表数字的总和
> **st:** 检查一个数字是否包含任何前导 0。

按照以下步骤解决问题:

1.  初始化一个 3D 数组 **dp[N][K][st]** 计算并存储上述递归关系的所有子问题的值。
2.  最后，返回 **dp[N][sum%K][st]** 的值。

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define M 1000

// Function to count the N digit numbers
// whose sum is divisible by K
int countNum(int N, int sum, int K,
             bool st, int dp[M][M][2])
{
    // Base case
    if (N == 0 and sum == 0) {
        return 1;
    }
    if (N < 0) {
        return 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N][sum][st] != -1) {
        return dp[N][sum][st];
    }

    // Store the count of N digit numbers
    // whose sum is divisible by K
    int res = 0;

    // Check if the number does not contain
    // any leading 0.
    int start = st == 1 ? 0 : 1;

    // Recurrence relation
    for (int i = start; i <= 9; i++) {
        res += countNum(N - 1, (sum + i) % K,
                        K, (st | i > 0), dp);
    }

    return dp[N][sum][st] = res;
}

// Driver Code
int main()
{
    int N = 2, K = 7;

    // Stores the values of
    // overlapping subproblems
    int dp[M][M][2];

    memset(dp, -1, sizeof(dp));

    cout << countNum(N, 0, K, 0, dp);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG {

    static final int M = 1000;

    // Function to count the N digit numbers
    // whose sum is divisible by K
    static int countNum(int N, int sum, int K,
                        int st, int dp[][][])
    {

        // Base case
        if (N == 0 && sum == 0) {
            return 1;
        }
        if (N < 0) {
            return 0;
        }

        // If already computed
        // subproblem occurred
        if (dp[N][sum][st] != -1) {
            return dp[N][sum][st];
        }

        // Store the count of N digit numbers
        // whose sum is divisible by K
        int res = 0;

        // Check if the number does not contain
        // any leading 0.
        int start = st == 1 ? 0 : 1;

        // Recurrence relation
        for (int i = start; i <= 9; i++) {
            res += countNum(N - 1, (sum + i) % K,
                            K, ((st | i) > 0) ? 1 : 0, dp);
        }
        return dp[N][sum][st] = res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 2, K = 7;

        // Stores the values of
        // overlapping subproblems
        int[][][] dp = new int[M][M][2];

        for (int[][] i : dp)
            for (int[] j : i)
                Arrays.fill(j, -1);

        System.out.print(countNum(N, 0, K, 0, dp));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the N digit
# numbers whose sum is divisible by K
def countNum(N, sum, K, st, dp):

    # Base case
    if (N == 0 and sum == 0):
        return 1

    if (N < 0):
        return 0

    # If already computed
    # subproblem occurred
    if (dp[N][sum][st] != -1):
        return dp[N][sum][st]

    # Store the count of N digit
    # numbers whose sum is divisible by K
    res = 0
    start = 1

    # Check if the number does not contain
    # any leading 0.
    if (st == 1):
        start = 0
    else:
        start = 1

    # Recurrence relation
    for i in range(start, 10):
        min = 0

        if ((st | i) > 0):
            min = 1
        else:
            min = 0

        res += countNum(N - 1, (sum + i) % K,
                        K, min, dp)
        dp[N][sum][st] = res

    return dp[N][sum][st]

# Driver code
if __name__ == '__main__':

    N = 2
    K = 7
    M = 100

    # Stores the values of
    # overlapping subproblems
    dp = [[[-1 for i in range(2)]
               for j in range(M)]
               for j in range(M)]

    print(countNum(N, 0, K, 0, dp))

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static int M = 1000;

// Function to count the N digit numbers
// whose sum is divisible by K
static int countNum(int N, int sum, int K,
                    int st, int[,, ] dp)
{

    // Base case
    if (N == 0 && sum == 0)
    {
        return 1;
    }
    if (N < 0)
    {
        return 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N, sum, st] != -1)
    {
        return dp[N, sum, st];
    }

    // Store the count of N digit numbers
    // whose sum is divisible by K
    int res = 0;

    // Check if the number does not contain
    // any leading 0.
    int start = (st == 1 ? 0 : 1);

    // Recurrence relation
    for(int i = start; i <= 9; i++)
    {
        res += countNum(N - 1, (sum + i) % K,
                        K, ((st | i) > 0) ? 1 : 0, dp);
    }
    return dp[N, sum, st] = res;
}

// Driver code
static public void Main()
{
    int N = 2, K = 7;

    // Stores the values of
    // overlapping subproblems
    int[,, ] dp = new int[M, M, 2];

    for(int i = 0; i < M; i++)
        for(int j = 0; j < M; j++)
            for(int k = 0; k < 2; k++)
                dp[i, j, k] = -1;

    Console.WriteLine(countNum(N, 0, K, 0, dp));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

var M = 1000;

// Function to count the N digit numbers
// whose sum is divisible by K
function countNum(N, sum, K, st, dp)
{
    // Base case
    if (N == 0 && sum == 0) {
        return 1;
    }
    if (N < 0) {
        return 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N][sum][st] != -1) {
        return dp[N][sum][st];
    }

    // Store the count of N digit numbers
    // whose sum is divisible by K
    var res = 0;

    // Check if the number does not contain
    // any leading 0.
    var start = st == 1 ? 0 : 1;

    // Recurrence relation
    for (var i = start; i <= 9; i++) {
        res += countNum(N - 1, (sum + i) % K,
                        K, (st | i > 0), dp);
    }

    return dp[N][sum][st] = res;
}

// Driver Code

var N = 2, K = 7;

// Stores the values of
// overlapping subproblems
var dp = Array.from(Array(M), ()=>Array(M));
for(var i =0; i<M; i++)
        for(var j =0; j<M; j++)
            dp[i][j] = new Array(2).fill(-1);
document.write( countNum(N, 0, K, 0, dp));

</script>
```

**输出:**

```
12
```

***时间复杂度:** O(10*N*K)*

***辅助空间:** O(N*K)*