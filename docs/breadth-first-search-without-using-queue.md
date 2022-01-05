# 不使用队列的广度优先搜索

> 原文:[https://www . geesforgeks . org/width-first-search-not-use-queue/](https://www.geeksforgeeks.org/breadth-first-search-without-using-queue/)

[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)是一种逐层遍历图或树的图遍历算法。在本文中， [BFS 对于一个图](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)是使用[邻接表](https://www.geeksforgeeks.org/prims-mst-for-adjacency-list-representation-greedy-algo-6/)实现的，而不使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)。
**举例:**

> **输入:**
> 
> ![](img/40ca76ea468053c881ac72e49e82f1e2.png)
> 
> **输出:** BFS 遍历= 2，0，3，1
> **说明:**
> 在下图中，我们从顶点 2 开始遍历。当我们到达顶点 0 时，我们寻找它的所有相邻顶点。2 也是 0 的相邻顶点。如果我们不标记访问过的顶点，那么 2 将被再次处理，并且它将成为一个不终止的过程。因此，下图的广度优先遍历是 2，0，3，1。

**方法:**这个问题可以通过使用来自给定源的简单广度优先遍历来解决。该实现使用 [**邻接表表示图形**](https://www.geeksforgeeks.org/prims-mst-for-adjacency-list-representation-greedy-algo-6/) 。
此处:

*   [STL Vector 容器](https://www.geeksforgeeks.org/vector-in-cpp-stl/)用于存储 BFS 遍历所需的相邻节点列表和节点队列。

*   一个 [**DP 数组**](https://www.geeksforgeeks.org/dynamic-programming/) 用来存储节点离源的距离。每次我们从一个节点移动到另一个节点，距离增加 1。如果到达节点的距离变得小于先前的距离，我们将更新存储在 DP[节点]中的值。

**以下是上述方法的实施:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to demonstrate
// the above mentioned approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the distance
// from the source to other nodes
void BFS(int curr, int N, vector<bool>& vis,
         vector<int>& dp, vector<int>& v,
         vector<vector<int> >& adj)
{

    while (curr <= N) {

        // Current node
        int node = v[curr - 1];
        cout << node << ", ";

        for (int i = 0; i < adj[node].size(); i++) {

            // Adjacent node
            int next = adj[node][i];

            if ((!vis[next])
                && (dp[next] < dp[node] + 1)) {

                // Stores the adjacent node
                v.push_back(next);

                // Increases the distance
                dp[next] = dp[node] + 1;

                // Mark it as visited
                vis[next] = true;
            }
        }
        curr += 1;
    }
}

// Function to print the distance
// from source to other nodes
void bfsTraversal(
    vector<vector<int> >& adj,
    int N, int source)
{
    // Initially mark all nodes as false
    vector<bool> vis(N + 1, false);

    // Initialize distance array with 0
    vector<int> dp(N + 1, 0), v;

    v.push_back(source);

    // Initially mark the starting
    // source as 0 and visited as true
    dp = 0;
    vis = true;

    // Call the BFS function
    BFS(1, N, vis, dp, v, adj);
}

// Driver code
int main()
{
    // No. of nodes in graph
    int N = 4;

    // Creating adjacency list
    // for representing graph
    vector<vector<int> > adj(N + 1);
    adj[0].push_back(1);
    adj[0].push_back(2);
    adj[1].push_back(2);
    adj[2].push_back(0);
    adj[2].push_back(3);
    adj[3].push_back(3);

    // Following is BFS Traversal
    // starting from vertex 2
    bfsTraversal(adj, N, 2);

    return 0;
}
```

## 蟒蛇 3

```
# C++ implementation to demonstrate
# the above mentioned approach
from queue import Queue

# Function to find the distance
# from the source to other nodes
def BFS(curr, N, vis,          dp,  v, adj):

    while (curr <= N) :

        # Current node
        node = v[curr - 1]
        print(node,end=  ", ")

        for i in range(len(adj[node])) :

            # Adjacent node
            next = adj[node][i]

            if ((not vis[next]) and (dp[next] < dp[node] + 1)) :

                # Stores the adjacent node
                v.append(next)

                # Increases the distance
                dp[next] = dp[node] + 1

                # Mark it as visited
                vis[next] = True

        curr += 1

# Function to prthe distance
# from source to other nodes
def bfsTraversal(adj,    N, source):
    # Initially mark all nodes as false
    vis=[False]*(N + 1)

    # Initialize distance array with 0
    dp=[0]*(N + 1); v=[]

    v.append(source)

    # Initially mark the starting
    # source as 0 and visited as true
    dp = 0
    vis = True

    # Call the BFS function
    BFS(1, N, vis, dp, v, adj)

# Driver code
if __name__ == '__main__':
    # No. of nodes in graph
    N = 4

    # Creating adjacency list
    # for representing graph
    adj=[[] for _ in range(N+1)]
    adj[0].append(1)
    adj[0].append(2)
    adj[1].append(2)
    adj[2].append(0)
    adj[2].append(3)
    adj[3].append(3)

    # Following is BFS Traversal
    # starting from vertex 2
    bfsTraversal(adj, N, 2)
```

**Output:** 

```
2, 0, 3, 1,
```

**时间复杂度:** O(V + E)，其中 V 为顶点数，E 为边数。
**辅助空间:** O(V)