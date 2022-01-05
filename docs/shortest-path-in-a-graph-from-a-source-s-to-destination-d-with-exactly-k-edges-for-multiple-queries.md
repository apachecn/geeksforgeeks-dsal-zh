# 图中从源 S 到目标 D 的最短路径，对于多个查询正好有 K 条边

> 原文:[https://www . geeksforgeeks . org/图中最短路径-从源 s 到目的地 d-精确 k 边-多查询/](https://www.geeksforgeeks.org/shortest-path-in-a-graph-from-a-source-s-to-destination-d-with-exactly-k-edges-for-multiple-queries/)

给定一个具有 **N** 个节点的图，一个节点 **S** 和 **Q** 个查询，每个查询都由一个节点 **D** 和 **K** 组成，任务是为每个查询找到恰好由 **K** 条边组成的从节点 **S** 到节点 **D** 的最短路径。如果不存在这样的路径，则打印 **-1** 。

**注:**T2 K 永远小于 **2 * N** 。

**示例:**

> **输入:** N = 3，边[][] = {{1，2，5}，{2，3，3}，{3，1，4}}，S = 1，Q = {{1，0}，{2，1}，{3，1}，{3，2}，{3，5}}
> **输出:** 0 5 -1 8 20
> 1。使用 0 边从 1 到 1 的最短路径将是 0。
> 2。使用 1 条边从 1 到 2 的最短路径将是 5，即 1- > 2。
> 3。节点 1 和 3 之间不存在 1 条边的路径。
> 4。使用 2 条边从 1 到 3 的最短路径将是 8，即 1- > 2- > 3。
> 5。使用 5 条边从 1 到 3 的最短路径将是 20，即 1->2->3->1->2->3。
> 
> **输入:** N = 4，边[][] = {{1，2，8}，{2，3，5}，{3，4，7}}，S = 1，Q = {{1，0}，{2，1}，{3，1}，{3，2}，{4，5}}
> **输出:** 0 8 -1 13 -1

**进场:**

*   这个问题可以借助[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)创建线性解来解决。
*   初始化一个[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，dp[N][2*N]，初始值为“inf”，除了 dp[S][0]为 0。
*   对该图进行预处理，以便为{0 到 N-1}之间的每个边长度找到每个节点到源的最短距离。数组 dp[][]将用于存储预处理的结果。
*   对于预处理，对[1，2*N-1]范围内的 J 运行一个循环，以找到图中每条边的 dp[X][J]，其中 **dp[X][J]** 是从节点“S”到节点“X”的最短路径，总共正好使用“J”条边。
*   借助于递推关系，我们可以找到 dp[X][J+1]:

> DP[edge . second][I]=**min**(DP[edge . second][I]，dp[ edge.first ][ i-1 ] +权重(edge))

*   对于 Q 中的每个查询，如果(dp[X][k] == inf)则返回-1，否则返回 dp[X][k]

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

#define inf 100000000

// Function to find the shortest path
// between S and D with exactly K edges
void ansQueries(int s,
                vector<pair<pair<int, int>, int> > ed,
                int n, vector<pair<int, int> > q)
{

    // To store the dp states
    int dp[n + 1][2 * n];

    // Initialising the dp[][] array
    for (int i = 0; i <= n; i++)
        dp[i][0] = inf;
    dp[s][0] = 0;

    // Pre-Processing
    for (int i = 1; i <= 2 * n - 1; i++) {

        // Initialising current state
        for (int j = 0; j <= n; j++)
            dp[j][i] = inf;

        // Updating current state
        for (auto it : ed) {
            dp[it.first.second][i]
                = min(
                    dp[it.first.second][i],
                    dp[it.first.first][i - 1] + it.second);
        }
    }

    for (int i = 0; i < q.size(); i++) {
        if (dp[q[i].first][q[i].second] == inf)
            cout << -1 << endl;
        else
            cout << dp[q[i].first][q[i].second]
                 << endl;
    }
}

// Driver code
int main()
{
    int n = 3;
    vector<pair<pair<int, int>, int> > ed;

    // Edges
    ed = { { { 1, 2 }, 5 },
           { { 2, 3 }, 3 },
           { { 3, 1 }, 4 } };

    // Source
    int s = 1;

    // Queries
    vector<pair<int, int> > q = { { 1, 0 },
                                  { 2, 1 },
                                  { 3, 1 },
                                  { 3, 2 },
                                  { 3, 5 } };

    // Function to answer queries
    ansQueries(s, ed, n, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static int inf = 100000000;

// Function to find the shortest path
// between S and D with exactly K edges
static void ansQueries(int s,
                       int[][] ed,
                int n, int[][] q)
{

    // To store the dp states
    int[][] dp = new int[n + 1][2 * n];

    // Initialising the dp[][] array
    for(int i = 0; i <= n; i++)
        dp[i][0] = inf;

    dp[s][0] = 0;

    // Pre-Processing
    for(int i = 1; i <= 2 * n - 1; i++)
    {

        // Initialising current state
        for(int j = 0; j <= n; j++)
            dp[j][i] = inf;

        // Updating current state
        for(int[] it : ed)
        {
            dp[it[1]][i] = Math.min(dp[it[1]][i],
                                    dp[it[0]][i - 1] +
                                       it[2]);
        }
    }

    for(int i = 0; i < q.length; i++)
    {
        if (dp[q[i][0]][q[i][1]] == inf) 
            System.out.println(-1); 
        else 
            System.out.println(dp[q[i][0]][q[i][1]]);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    // Edges
    int[][] ed = { { 1, 2, 5 },
                   { 2, 3, 3 },
                   { 3, 1, 4 } };

    // Source
    int s = 1;

    // Queries
    int[][] q = { { 1, 0 },
                  { 2, 1 },
                  { 3, 1 },
                  { 3, 2 },
                  { 3, 5 } };

    // Function to answer queries
    ansQueries(s, ed, n, q);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys,numpy as np

inf = sys.maxsize;

# Function to find the shortest path
# between S and D with exactly K edges
def ansQueries(s, ed, n, q) :

    # To store the dp states
    dp = np.zeros((n + 1, 2 * n));

    # Initialising the dp[][] array
    for i in range(n + 1) :
        dp[i][0] = inf;

    dp[s][0] = 0;

    # Pre-Processing
    for i in range( 1, 2 * n) :

        # Initialising current state
        for j in range( n + 1) :
            dp[j][i] = inf;

        # Updating current state
        for it in ed :
            dp[it[1]][i] = min( dp[it[1]][i],
                                dp[it[0]][i - 1] + ed[it]);

    for i in range(len(q)) :
        if (dp[q[i][0]][q[i][1]] == inf) :
            print(-1);
        else :
            print(dp[q[i][0]][q[i][1]]);

# Driver code
if __name__ == "__main__" :

    n = 3;

    # Edges
    ed = { ( 1, 2 ) : 5 ,
        ( 2, 3 ) : 3 ,
        ( 3, 1 ) : 4 };

    # Source
    s = 1;

    # Queries
    q = [
        ( 1, 0 ),
        ( 2, 1 ),
        ( 3, 1 ),
        ( 3, 2 ),
        ( 3, 5 )
        ];

    # Function to answer queries
    ansQueries(s, ed, n, q);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{
  static int inf = 100000000;

  // Function to find the shortest path
  // between S and D with exactly K edges
  static void ansQueries(int s, int[][] ed, int n, int[][] q)
  {

    // To store the dp states
    int[, ] dp = new int[n + 1, 2 * n];

    // Initialising the dp[][] array
    for (int i = 0; i <= n; i++)
      dp[i, 0] = inf;
    dp[s, 0] = 0;

    // Pre-Processing
    for (int i = 1; i <= 2 * n - 1; i++)
    {

      // Initialising current state
      for (int j = 0; j <= n; j++)
        dp[j, i] = inf;

      // Updating current state
      foreach (int[] it in ed)
      {
        dp[it[1], i] = Math.Min(dp[it[1], i],
                                dp[it[0], i - 1] + it[2]);
      }
    }

    for (int i = 0; i < q.Length; i++)
    {
      if (dp[q[i][0], q[i][1]] == inf)
        Console.WriteLine(-1);
      else
        Console.WriteLine(dp[q[i][0], q[i][1]]);
    }
  }

  // Driver code
  public static void Main(string[] args)
  {
    int n = 3;

    // Edges
    int[][] ed = {
      new int[3]{1, 2, 5},
      new int[3]{2, 3, 3},
      new int[3]{3, 1, 4}
    };

    // Source
    int s = 1;

    // Queries
    int[][] q = {
      new int[2]{1, 0},
      new int[2]{2, 1},
      new int[2]{3, 1},
      new int[2]{3, 2},
      new int[2]{3, 5}
    };

    // Function to answer queries
    ansQueries(s, ed, n, q);
  }
}   

// This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var inf = 100000000;

// Function to find the shortest path
// between S and D with exactly K edges
function ansQueries( s, ed, n,  q)
{

    // To store the dp states
    var dp = Array.from(Array(n+1), ()=> Array(2*n));

    // Initialising the dp[][] array
    for (var i = 0; i <= n; i++)
        dp[i][0] = inf;
    dp[s][0] = 0;

    // Pre-Processing
    for (var i = 1; i <= 2 * n - 1; i++) {

        // Initialising current state
        for (var j = 0; j <= n; j++)
            dp[j][i] = inf;

        // Updating current state
        for(var it =0; it<ed.length; it++)
        {
            dp[ed[it][0][1]][i]
                = Math.min(
                    dp[ed[it][0][1]][i],
                    dp[ed[it][0][0]][i - 1] + ed[it][1]);
        }
    }

    for (var i = 0; i < q.length; i++) {
        if (dp[q[i][0]][q[i][1]] == inf)
            document.write( -1+ "<br>" );
        else
            document.write( dp[q[i][0]][q[i][1]]+ "<br>");
    }
}

// Driver code
var n = 3;
var ed;
// Edges
ed = [ [ [ 1, 2 ], 5 ],
       [ [ 2, 3 ], 3 ],
       [ [ 3, 1 ], 4 ] ];
// Source
var s = 1;
// Queries
var q = [ [ 1, 0 ],
                              [ 2, 1 ],
                              [ 3, 1 ],
                              [ 3, 2 ],
                              [ 3, 5 ] ];
// Function to answer queries
ansQueries(s, ed, n, q);

</script>
```

**Output:** 

```
0
5
-1
8
20
```

**时间复杂度:**O(Q+N * E)
T3】空间复杂度: O(N*N)