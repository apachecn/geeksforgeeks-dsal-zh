# 火车站| TCS CodeVita 2020

> 原文:[https://www . geesforgeks . org/railway-station-TCS-codevita-2020/](https://www.geeksforgeeks.org/railway-station-tcs-codevita-2020/)

给定一个整数 **N** ，表示位于源和目的地之间的站点数量。每个车站有三列可用列车，其停运模式如下:

*   **1 次列车:**在各站停靠
*   **2 号列车:**在每个备降站停靠
*   **3 次列车:**每三站停一次

任务是找到使用任何可能的火车组合从源头到达目的地的方法数量。

**示例:**

> **输入:** N = 2
> **输出:** 4
> **解释:**
> 有 4 种可能的方式从出发地前往目的地，中间有 2 个车站:
> 1 号列车(出发地)—>1 号列车(出发地 1 号车站)—>1 号列车(出发地 2 号车站)—>目的地
> 2 号列车(出发地)—>1 号列车(出发地 2 号车站)—>目的地
> 1 号列车(出发地)—【T11 号列车
> 
> **输入:** N = 0
> **输出:** 1
> **解释:**在源和目的地之间不存在车站。所以出行方式只有一种，即
> 1 次列车(出发地)—>目的地

**方法:**解决问题的主要思路是用[递归](https://www.geeksforgeeks.org/recursion/)配合[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来解决这个问题。循环关系如下:

> **F(N)= F(N–1)+F(N–2)+F(N–3)，**
> 
> 其中，
> **F(N–1)**计算到达(N–1)<sup>第</sup>站的方式。
> **F(N–2)**计算到达(N–2)<sup>第</sup>站的行程。
> **F(N–3)**计算到达(N–3)<sup>第</sup>站的行程。

按照以下步骤解决问题:

1.  初始化数组 **dp[]** 进行记忆。最初将所有指数设置为 **-1** 。
2.  定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)**find way()**来计算到达**N**T6 站的路数。
3.  需要考虑以下基本情况:
    *   对于 **x < 0** 返回 **0。**
    *   对于 **x = 0** ，返回 **1。**
    *   对于 **x = 1** ，返回 **2。**
    *   对于 **x = 2，**返回 **4。**
4.  如果当前状态，比如 **x** ，已经评估，即 **dp[x]** 不等于 **-1** ，只需返回评估值即可。
5.  否则，递归计算**find way(x–1)**、**find way(x–2)**和**find way(x–3)**，并将它们的和存储在**DP【x】**中。
6.  返回 **dp[x]** 。

下面是上述方法的实现:

## C++14

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Dp table for memoization
int dp[100000];

// Function to count the number
// of ways to N-th station
int findWays(int x)
{
    // Base Cases
    if (x < 0)
        return 0;

    if (x == 0)
        return 1;

    if (x == 1)
        return 2;

    if (x == 2)
        return 4;

    // If current state is
    // already evaluated
    if (dp[x] != -1)
        return dp[x];

    // Recursive calls

    // Count ways in which
    // train 1 can be chosen
    int count = findWays(x - 1);

    // Count ways in which
    // train 2 can be chosen
    count += findWays(x - 2);

    // Count ways in which
    // train 3 can be chosen
    count += findWays(x - 3);

    // Store the current state
    dp[x] = count;

    // Return the number of ways
    return dp[x];
}

// Driver Code
int main()
{

    // Given Input
    int n = 4;

    // Initialize DP table with -1
    memset(dp, -1, sizeof(dp));

    // Function call to count
    // the number of ways to
    // reach the n-th station
    cout << findWays(n) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Dp table for memoization
  static int dp[] = new int[100000];

  // Function to count the number
  // of ways to N-th station
  static int findWays(int x)
  {

    // Base Cases
    if (x < 0)
      return 0;

    if (x == 0)
      return 1;

    if (x == 1)
      return 2;

    if (x == 2)
      return 4;

    // If current state is
    // already evaluated
    if (dp[x] != -1)
      return dp[x];

    // Recursive calls

    // Count ways in which
    // train 1 can be chosen
    int count = findWays(x - 1);

    // Count ways in which
    // train 2 can be chosen
    count += findWays(x - 2);

    // Count ways in which
    // train 3 can be chosen
    count += findWays(x - 3);

    // Store the current state
    dp[x] = count;

    // Return the number of ways
    return dp[x];
  }

  // Driven Code
  public static void main(String[] args)
  {

    // Given Input
    int n = 4;

    // Initialize DP table with -1
    Arrays.fill(dp, -1);

    // Function call to count
    // the number of ways to
    // reach the n-th station
    System.out.print(findWays(n));
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Dp table for memoization
dp = [-1 for i in range(100000)]

# Function to count the number
# of ways to N-th station
def findWays(x):

    # Base Cases
    if (x < 0):
        return 0

    if (x == 0):
        return 1

    if (x == 1):
        return 2

    if (x == 2):
        return 4

    # If current state is
    # already evaluated
    if (dp[x] != -1):
        return dp[x]

    # Recursive calls

    # Count ways in which
    # train 1 can be chosen
    count = findWays(x - 1)

    # Count ways in which
    # train 2 can be chosen
    count += findWays(x - 2)

    # Count ways in which
    # train 3 can be chosen
    count += findWays(x - 3)

    # Store the current state
    dp[x] = count

    # Return the number of ways
    return dp[x]

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 4

    # Function call to count
    # the number of ways to
    # reach the n-th station
    print(findWays(n))

# This code is contributed by SURENDRA_GANGWAR
```

**Output:** 

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)