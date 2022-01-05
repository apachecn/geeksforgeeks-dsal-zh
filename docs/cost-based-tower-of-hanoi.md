# 基于成本的河内塔

> 原文:[https://www.geeksforgeeks.org/cost-based-tower-of-hanoi/](https://www.geeksforgeeks.org/cost-based-tower-of-hanoi/)

标准的河内塔问题在这里解释。在标准问题中，所有的盘交易都被认为是相同的。给定一个 3×3 的矩阵成本[][]包含棒之间的盘转移成本，其中**成本[i][j]** 存储将盘从**棒 i** 转移到**棒 j** 的成本。同一杆之间的转移成本为 **0** 。因此成本矩阵的对角线元素都是**0**。任务是打印所有 **N** 盘从**杆 1** 转移到**杆 3** 的最小成本。
**例:**

> **输入:** N = 2
> 成本= {
> { 0，1，2}，
> { 2，0，1}，
> { 3，2，0}}
> **输出:** 4
> 有 2 个盘，小的在大的上。
> 将较小的圆盘从杆 1 转移到杆 2。
> 此转移的成本等于 1
> 将较大的圆盘从杆 1 转移到杆 3。
> 本次转账费用等于 2。
> 将较小的圆盘从杆 2 转移到杆 3。
> 本次转账费用等于 1
> 合计最低费用等于 4。
> **输入:** N = 3
> 成本= {
> { 0，1，2}，
> { 2，0，1}，
> { 3，2，0}}
> **输出:** 12

**方法:**思路是采用自顶向下[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。
假设**最小成本(idx，src，dest)** 是将 **idx** 到 **N** 的索引盘从**杆 src** 转移到**杆 dest** 的最小成本。既不是源棒也不是目的棒的第三棒的值为**rem = 6 –( I+j)**，因为棒号是 1、2 和 3，它们的和是 6。如果第一个和第三个杆分别是源杆和目的杆，那么辅助杆的编号为 6 –( 1+3)= 2。
现在将问题分解为如下子问题:

*   **情况 1:** 首先将所有带有索引 **(idx + 1)到 N** 的圆盘转移到剩余的杆上。现在将最大的光盘转移到目标棒。再次将剩余杆上的所有光盘转移到目标杆上。这个过程将花费。

> 成本=最小成本(idx + 1，src，rem) +成本[src][dest] +最小成本(idx + 1，rem，dest)

*   **情况 2:** 首先将所有带有索引 **(idx + 1)到 N** 的光盘转移到目的杆。现在将最大的圆盘转移到剩余的杆上。再次将所有光盘从目标棒转移到源棒。现在将最大的光盘从剩余棒转移到目标棒。再次将光盘从源棒转移到目标棒。这一过程的成本为:

> 成本 = mincost（idx + 1， src， dest） + cost[src][rem] + mincost（idx + 1， dest， src） + cost[row][dest] + mincost（idx + 1， src， dest）

*   答案将等于上述两种情况中的最小值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define RODS 3
#define N 3
int dp[N + 1][RODS + 1][RODS + 1];

// Function to initialize the dp table
void initialize()
{

    // Initialize with maximum value
    for (int i = 0; i <= N; i += 1) {
        for (int j = 1; j <= RODS; j++) {
            for (int k = 1; k <= RODS; k += 1) {
                dp[i][j][k] = INT_MAX;
            }
        }
    }
}
// Function to return the minimum cost
int mincost(int idx, int src, int dest,
            int costs[RODS][RODS])
{

    // Base case
    if (idx > N)
        return 0;

    // If problem is already solved,
    // return the pre-calculated answer
    if (dp[idx][src][dest] != INT_MAX)
        return dp[idx][src][dest];

    // Number of the auxiliary disk
    int rem = 6 - (src + dest);

    // Initialize the minimum cost as Infinity
    int ans = INT_MAX;

    // Calculationg the cost for first case
    int case1 = costs[src - 1][dest - 1]
                + mincost(idx + 1, src, rem, costs)
                + mincost(idx + 1, rem, dest, costs);

    // Calculating the cost for second case
    int case2 = costs[src - 1][rem - 1]
                + mincost(idx + 1, src, dest, costs)
                + mincost(idx + 1, dest, src, costs)
                + costs[rem - 1][dest - 1]
                + mincost(idx + 1, src, dest, costs);

    // Minimum of both the above cases
    ans = min(case1, case2);

    // Store it in the dp table
    dp[idx][src][dest] = ans;

    // Return the minimum cost
    return ans;
}

// Driver code
int main()
{
    int costs[RODS][RODS] = { { 0, 1, 2 },
                              { 2, 0, 1 },
                              { 3, 2, 0 } };
    initialize();
    cout << mincost(1, 1, 3, costs);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int RODS = 3;
static int N = 3;
static int [][][]dp=new int[N + 1][RODS + 1][RODS + 1];

// Function to initialize the dp table
static void initialize()
{

    // Initialize with maximum value
    for (int i = 0; i <= N; i += 1)
    {
        for (int j = 1; j <= RODS; j++)
        {
            for (int k = 1; k <= RODS; k += 1)
            {
                dp[i][j][k] = Integer.MAX_VALUE;
            }
        }
    }
}

// Function to return the minimum cost
static int mincost(int idx, int src, int dest,int costs[][])
{

    // Base case
    if (idx > N)
        return 0;

    // If problem is already solved,
    // return the pre-calculated answer
    if (dp[idx][src][dest] != Integer.MAX_VALUE)
        return dp[idx][src][dest];

    // Number of the auxiliary disk
    int rem = 6 - (src + dest);

    // Initialize the minimum cost as Infinity
    int ans = Integer.MAX_VALUE;

    // Calculationg the cost for first case
    int case1 = costs[src - 1][dest - 1]
                + mincost(idx + 1, src, rem, costs)
                + mincost(idx + 1, rem, dest, costs);

    // Calculating the cost for second case
    int case2 = costs[src - 1][rem - 1]
                + mincost(idx + 1, src, dest, costs)
                + mincost(idx + 1, dest, src, costs)
                + costs[rem - 1][dest - 1]
                + mincost(idx + 1, src, dest, costs);

    // Minimum of both the above cases
    ans = Math.min(case1, case2);

    // Store it in the dp table
    dp[idx][src][dest] = ans;

    // Return the minimum cost
    return ans;
}

// Driver code
public static void main (String[] args)
{

    int [][]costs = { { 0, 1, 2 },
                            { 2, 0, 1 },
                            { 3, 2, 0 } };
    initialize();
        System.out.print (mincost(1, 1, 3, costs));

}
}

// This code is contributed by ajit..23@
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np
import sys

RODS = 3
N = 3
dp = np.zeros((N + 1,RODS + 1,RODS + 1));

# Function to initialize the dp table
def initialize() :

    # Initialize with maximum value
    for i in range(N + 1) :
        for j in range(1, RODS + 1) :
            for k in range(1, RODS + 1) :
                dp[i][j][k] = sys.maxsize;

# Function to return the minimum cost
def mincost(idx, src, dest, costs) :

    # Base case
    if (idx > N) :
        return 0;

    # If problem is already solved,
    # return the pre-calculated answer
    if (dp[idx][src][dest] != sys.maxsize) :
        return dp[idx][src][dest];

    # Number of the auxiliary disk
    rem = 6 - (src + dest);

    # Initialize the minimum cost as Infinity
    ans = sys.maxsize;

    # Calculationg the cost for first case
    case1 = costs[src - 1][dest - 1] + mincost(idx + 1, src, rem, costs) + mincost(idx + 1, rem, dest, costs);

    # Calculating the cost for second case
    case2 = (costs[src - 1][rem - 1] + mincost(idx + 1, src, dest, costs) + mincost(idx + 1, dest, src, costs) + costs[rem - 1][dest - 1] + mincost(idx + 1, src, dest, costs));

    # Minimum of both the above cases
    ans = min(case1, case2);

    # Store it in the dp table
    dp[idx][src][dest] = ans;

    # Return the minimum cost
    return ans;

# Driver code
if __name__ == "__main__" :

    costs = [ [ 0, 1, 2 ],
            [ 2, 0, 1 ],
            [ 3, 2, 0 ] ];
    initialize();
    print(mincost(1, 1, 3, costs));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int RODS = 3;
static int N = 3;
static int [,,]dp=new int[N + 1,RODS + 1,RODS + 1];

// Function to initialize the dp table
static void initialize()
{

    // Initialize with maximum value
    for (int i = 0; i <= N; i += 1)
    {
        for (int j = 1; j <= RODS; j++)
        {
            for (int k = 1; k <= RODS; k += 1)
            {
                dp[i,j,k] = int.MaxValue;
            }
        }
    }
}

// Function to return the minimum cost
static int mincost(int idx, int src, int dest,int [,]costs)
{

    // Base case
    if (idx > N)
        return 0;

    // If problem is already solved,
    // return the pre-calculated answer
    if (dp[idx,src,dest] != int.MaxValue)
        return dp[idx,src,dest];

    // Number of the auxiliary disk
    int rem = 6 - (src + dest);

    // Initialize the minimum cost as Infinity
    int ans = int.MaxValue;

    // Calculationg the cost for first case
    int case1 = costs[src - 1,dest - 1]
                + mincost(idx + 1, src, rem, costs)
                + mincost(idx + 1, rem, dest, costs);

    // Calculating the cost for second case
    int case2 = costs[src - 1,rem - 1]
                + mincost(idx + 1, src, dest, costs)
                + mincost(idx + 1, dest, src, costs)
                + costs[rem - 1,dest - 1]
                + mincost(idx + 1, src, dest, costs);

    // Minimum of both the above cases
    ans = Math.Min(case1, case2);

    // Store it in the dp table
    dp[idx,src,dest] = ans;

    // Return the minimum cost
    return ans;
}

// Driver code
public static void Main (String[] args)
{

    int [,]costs = { { 0, 1, 2 },
                            { 2, 0, 1 },
                            { 3, 2, 0 } };
    initialize();
        Console.WriteLine(mincost(1, 1, 3, costs));

}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let RODS = 3;
    let N = 3;
    let dp = new Array(N + 1);

    // Function to initialize the dp table
    function initialize()
    {

        // Initialize with maximum value
        for (let i = 0; i <= N; i += 1)
        {
            dp[i] = new Array(RODS + 1);
            for (let j = 1; j <= RODS; j++)
            {
                dp[i][j] = new Array(RODS + 1);
                for (let k = 1; k <= RODS; k += 1)
                {
                    dp[i][j][k] = Number.MAX_VALUE;
                }
            }
        }
    }

    // Function to return the minimum cost
    function mincost(idx, src, dest, costs)
    {

        // Base case
        if (idx > N)
            return 0;

        // If problem is already solved,
        // return the pre-calculated answer
        if (dp[idx][src][dest] != Number.MAX_VALUE)
            return dp[idx][src][dest];

        // Number of the auxiliary disk
        let rem = 6 - (src + dest);

        // Initialize the minimum cost as Infinity
        let ans = Number.MAX_VALUE;

        // Calculationg the cost for first case
        let case1 = costs[src - 1][dest - 1]
                    + mincost(idx + 1, src, rem, costs)
                    + mincost(idx + 1, rem, dest, costs);

        // Calculating the cost for second case
        let case2 = costs[src - 1][rem - 1]
                    + mincost(idx + 1, src, dest, costs)
                    + mincost(idx + 1, dest, src, costs)
                    + costs[rem - 1][dest - 1]
                    + mincost(idx + 1, src, dest, costs);

        // Minimum of both the above cases
        ans = Math.min(case1, case2);

        // Store it in the dp table
        dp[idx][src][dest] = ans;

        // Return the minimum cost
        return ans;
    }

    let costs = [ [ 0, 1, 2 ],
                 [ 2, 0, 1 ],
                 [ 3, 2, 0 ] ];
    initialize();
      document.write(mincost(1, 1, 3, costs));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N)，其中 N 为给定棒中的圆盘数。