# 打印从 1 开始的图形在字典上最小的 DFS

> 原文： [https://www.geeksforgeeks.org/print-the-lexicographically-smallest-dfs-of-the-graph-starting-from-1/](https://www.geeksforgeeks.org/print-the-lexicographically-smallest-dfs-of-the-graph-starting-from-1/)

给定一个具有 **N 个顶点**和 **M 个边**的连通图。 任务是从 1 开始打印该图的按字典顺序最小的 DFS 遍历。

**示例：**

> **输入：** N = 5，M = 5，边缘[] = {{1，4}，{3，4}，{5，4}，{3，2}，{1，5} }
> **输出：** 1 4 3 2 5
> 
> **输入：** N = 5，M = 8，边缘[] = {{1，4}，{3，4}，{5，4}，{3，2}，{1，5} ，{1、2}，{1、3}，{3、5}}
> **输出：** 1 2 3 4 5

**方法：**而不是正常的 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，首先我们必须对每个顶点的边缘进行排序，以便在每个回合中仅首先选择最小的边缘。 排序后，只需执行正常的 DFS，这将提供字典上最小的 DFS 遍历。

下面是上述方法的实现：

## C ++

```

// C++ program to find the lexicographically 
// smallest traversal of a graph 
#include <bits/stdc++.h> 
using namespace std; 

// Utility function to add an 
// edge to the graph 
void insertEdges(int u, int v, vector<int>* adj) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// Function to perform DFS traversal 
void dfs(vector<int>* adj, int src, int n, 
         bool* visited) 
{ 
    // Print current vertex 
    cout << src << " "; 

    // Mark it as visited 
    visited[src] = true; 

    // Iterate over all the edges connected 
    // to this vertex 
    for (int i = 0; i < adj[src].size(); i++) { 
        // If this vertex is not visited, 
        /// call dfs from this node 
        if (!visited[adj[src][i]]) 
            dfs(adj, adj[src][i], n, visited); 
    } 
} 

// Function to print the lexicographically 
// smallest DFS 
void printLexoSmall(vector<int>* adj, int n) 
{ 
    // A boolean array to keep track of 
    // nodes visited 
    bool visited[n + 1] = { 0 }; 

    // Sort the edges of each vertex in 
    // ascending order 
    for (int i = 0; i < n; i++) 
        sort(adj[i].begin(), adj[i].end()); 

    // Call DFS 
    for (int i = 1; i < n; i++) { 
        if (!visited[i]) 
            dfs(adj, i, n, visited); 
    } 
} 

// Driver code 
int main() 
{ 
    int n = 5, m = 5; 
    vector<int> adj[n + 1]; 

    insertEdges(1, 4, adj); 
    insertEdges(3, 4, adj); 
    insertEdges(5, 4, adj); 
    insertEdges(3, 2, adj); 
    insertEdges(1, 5, adj); 
    insertEdges(1, 2, adj); 
    insertEdges(3, 5, adj); 
    insertEdges(1, 3, adj); 

    printLexoSmall(adj, n); 

    return 0; 
} 

```