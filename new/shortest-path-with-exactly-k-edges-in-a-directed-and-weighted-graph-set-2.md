# 在有向图和加权图中具有恰好 k 个边的最短路径| 设置 2

> 原文： [https://www.geeksforgeeks.org/shortest-path-with-exactly-k-edges-in-a-directed-and-weighted-graph-set-2/](https://www.geeksforgeeks.org/shortest-path-with-exactly-k-edges-in-a-directed-and-weighted-graph-set-2/)

给定有向加权图和其中两个顶点`S`和`D`，任务是找到从`S`到`D`的最短路径。 路径上正好`K`个边。 如果不存在这样的路径，则打印-1。

**示例**：

> **输入**：N = 3，K = 2，ed = {{{{1，2}，5}，{{2，3}，3}，{{3，1}，4}}， S = 1，D = 3
> **输出**：8
> **说明**：具有两个边的最短路径将是 1- > 2- > 3
> 
> **输入**：N = 3，K = 4，ed = {{{{1，2}，5}，{{2，3}，3}，{{3，1}，4}}， S = 1，D = 3
> **输出**：-1
> **说明**：从节点 1 到 3 都不存在边长为 4 的路径
> 
> **输入**：N = 3，K = 5，ed = {{{{1，2}，5}，{{2，3}，3}，{{3，1}，4}}， S = 1，D = 3
> **输出**：20
> **说明**：最短路径为 1- > 2- > 3- > 1 -> 2- > 3。

**方法**：针对该问题的 **O（V ^ 3 * K）**方法已在[先前的文章中进行了讨论。](https://www.geeksforgeeks.org/shortest-path-exactly-k-edges-directed-weighted-graph/) 在本文中，讨论了用于解决此问题的 **O（E * K）**方法。
的想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决此问题。

设 dp [X] [J]为从节点`S`到节点`X`的最短路径，总共使用正好`J`边。 使用此方法，可以将 dp [X] [J + 1]计算为：

```
dp[X][J+1] = min(arr[Y][J]+weight[{Y, X}])
for all Y which has an edge from Y to X.

```

可以通过以下步骤计算问题的结果：

1.  初始化一个数组，dis []的初始值为'inf'，但 dis [S]的值为 0。
2.  当我等于 1 – K 时，运行一个循环
    *   初始化一个数组 dis1 []，其初始值为'inf'。
    *   对于图中的每个边，
        dis1 [edge.second] = min（dis1 [edge.second]，dis [edge.first] + weight（edge））
3.  如果 dist [d]为无穷大，则返回-1，否则返回 dist [d]。

下面是上述方法的实现：

## CPP

```

// C++ implementation of the above approach 
#include <bits/stdc++.h> 
#define inf 100000000 
using namespace std; 

// Function to find the smallest path 
// with exactly K edges 
double smPath(int s, int d, 
              vector<pair<pair<int, int>, int> > ed, 
              int n, int k) 
{ 
    // Array to store dp 
    int dis[n + 1]; 

    // Initialising the array 
    for (int i = 0; i <= n; i++) 
        dis[i] = inf; 
    dis[s] = 0; 

    // Loop to solve DP 
    for (int i = 0; i < k; i++) { 

        // Initialising next state 
        int dis1[n + 1]; 
        for (int j = 0; j <= n; j++) 
            dis1[j] = inf; 

        // Recurrence relation 
        for (auto it : ed) 
            dis1[it.first.second] = min(dis1[it.first.second], 
                                        dis[it.first.first] 
                                            + it.second); 
        for (int i = 0; i <= n; i++) 
            dis[i] = dis1[i]; 
    } 

    // Returning final answer 
    if (dis[d] == inf) 
        return -1; 
    else
        return dis[d]; 
} 

// Driver code 
int main() 
{ 

    int n = 4; 
    vector<pair<pair<int, int>, int> > ed; 

    // Input edges 
    ed = { { { 0, 1 }, 10 }, 
           { { 0, 2 }, 3 }, 
           { { 0, 3 }, 2 }, 
           { { 1, 3 }, 7 }, 
           { { 2, 3 }, 7 } }; 

    // Source and Destination 
    int s = 0, d = 3; 

    // Number of edges in path 
    int k = 2; 

    // Calling the function 
    cout << smPath(s, d, ed, n, k); 
} 

```