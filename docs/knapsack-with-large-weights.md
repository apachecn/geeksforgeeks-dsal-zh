# 大重量背包

> 原文:[https://www.geeksforgeeks.org/knapsack-with-large-weights/](https://www.geeksforgeeks.org/knapsack-with-large-weights/)

给定一个容量为 **C** 的背包和两个代表 **N** 不同物品的重量和价值的数组**w【】**和**val【】**，任务是找到你能放入背包的最大值。物品不可破，重量为 **X** 的物品占背包 **X** 的容量。

**示例:**

> **输入:** w[] = {3，4，5}，val[] = {30，50，60}，C = 8
> **输出:** 90
> 我们取对象‘1’和‘3’。
> 我们得到的总值是(30 + 60) = 90。
> 总重量为 8，因此符合给定的容量
> 
> **输入:** w[] = {10000}，val[] = {10}，C = 100000
> T3】输出: 10

**方法:**传统著名的 [0-1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题可以在 O(N*C)时间内解决，但是如果背包容量巨大，那么 2D N*C 阵列就无法制作。幸运的是，可以通过重新定义 dp 的状态来解决这个问题。
我们先来看看民主党的状态。
**DP【V】【I】**代表获得至少 **V** 值所需的子阵列**arr【I…N-1】**的最小权重子集。循环关系为:

> dp[V][i] = min（dp[V][i+1]， w[i] + dp[V – val[i]][i + 1]）

因此，对于从 **0** 到 **V** 可能的最大值的每个 **V** ，尝试找出给定的 **V** 是否可以用给定的数组来表示。能代表的最大的这样的 **V** 就成了必答。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define V_SUM_MAX 1000
#define N_MAX 100
#define W_MAX 10000000

// To store the states of DP
int dp[V_SUM_MAX + 1][N_MAX];
bool v[V_SUM_MAX + 1][N_MAX];

// Function to solve the recurrence relation
int solveDp(int r, int i, vector<int>& w, vector<int>& val, int n)
{
    // Base cases
    if (r <= 0)
        return 0;
    if (i == n)
        return W_MAX;
    if (v[r][i])
        return dp[r][i];

    // Marking state as solved
    v[r][i] = 1;

    // Recurrence relation
    dp[r][i]
        = min(solveDp(r, i + 1, w, val, n),
              w[i] + solveDp(r - val[i],
                             i + 1, w, val, n));
    return dp[r][i];
}

// Function to return the maximum weight
int maxWeight(vector<int>& w, vector<int>& val, int n, int c)
{

    // Iterating through all possible values
    // to find the the largest value that can
    // be represented by the given weights
    for (int i = V_SUM_MAX; i >= 0; i--) {
        if (solveDp(i, 0, w, val, n) <= c) {
            return i;
        }
    }
    return 0;
}

// Driver code
int main()
{
    vector<int> w = { 3, 4, 5 };
    vector<int> val = { 30, 50, 60 };
    int n = (int)w.size();
    int C = 8;

    cout << maxWeight(w, val, n, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int V_SUM_MAX = 1000;
    static final int N_MAX = 100;
    static final int W_MAX = 10000000;

    // To store the states of DP
    static int dp[][] = new int[V_SUM_MAX + 1][N_MAX];
    static boolean v[][] = new boolean [V_SUM_MAX + 1][N_MAX];

    // Function to solve the recurrence relation
    static int solveDp(int r, int i, int w[],      
                          int val[], int n)
    {
        // Base cases
        if (r <= 0)
            return 0;

        if (i == n)
            return W_MAX;

        if (v[r][i])
            return dp[r][i];

        // Marking state as solved
        v[r][i] = true;

        // Recurrence relation
        dp[r][i] = Math.min(solveDp(r, i + 1, w, val, n),
                     w[i] + solveDp(r - val[i],
                                    i + 1, w, val, n));

        return dp[r][i];
    }

    // Function to return the maximum weight
    static int maxWeight(int w[], int val[],
                         int n, int c)
    {

        // Iterating through all possible values
        // to find the the largest value that can
        // be represented by the given weights
        for (int i = V_SUM_MAX; i >= 0; i--)
        {
            if (solveDp(i, 0, w, val, n) <= c)
            {
                return i;
            }
        }
        return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        int w[] = { 3, 4, 5 };
        int val[] = { 30, 50, 60 };
        int n = w.length;
        int C = 8;

        System.out.println(maxWeight(w, val, n, C));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
V_SUM_MAX = 1000
N_MAX = 100
W_MAX = 10000000

# To store the states of DP
dp = [[ 0 for i in range(N_MAX)]
          for i in range(V_SUM_MAX + 1)]
v = [[ 0 for i in range(N_MAX)]
         for i in range(V_SUM_MAX + 1)]

# Function to solve the recurrence relation
def solveDp(r, i, w, val, n):

    # Base cases
    if (r <= 0):
        return 0
    if (i == n):
        return W_MAX
    if (v[r][i]):
        return dp[r][i]

    # Marking state as solved
    v[r][i] = 1

    # Recurrence relation
    dp[r][i] = min(solveDp(r, i + 1, w, val, n),
            w[i] + solveDp(r - val[i], i + 1,
                            w, val, n))
    return dp[r][i]

# Function to return the maximum weight
def maxWeight( w, val, n, c):

    # Iterating through all possible values
    # to find the the largest value that can
    # be represented by the given weights
    for i in range(V_SUM_MAX, -1, -1):
        if (solveDp(i, 0, w, val, n) <= c):
            return i

    return 0

# Driver code
if __name__ == '__main__':
    w = [3, 4, 5]
    val = [30, 50, 60]
    n = len(w)
    C = 8

    print(maxWeight(w, val, n, C))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static readonly int V_SUM_MAX = 1000;
    static readonly int N_MAX = 100;
    static readonly int W_MAX = 10000000;

    // To store the states of DP
    static int [,]dp = new int[V_SUM_MAX + 1, N_MAX];
    static bool [,]v = new bool [V_SUM_MAX + 1, N_MAX];

    // Function to solve the recurrence relation
    static int solveDp(int r, int i, int []w,    
                       int []val, int n)
    {
        // Base cases
        if (r <= 0)
            return 0;

        if (i == n)
            return W_MAX;

        if (v[r, i])
            return dp[r, i];

        // Marking state as solved
        v[r, i] = true;

        // Recurrence relation
        dp[r, i] = Math.Min(solveDp(r, i + 1, w, val, n),
                     w[i] + solveDp(r - val[i],
                                    i + 1, w, val, n));

        return dp[r, i];
    }

    // Function to return the maximum weight
    static int maxWeight(int []w, int []val,
                         int n, int c)
    {

        // Iterating through all possible values
        // to find the the largest value that can
        // be represented by the given weights
        for (int i = V_SUM_MAX; i >= 0; i--)
        {
            if (solveDp(i, 0, w, val, n) <= c)
            {
                return i;
            }
        }
        return 0;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []w = { 3, 4, 5 };
        int []val = { 30, 50, 60 };
        int n = w.Length;
        int C = 8;

        Console.WriteLine(maxWeight(w, val, n, C));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var V_SUM_MAX = 1000
var N_MAX = 100
var W_MAX = 10000000

// To store the states of DP
var dp = Array.from(Array(V_SUM_MAX+1), ()=> Array(N_MAX));
var v = Array.from(Array(V_SUM_MAX+1), ()=> Array(N_MAX));

// Function to solve the recurrence relation
function solveDp(r, i, w, val, n)
{
    // Base cases
    if (r <= 0)
        return 0;
    if (i == n)
        return W_MAX;
    if (v[r][i])
        return dp[r][i];

    // Marking state as solved
    v[r][i] = 1;

    // Recurrence relation
    dp[r][i]
        = Math.min(solveDp(r, i + 1, w, val, n),
              w[i] + solveDp(r - val[i],
                             i + 1, w, val, n));
    return dp[r][i];
}

// Function to return the maximum weight
function maxWeight(w, val, n, c)
{

    // Iterating through all possible values
    // to find the the largest value that can
    // be represented by the given weights
    for (var i = V_SUM_MAX; i >= 0; i--) {
        if (solveDp(i, 0, w, val, n) <= c) {
            return i;
        }
    }
    return 0;
}

// Driver code
var w = [3, 4, 5];
var val = [30, 50, 60];
var n = w.length;
var C = 8;
document.write( maxWeight(w, val, n, C));

</script>
```

**Output:** 

```
90
```

**时间复杂度:** O(V_sum * N)，其中 V_sum 是数组 val[]中所有值的和。

**辅助空间:** O(V_sum * N)其中 V_sum 是数组 val[]中所有值的和。