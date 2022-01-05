# 使用 STL 进行竞争性编程的图形实现|集合 1(未加权和无向的 DFS)

> 原文:[https://www . geesforgeks . org/graph-implementation-use-STL-for-competitive-programming-set-1-DFS-of-unweighted-and-directed/](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)

我们已经在[图形及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)中介绍了图形基础。在这篇文章中，使用了一种不同的基于 STL 的表示，这有助于使用[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)快速实现图形。实现是为了图的邻接表表示。
下面是一个有 5 个顶点的无向图和未加权图的例子。

![8](img/1ef79a5320e6115e8c3ada572164793e.png)

下面是图的邻接表表示。

![9 (1)](img/218bff5938529b5ffa08e970848d05ad.png)

我们在 STL 中使用向量来实现使用邻接表表示的图。

*   [载体:](https://www.geeksforgeeks.org/vector-in-cpp-stl/)一个序列容器。这里我们用它来存储所有顶点的邻接表。我们用顶点数作为这个向量的索引。

其思想是将一个图表示为一组向量，这样每个向量都表示一个顶点的邻接表。下面是一个完整的基于 STL 的 C++程序，用于 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。

## C++

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

    // Vertex numbers should be from 0 to 4.
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

## 蟒蛇 3

```
# A simple representation of graph using STL,
# for the purpose of competitive programming

# A utility function to add an edge in an
# undirected graph.
def addEdge(adj, u, v):
    adj[u].append(v)
    adj[v].append(u)
    return adj

# A utility function to do DFS of graph
# recursively from a given vertex u.
def DFSUtil(u, adj, visited):
    visited[u] = True
    print(u, end = " ")
    for i in range(len(adj[u])):
        if (visited[adj[u][i]] == False):
            DFSUtil(adj[u][i], adj, visited)

# This function does DFSUtil() for all
# unvisited vertices.
def DFS(adj, V):
    visited = [False]*(V+1)

    for u in range(V):
        if (visited[u] == False):
            DFSUtil(u, adj, visited)

# Driver code
if __name__ == '__main__':
    V = 5

    # The below line may not work on all
    # compilers.  If it does not work on
    # your compiler, please replace it with
    # following
    # vector<int> *adj = new vector<int>[V]
    adj = [[] for i in range(V)]

    # Vertex numbers should be from 0 to 4.
    adj = addEdge(adj, 0, 1)
    adj = addEdge(adj, 0, 4)
    adj = addEdge(adj, 1, 2)
    adj = addEdge(adj, 1, 3)
    adj = addEdge(adj, 1, 4)
    adj = addEdge(adj, 2, 3)
    adj = addEdge(adj, 3, 4)
    DFS(adj, V)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// A simple representation of graph using STL,
// for the purpose of competitive programming

    // A utility function to add an edge in an
// undirected graph.
    function addEdge(adj,u,v)
    {
        adj[u].push(v);
        adj[v].push(u);
    }

    // A utility function to do DFS of graph
// recursively from a given vertex u.
    function DFSUtil(u,adj,visited)
    {
        visited[u] = true;
        document.write(u+" ");
    for (let i=0; i<adj[u].length; i++)
        if (visited[adj[u][i]] == false)
            DFSUtil(adj[u][i], adj, visited);
    }

    // This function does DFSUtil() for all
// unvisited vertices.
    function DFS(adj,V)
    {
        let visited=new Array(V);
        for(let i=0;i<V;i++)
        {
            visited[i]=false;
        }
    for (let u=0; u<V; u++)
        if (visited[u] == false)
            DFSUtil(u, adj, visited);
    }

    // Driver code
    let V = 5;

    // The below line may not work on all
    // compilers.  If it does not work on
    // your compiler, please replace it with
    // following
    // vector<int> *adj = new vector<int>[V];
    let adj=new Array(V);
    for(let i=0;i<V;i++)
    {
        adj[i]=[];
    }

    // Vertex numbers should be from 0 to 4.
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 4);
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 1, 4);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    DFS(adj, V);

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
0 1 2 3 4
```

**下面是相关文章:**
[使用 STL 进行竞争编程的图实现| Set 2(加权图)](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)
[Dijkstra 的最短路径算法使用 STL 的 priority _ queue](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)
[Dijkstra 的最短路径算法使用 set in STL](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/)
[Kruskal 的最小生成树使用 STL in C++](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/)
[Prim 的算法使用 priority_queue in STL](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/) 如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息