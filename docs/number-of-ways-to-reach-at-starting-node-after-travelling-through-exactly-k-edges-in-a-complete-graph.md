# 在一个完整的图中通过 K 条边后到达起始节点的路数

> 原文:[https://www . geeksforgeeks . org/完整图中精确穿过 k 条边后到达起始节点的路径数/](https://www.geeksforgeeks.org/number-of-ways-to-reach-at-starting-node-after-travelling-through-exactly-k-edges-in-a-complete-graph/)

给定一个具有 **N** 节点和 **N*(N-1)/2** 边以及正整数 **K** 的[完整图](https://www.geeksforgeeks.org/graph-types-and-applications/)，任务是如果你从节点 **1** 开始，找到路的数量，如果必须遍历恰好 **K** 边，则在同一节点结束。

> **输入:** N = 4，K = 3
> **输出:** 6
> **说明:**可能的方式有-
> 1→2→3→1
> 1→2→4→1
> 1→3→2→1
> 1→3→4→1
> 1→4→2→1
> 1→4→3→1
> 
> **输入:** N = 5，K = 3
> T3】输出: 12

**天真方法:**解决这个问题最简单的方法是从当前顶点的每条边遍历，这会导致解是指数时间。

***时间复杂度:** O(N^N)*
***辅助空间:** O(N)，由于栈空间在*中对 [*递归函数*](https://www.geeksforgeeks.org/recursive-functions/) *调用。*

**有效方法:**该问题具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。所以这个问题可以用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)来解决。像其他典型的[动态规划](http://www.geeksforgeeks.org/dynamic-programming/) (DP)问题一样，可以通过构建存储子问题结果的临时数组来避免相同子问题的重新计算。按照以下步骤解决问题:

*   初始化一个 **dp[]** [数组](https://www.geeksforgeeks.org/array-data-structure/)，其中 **dp[i]** 用节点存储到达**的路数，并将 **dp[0]** 初始化为 **1。****
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，K】**中迭代，并执行以下步骤:
    *   将变量**初始化为 **0** 到**T5，存储到达所有节点的路径数。****
    *   [使用变量 **j、**在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，然后在 **numWays 中添加**DP【j】**。**
    *   [使用变量 **j、**在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，然后将**DP【j】**的值更新为**DP【j】**和**numWays–DP【j】**的最大值。
*   执行上述步骤后，打印**DP【0】**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find number of ways to
// reach from node 1 to 1 again, after
// moving exactly K edges
void numberOfWays(int n, int k)
{
    // Initialize a dp[] array, where dp[i]
    // stores number of ways to reach at
    // a i node
    int dp[1000];

    // Initialize the dp array with 0
    for (int i = 0; i < n; i++) {
        dp[i] = 0;
    }

    // Base Case
    dp[0] = 1;

    // Iterate for the number of edges moved
    for (int i = 1; i <= k; i++) {
        // Sum will store number of ways to
        // reach all the nodes
        int numWays = 0;

        // Iterate for every possible state
        // for the current step
        for (int j = 0; j < n; j++) {
            numWays += dp[j];
        }

        // Update the value of the dp array
        // after travelling each edge
        for (int j = 0; j < n; j++) {
            dp[j] = numWays - dp[j];
        }
    }

    // Print dp[0] as the answer
    cout << dp[0] << endl;
}

// Driver Code
int main()
{
    // Given Input
    int N = 5, K = 3;

    // Function Call
    numberOfWays(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find number of ways to
// reach from node 1 to 1 again, after
// moving exactly K edges
static void numberOfWays(int n, int k)
{

    // Initialize a dp[] array, where dp[i]
    // stores number of ways to reach at
    // a i node
    int[] dp = new int[1000];

    // Initialize the dp array with 0
    for(int i = 0; i < n; i++)
    {
        dp[i] = 0;
    }

    // Base Case
    dp[0] = 1;

    // Iterate for the number of edges moved
    for(int i = 1; i <= k; i++)
    {

        // Sum will store number of ways to
        // reach all the nodes
        int numWays = 0;

        // Iterate for every possible state
        // for the current step
        for(int j = 0; j < n; j++)
        {
            numWays += dp[j];
        }

        // Update the value of the dp array
        // after travelling each edge
        for(int j = 0; j < n; j++)
        {
            dp[j] = numWays - dp[j];
        }
    }

    // Print dp[0] as the answer
    System.out.println(dp[0] + "\n");
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int N = 5, K = 3;

    // Function Call
    numberOfWays(N, K);
}
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find number of ways to
# reach from node 1 to 1 again, after
# moving exactly K edges
def numberOfWays(n, k):

    # Initialize a dp[] array, where dp[i]
    # stores number of ways to reach at
    # a i node
    dp = [0 for i in range(1000)]

    # Base Case
    dp[0] = 1

    # Iterate for the number of edges moved
    for i in range(1, k + 1, 1):

        # Sum will store number of ways to
        # reach all the nodes
        numWays = 0

        # Iterate for every possible state
        # for the current step
        for j in range(n):
            numWays += dp[j]

        # Update the value of the dp array
        # after travelling each edge
        for j in range(n):
            dp[j] = numWays - dp[j]

    # Print dp[0] as the answer
    print(dp[0])

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 5
    K = 3

    # Function Call
    numberOfWays(N, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find number of ways to
// reach from node 1 to 1 again, after
// moving exactly K edges
static void numberOfWays(int n, int k)
{

    // Initialize a dp[] array, where dp[i]
    // stores number of ways to reach at
    // a i node
    int[] dp = new int[1000];

    // Initialize the dp array with 0
    for(int i = 0; i < n; i++)
    {
        dp[i] = 0;
    }

    // Base Case
    dp[0] = 1;

    // Iterate for the number of edges moved
    for(int i = 1; i <= k; i++)
    {

        // Sum will store number of ways to
        // reach all the nodes
        int numWays = 0;

        // Iterate for every possible state
        // for the current step
        for(int j = 0; j < n; j++)
        {
            numWays += dp[j];
        }

        // Update the value of the dp array
        // after travelling each edge
        for(int j = 0; j < n; j++)
        {
            dp[j] = numWays - dp[j];
        }
    }

    // Print dp[0] as the answer
    Console.Write(dp[0]);
}

// Driver Code
static public void Main ()
{

    // Given Input
    int N = 5, K = 3;

    // Function Call
    numberOfWays(N, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find number of ways to
// reach from node 1 to 1 again, after
// moving exactly K edges
function numberOfWays(n, k)
{

    // Initialize a dp[] array, where dp[i]
    // stores number of ways to reach at
    // a i node
    let dp = Array(1000);

    // Initialize the dp array with 0
    for(let i = 0; i < n; i++)
    {
        dp[i] = 0;
    }

    // Base Case
    dp[0] = 1;

    // Iterate for the number of edges moved
    for(let i = 1; i <= k; i++)
    {

        // Sum will store number of ways to
        // reach all the nodes
        let numWays = 0;

        // Iterate for every possible state
        // for the current step
        for(let j = 0; j < n; j++)
        {
            numWays += dp[j];
        }

        // Update the value of the dp array
        // after travelling each edge
        for(let j = 0; j < n; j++)
        {
            dp[j] = numWays - dp[j];
        }
    }

    // Print dp[0] as the answer
    document.write(dp[0]);
}

// Driver Code

// Given Input
let N = 5;
let K = 3;

// Function Call
numberOfWays(N, K);

</script>
```

**Output**

```
12
```

***时间复杂度:** O(N×K)*
***辅助空间:** O(N)*