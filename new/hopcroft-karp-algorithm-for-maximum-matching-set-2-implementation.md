# 用于最大匹配的 Hopcroft-Karp 算法| 第 2 组（实施）

> 原文： [https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-2-implementation/](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-2-implementation/)

我们强烈建议您先参考以下帖子。

[用于最大匹配的 Hopcroft-Karp 算法| 第 1 组（简介）](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-1-introduction/)

在开始实施之前，没有什么要注意的重要事情。

1.  我们需要**找到一个扩展路径**（在匹配边和不匹配边之间交替并且以自由顶点作为起点和终点的路径）。

2.  找到替代路径后，我们需要**将找到的路径添加到现有的 Matching** 中。 这里添加路径的意思是，使该路径上的先前匹配边为不匹配，而先前未匹配边为匹配。

这个想法是使用 BFS（宽度优先搜索）来查找增强路径。 由于 BFS 逐级遍历，因此它用于将图形划分为匹配的边和不匹配的边。 添加了一个虚拟顶点 NIL，该虚拟顶点 NIL 连接到左侧的所有顶点和右侧的所有顶点。 以下数组用于查找扩充路径。 到 NIL 的距离初始化为 INF（无限）。 如果我们从虚拟顶点开始，然后使用不同顶点的交替路径返回到虚拟顶点，那么就有一条增加路径。

1.  pairU []：大小为 m + 1 的数组，其中 m 是二分图左侧的顶点数。 pairU [u]如果 u 匹配则在右侧存储一对 u，否则存储 NIL。

2.  pairV []：大小为 n + 1 的数组，其中 n 是二分图右侧的顶点数。 pairV [v]如果 v 匹配，则在左侧存储 v 对，否则存储 NIL。

3.  dist []：大小为 m + 1 的数组，其中 m 是二分图左侧的顶点数。 如果 u 不匹配，则 dist [u]初始化为 0，否则初始化为 INF（无限）。 NIL 的 dist []也初始化为 INF

一旦找到扩展路径，就可以使用 DFS（深度优先搜索）将扩展路径添加到当前匹配中。 DFS 只需遵循 BFS 设置距离数组即可。 如果 v 在 BFS 中紧挨着 u，它将填充 pairU [u]和 pairV [v]中的值。

下面是上述 Hopkroft Karp 算法的 C++实现。

```

// C++ implementation of Hopcroft Karp algorithm for 
// maximum matching 
#include<bits/stdc++.h> 
using namespace std; 
#define NIL 0 
#define INF INT_MAX 

// A class to represent Bipartite graph for Hopcroft 
// Karp implementation 
class BipGraph 
{ 
    // m and n are number of vertices on left 
    // and right sides of Bipartite Graph 
    int m, n; 

    // adj[u] stores adjacents of left side 
    // vertex 'u'. The value of u ranges from 1 to m. 
    // 0 is used for dummy vertex 
    list<int> *adj; 

    // These are basically pointers to arrays needed 
    // for hopcroftKarp() 
    int *pairU, *pairV, *dist; 

public: 
    BipGraph(int m, int n); // Constructor 
    void addEdge(int u, int v); // To add edge 

    // Returns true if there is an augmenting path 
    bool bfs(); 

    // Adds augmenting path if there is one beginning 
    // with u 
    bool dfs(int u); 

    // Returns size of maximum matcing 
    int hopcroftKarp(); 
}; 

// Returns size of maximum matching 
int BipGraph::hopcroftKarp() 
{ 
    // pairU[u] stores pair of u in matching where u 
    // is a vertex on left side of Bipartite Graph. 
    // If u doesn't have any pair, then pairU[u] is NIL 
    pairU = new int[m+1]; 

    // pairV[v] stores pair of v in matching. If v 
    // doesn't have any pair, then pairU[v] is NIL 
    pairV = new int[n+1]; 

    // dist[u] stores distance of left side vertices 
    // dist[u] is one more than dist[u'] if u is next 
    // to u'in augmenting path 
    dist = new int[m+1]; 

    // Initialize NIL as pair of all vertices 
    for (int u=0; u<=m; u++) 
        pairU[u] = NIL; 
    for (int v=0; v<=n; v++) 
        pairV[v] = NIL; 

    // Initialize result 
    int result = 0; 

    // Keep updating the result while there is an 
    // augmenting path. 
    while (bfs()) 
    { 
        // Find a free vertex 
        for (int u=1; u<=m; u++) 

            // If current vertex is free and there is 
            // an augmenting path from current vertex 
            if (pairU[u]==NIL && dfs(u)) 
                result++; 
    } 
    return result; 
} 

// Returns true if there is an augmenting path, else returns 
// false 
bool BipGraph::bfs() 
{ 
    queue<int> Q; //an integer queue 

    // First layer of vertices (set distance as 0) 
    for (int u=1; u<=m; u++) 
    { 
        // If this is a free vertex, add it to queue 
        if (pairU[u]==NIL) 
        { 
            // u is not matched 
            dist[u] = 0; 
            Q.push(u); 
        } 

        // Else set distance as infinite so that this vertex 
        // is considered next time 
        else dist[u] = INF; 
    } 

    // Initialize distance to NIL as infinite 
    dist[NIL] = INF; 

    // Q is going to contain vertices of left side only.  
    while (!Q.empty()) 
    { 
        // Dequeue a vertex 
        int u = Q.front(); 
        Q.pop(); 

        // If this node is not NIL and can provide a shorter path to NIL 
        if (dist[u] < dist[NIL]) 
        { 
            // Get all adjacent vertices of the dequeued vertex u 
            list<int>::iterator i; 
            for (i=adj[u].begin(); i!=adj[u].end(); ++i) 
            { 
                int v = *i; 

                // If pair of v is not considered so far 
                // (v, pairV[V]) is not yet explored edge. 
                if (dist[pairV[v]] == INF) 
                { 
                    // Consider the pair and add it to queue 
                    dist[pairV[v]] = dist[u] + 1; 
                    Q.push(pairV[v]); 
                } 
            } 
        } 
    } 

    // If we could come back to NIL using alternating path of distinct 
    // vertices then there is an augmenting path 
    return (dist[NIL] != INF); 
} 

// Returns true if there is an augmenting path beginning with free vertex u 
bool BipGraph::dfs(int u) 
{ 
    if (u != NIL) 
    { 
        list<int>::iterator i; 
        for (i=adj[u].begin(); i!=adj[u].end(); ++i) 
        { 
            // Adjacent to u 
            int v = *i; 

            // Follow the distances set by BFS 
            if (dist[pairV[v]] == dist[u]+1) 
            { 
                // If dfs for pair of v also returns 
                // true 
                if (dfs(pairV[v]) == true) 
                { 
                    pairV[v] = u; 
                    pairU[u] = v; 
                    return true; 
                } 
            } 
        } 

        // If there is no augmenting path beginning with u. 
        dist[u] = INF; 
        return false; 
    } 
    return true; 
} 

// Constructor 
BipGraph::BipGraph(int m, int n) 
{ 
    this->m = m; 
    this->n = n; 
    adj = new list<int>[m+1]; 
} 

// To add edge from u to v and v to u 
void BipGraph::addEdge(int u, int v) 
{ 
    adj[u].push_back(v); // Add u to v’s list. 
} 

// Driver Program 
int main() 
{ 
    BipGraph g(4, 4); 
    g.addEdge(1, 2); 
    g.addEdge(1, 3); 
    g.addEdge(2, 1); 
    g.addEdge(3, 2); 
    g.addEdge(4, 2); 
    g.addEdge(4, 4); 

    cout << "Size of maximum matching is " << g.hopcroftKarp(); 

    return 0; 
} 

```

输出：

```
Size of maximum matching is 4
```

以上实现主要是从 [Hopcroft Karp 算法](https://en.wikipedia.org/wiki/Hopcroft%E2%80%93Karp_algorithm)的 Wiki 页面提供的算法中采用的。

本文由 **Rahul Gupta** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

