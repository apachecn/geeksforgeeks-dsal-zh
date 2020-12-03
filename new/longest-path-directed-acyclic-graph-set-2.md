# 有向无环图中的最长路径 设置 2

> 原文： [https://www.geeksforgeeks.org/longest-path-directed-acyclic-graph-set-2/](https://www.geeksforgeeks.org/longest-path-directed-acyclic-graph-set-2/)

给定加权有向无环图（DAG）和其中的源顶点，找到给定图中从源顶点到所有其他顶点的最长距离。

我们已经讨论了如何在集合 1 中找到有向无环图（DAG）中的[最长路径。在本文中，我们将讨论另一种有趣的解决方案，以使用算法来查找](https://www.geeksforgeeks.org/find-longest-path-directed-acyclic-graph/)[来找到 DAG 的最长路径。 ] DAG](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/) 中的最短路径。

想法是**否定路径的权重并在图形**中找到最短路径。 加权图 G 中两个给定顶点 s 和 t 之间的最长路径与图 G'中从 G 得出的最短路径（通过将每个权重更改为负值）相同。 因此，如果可以在 G’中找到最短路径，那么也可以在 G 中找到最长路径。

以下是寻找最长路径的分步过程–

我们将给定图的每条边的权重更改为负值，并将到所有顶点的距离初始化为无穷大，到源的距离初始化为 0，然后找到该图的拓扑排序，该图表示该图的线性排序。 当我们按拓扑顺序考虑顶点 u 时，可以确保我们考虑了它的每个传入边。 也就是说，我们已经找到了到达该顶点的最短路径，并且可以使用该信息来更新其所有相邻顶点的更短路径。 一旦我们有了拓扑顺序，我们就会按照拓扑顺序逐一处理所有顶点。 对于每个要处理的顶点，我们使用当前顶点到源顶点及其边权重的最短距离来更新其相邻顶点的距离。 即

```
for every adjacent vertex v of every vertex u in topological order
    if (dist[v] > dist[u] + weight(u, v))
    dist[v] = dist[u] + weight(u, v)

```

一旦找到了源顶点的所有最短路径，最长路径就是对最短路径的求反。

以下是其 C++实现–

```

// A C++ program to find single source longest distances 
// in a DAG 
#include <bits/stdc++.h> 
using namespace std; 

// Graph is represented using adjacency list. Every node of 
// adjacency list contains vertex number of the vertex to 
// which edge connects. It also contains weight of the edge 
class AdjListNode 
{ 
    int v; 
    int weight; 
public: 
    AdjListNode(int _v, int _w) 
    { 
        v = _v; 
        weight = _w; 
    } 
    int getV() 
    { 
        return v; 
    } 
    int getWeight() 
    { 
        return weight; 
    } 
}; 

// Graph class represents a directed graph using adjacency 
// list representation 
class Graph 
{ 
    int V; // No. of vertices 

    // Pointer to an array containing adjacency lists 
    list<AdjListNode>* adj; 

    // This function uses DFS 
    void longestPathUtil(int, vector<bool> &, stack<int> &); 
public: 
    Graph(int); // Constructor 
    ~Graph();   // Destructor 

    // function to add an edge to graph 
    void addEdge(int, int, int); 

    void longestPath(int); 
}; 

Graph::Graph(int V) // Constructor 
{ 
    this->V = V; 
    adj = new list<AdjListNode>[V]; 
} 

Graph::~Graph() // Destructor 
{ 
    delete[] adj; 
} 

void Graph::addEdge(int u, int v, int weight) 
{ 
    AdjListNode node(v, weight); 
    adj[u].push_back(node); // Add v to u's list 
} 

// A recursive function used by longestPath. See below 
// link for details. 
// https://www.geeksforgeeks.org/topological-sorting/ 
void Graph::longestPathUtil(int v, vector<bool> &visited, 
                            stack<int> &Stack) 
{ 
    // Mark the current node as visited 
    visited[v] = true; 

    // Recur for all the vertices adjacent to this vertex 
    for (AdjListNode node : adj[v]) 
    { 
        if (!visited[node.getV()]) 
            longestPathUtil(node.getV(), visited, Stack); 
    } 

    // Push current vertex to stack which stores topological 
    // sort 
    Stack.push(v); 
} 

// The function do Topological Sort and finds longest 
// distances from given source vertex 
void Graph::longestPath(int s) 
{ 
    // Initialize distances to all vertices as infinite and 
    // distance to source as 0 
    int dist[V]; 
    for (int i = 0; i < V; i++) 
        dist[i] = INT_MAX; 
    dist[s] = 0; 

    stack<int> Stack; 

    // Mark all the vertices as not visited 
    vector<bool> visited(V, false); 

    for (int i = 0; i < V; i++) 
        if (visited[i] == false) 
            longestPathUtil(i, visited, Stack); 

    // Process vertices in topological order 
    while (!Stack.empty()) 
    { 
        // Get the next vertex from topological order 
        int u = Stack.top(); 
        Stack.pop(); 

        if (dist[u] != INT_MAX) 
        { 
            // Update distances of all adjacent vertices 
            // (edge from u -> v exists) 
            for (AdjListNode v : adj[u]) 
            { 
                // consider negative weight of edges and 
                // find shortest path 
                if (dist[v.getV()] > dist[u] + v.getWeight() * -1) 
                    dist[v.getV()] = dist[u] + v.getWeight() * -1; 
            } 
        } 
    } 

    // Print the calculated longest distances 
    for (int i = 0; i < V; i++) 
    { 
        if (dist[i] == INT_MAX) 
            cout << "INT_MIN "; 
        else
            cout << (dist[i] * -1) << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    Graph g(6); 

    g.addEdge(0, 1, 5); 
    g.addEdge(0, 2, 3); 
    g.addEdge(1, 3, 6); 
    g.addEdge(1, 2, 2); 
    g.addEdge(2, 4, 4); 
    g.addEdge(2, 5, 2); 
    g.addEdge(2, 3, 7); 
    g.addEdge(3, 5, 1); 
    g.addEdge(3, 4, -1); 
    g.addEdge(4, 5, -2); 

    int s = 1; 

    cout << "Following are longest distances from "
         << "source vertex " << s << " \n"; 
    g.longestPath(s); 

    return 0; 
} 

```

输出：

```
Following are longest distances from source vertex 1 
INT_MIN 0 2 9 8 10 

```

**时间复杂度**：拓扑排序的时间复杂度为 O（V + E）。 找到拓扑顺序后，该算法将处理所有顶点，并且对于每个顶点，它将为所有相邻顶点运行一个循环。 由于图中的所有相邻顶点均为 O（E），因此内部循环运行 O（V + E）次。 因此，该算法的总时间复杂度为 O（V + E）。

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

