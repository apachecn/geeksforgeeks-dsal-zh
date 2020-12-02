# 使用 STL 进行竞争性编程的图形实现| 设置 1（未加权和无向的 DFS）

> 原文： [https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)

我们在[图及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)中介绍了图基础。 在本文中，将使用基于 STL 的不同表示形式，这有助于使用[向量](http://quiz.geeksforgeeks.org/vector-sequence-containers-the-c-standard-template-library-stl-set-1/)快速实现图形。 该实现用于图形的邻接表表示。

以下是具有 5 个顶点的示例无向图和无权图。
![8](img/1ef79a5320e6115e8c3ada572164793e.png)

下面是该图的邻接列表表示。
![9 (1)](img/218bff5938529b5ffa08e970848d05ad.png)

我们在 STL 中使用向量来使用邻接表表示实现图形。

*   [vector：](http://quiz.geeksforgeeks.org/vector-sequence-containers-the-c-standard-template-library-stl-set-1/)一个序列容器。 在这里，我们使用它来存储所有顶点的邻接列表。 我们使用顶点数作为该向量的索引。

想法是将图表示为向量数组，以使每个向量都表示顶点的邻接表。 以下是用于 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)的完整的基于 STL 的 C ++程序。

```

// A simple representation of graph using STL, 
// for the purpose of competitive programming 
#include<bits/stdc++.h> 
using namespace std; 

// A utility function to add an edge in an 
// undirected graph. 
void addEdge(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// A utility function to do DFS of graph 
// recursively from a given vertex u. 
void DFSUtil(int u, vector<int> adj[], 
                    vector<bool> &visited) 
{ 
    visited[u] = true; 
    cout << u << " "; 
    for (int i=0; i<adj[u].size(); i++) 
        if (visited[adj[u][i]] == false) 
            DFSUtil(adj[u][i], adj, visited); 
} 

// This function does DFSUtil() for all  
// unvisited vertices. 
void DFS(vector<int> adj[], int V) 
{ 
    vector<bool> visited(V, false); 
    for (int u=0; u<V; u++) 
        if (visited[u] == false) 
            DFSUtil(u, adj, visited); 
} 

// Driver code 
int main() 
{ 
    int V = 5; 

    // The below line may not work on all 
    // compilers.  If it does not work on 
    // your compiler, please replace it with 
    // following 
    // vector<int> *adj = new vector<int>[V]; 
    vector<int> adj[V]; 

    // Vertex numbers should be from 0 to 4\. 
    addEdge(adj, 0, 1); 
    addEdge(adj, 0, 4); 
    addEdge(adj, 1, 2); 
    addEdge(adj, 1, 3); 
    addEdge(adj, 1, 4); 
    addEdge(adj, 2, 3); 
    addEdge(adj, 3, 4); 
    DFS(adj, V); 
    return 0; 
} 

```

输出：

```
0 1 2 3 4
```

**以下是相关文章**：
[使用 STL 进行竞争性编程的图形实现| 集合 2（加权图）](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)
[使用 STL 的 priority_queue 的 Dijkstra 最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)
[使用 STL 中的集的 Dijkstra 最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/)
[Kruskal 的 在 C ++中使用 STL 的最小生成树](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/)
[在 STL](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/) 中使用 priority_queue 的 Prim 算法

本文由 **Shubham Gupta** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)