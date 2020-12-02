# 无向图

的所有连接组件之间的最大边数

> 原文： [https://www.geeksforgeeks.org/maximum-number-of-edges-among-all-connected-components-of-an-undirected-graph/](https://www.geeksforgeeks.org/maximum-number-of-edges-among-all-connected-components-of-an-undirected-graph/)

给定整数'N'和'K'其中，N 是无向图的顶点数，'K'表示同一图中的边数（每个边由一对整数表示，其中 i，j 表示 顶点“ i”直接连接到图中的顶点“ j”）。

任务是在给定图中找到所有已连接组件中的最大边数。

**示例：**

> **输入：** N = 6，K = 4，
> 边沿= {{{1，2}，{2，3}，{3，1}，{4，5}}
> [ **输出：** 3
> 此处，图形具有 3 个分量
> 第 1 个分量 1-2-3-1：3 个边
> 第 2 个分量 4-5：1 个边
> 第 3 个分量 6： 0 个边
> max（3，1，0）= 3 个边
> 
> **输入：** N = 3，K = 2，
> 边沿= {{{1，2}，{2，3}}
> **输出：** 2

**方法：**

*   使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，分别找到所有连接组件中每个边的度数之和。
*   现在，根据[握手引理](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)，无向图的连接部分中的边总数等于其所有顶点度的总和的一半。
*   在所有连接的组件中打印最大数量的边。

下面是上述方法的实现：

## C ++

```

// C++ program to find the connected component 
// with maximum number of edges 
#include <bits/stdc++.h> 
using namespace std; 

// DFS function 
int dfs(int s, vector<int> adj[], vector<bool> visited, 
                                             int nodes) 
{ 
    // Adding all the edges connected to the vertex 
    int adjListSize = adj[s].size(); 
    visited[s] = true; 
    for (long int i = 0; i < adj[s].size(); i++) { 
        if (visited[adj[s][i]] == false) { 
            adjListSize += dfs(adj[s][i], adj, visited, nodes); 
        } 
    } 
    return adjListSize; 
} 

int maxEdges(vector<int> adj[], int nodes) 
{ 
    int res = INT_MIN; 
    vector<bool> visited(nodes, false); 
    for (long int i = 1; i <= nodes; i++) { 
        if (visited[i] == false) { 
            int adjListSize = dfs(i, adj, visited, nodes); 
            res = max(res, adjListSize/2); 
        }       
    } 
    return res; 
} 

// Driver code 
int main() 
{ 
    int nodes = 3; 
    vector<int> adj[nodes+1]; 

    // Edge from vertex 1 to vertex 2 
    adj[1].push_back(2); 
    adj[2].push_back(1); 

    // Edge from vertex 2 to vertex 3 
    adj[2].push_back(3); 
    adj[3].push_back(2); 

    cout << maxEdges(adj, nodes); 

    return 0; 
} 

```