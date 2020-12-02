# 查找图形的最大值排列

> 原文： [https://www.geeksforgeeks.org/find-the-maximum-value-permutation-of-a-graph/](https://www.geeksforgeeks.org/find-the-maximum-value-permutation-of-a-graph/)

给定一个包含`N`个节点的图。 对于节点 **P <sub>1</sub> ，P <sub>2</sub> ，P <sub>3</sub> ，...，P <sub>N</sub>** 的任何置换 排列的数量定义为索引的数量，该索引在其左侧至少具有一个边缘的节点。 在所有排列中找到最大值。

**示例**：

> **输入**：N = 3，边缘[] = {{1，2}，{2，3}}
> **输出**：2
> 考虑置换 2 1 3
> 节点 1 在其左侧具有节点 2，并且在图中有一条边将其连接。
> 节点 3 在其左侧具有节点 2，并且在图中有一条边将其连接。
> 
> **输入**：N = 4，边缘[] = {{1，3}，{2，4}}
> **输出**：2
> 考虑排列 1 2 3 4
> 节点 3 在其左侧具有节点 1，并且在图中有一条边将其连接。
> 节点 4 在其左侧具有节点 2，并且在图中有一条边将其连接。

**方法**：让我们从头开始的任何节点开始，我们可以跟着其附近的任何节点进行跟踪，然后重复该过程。 这类似于 dfs 遍历，在该遍历中，除第一个节点外，每个节点之前都有一个与之共享边的节点。 因此，对于每个连接的组件，该组件的节点排列所能获得的最大值是**组件的大小– 1** 。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the number of nodes 
// in the current connected component 
int dfs(int x, vector<int> adj[], int vis[]) 
{ 
    // Initialise size to 1 
    int sz = 1; 

    // Mark the node as visited 
    vis[x] = 1; 

    // Start a dfs for every unvisited 
    // adjacent node 
    for (auto ch : adj[x]) 
        if (!vis[ch]) 
            sz += dfs(ch, adj, vis); 

    // Return the number of nodes in 
    // the current connected component 
    return sz; 
} 

// Function to return the maximum value 
// of the required permutation 
int maxValue(int n, vector<int> adj[]) 
{ 
    int val = 0; 
    int vis[n + 1] = { 0 }; 

    // For each connected component 
    // add the corresponding value 
    for (int i = 1; i <= n; i++) 
        if (!vis[i]) 
            val += dfs(i, adj, vis) - 1; 
    return val; 
} 

// Driver code 
int main() 
{ 
    int n = 3; 
    vector<int> adj[n + 1] = { { 1, 2 }, { 2, 3 } }; 
    cout << maxValue(n, adj); 

    return 0; 
} 

```