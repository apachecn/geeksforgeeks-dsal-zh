# Kahn 的拓扑排序算法

> 原文： [https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)

对 **D** 相连的**的拓扑排序**循环 **G** raph（DAG）是顶点的线性排序，使得对于每个有向边 uv，顶点 u 都位于 v in 之前 订购。 如果图形不是 DAG，则无法对图形进行拓扑排序。

例如，下图的拓扑排序是“ 5 4 2 3 1 0”。 一个图可以有多个拓扑排序。 例如，下图的另一拓扑排序是“ 4 5 2 0 3 1”。 拓扑排序中的第一个顶点始终是度数为 0 的顶点（没有传入边的顶点）。

[![graph](img/7d0dd3600bc879e60d2864710a2aab68.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/graph.png)

让我们看几个带有适当说明的示例：
**示例：**

> **输入：** ![](img/b40cfedfd46f58209c37921ff7dfd8a5.png)
> **输出：** 5 4 2 3 1 0
> **说明：** DAG 的拓扑排序是按顺序进行的 这样对于每个有向边 uv，在排序中，顶点 u 在 v 之前。 5 没有进入边缘。 4 没有输入边缘，2 和 0 具有 4 和 5 的输入边缘，最后放置 1。
> 
> **输入：** ![](img/d9d816f89505d5e46c2716780ffc6fc6.png)
> **输出：** 0 3 4 1 2
> **说明：** 0 和 3 没有输入边，4 和 1 有输入边 从 0 和 3 进入的边。最后放置 2。

已经讨论了基于 [DFS 的解决方案来查找拓扑类别](https://www.geeksforgeeks.org/topological-sorting/)。

<u>**解决方案**</u> ：在本文中，我们将看到在有向无环图（DAG）中找到顶点的线性顺序的另一种方法。 该方法基于以下事实：

**DAG G 至少具有一个度数为 0 的顶点和一个度数为 0 的顶点**。
**证明：**上述事实有一个简单的证明，即 DAG 不包含循环，这意味着所有路径的长度都是有限的。 现在，使 S 为从 u（源）到 v（目标）的最长路径。 由于 S 是最长的路径，所以不会有到 u 的输入边，也不会有从 v 的输出边，因此，如果发生这种情况，则 S 不会是最长的路径
= > indegree（u）= 0 和 outdegree （v）= 0

**算法：**查找 DAG 拓扑顺序所涉及的步骤：
**步骤-1：**计算存在于每个 DAG 中的每个顶点的度数（进入边的数量） DAG 并将访问的节点数初始化为 0。

**步骤 2：**选取度数为 0 的所有顶点并将其添加到队列中（入队操作）

**步骤 3：**然后从队列中删除一个顶点（出队操作）。

1.  访问的节点数增加 1。
2.  将其所有相邻节点的度数减少 1。
3.  如果将相邻节点的度降低到零，则将其添加到队列中。

**步骤 5：**重复步骤 3，直到队列为空。

**步骤 5：**如果访问的节点数是**，而不是**不等于图中的节点数，则对于给定的图，不可能进行拓扑排序。

**如何找到每个节点的度数？**
有两种计算每个顶点的度数的方法：

1.  Take an in-degree array which will keep track of
    Traverse the array of edges and simply increase the counter of the destination node by 1.

    ```
    for each node in Nodes
        indegree[node] = 0;
    for each edge(src, dest) in Edges
        indegree[dest]++
    ```

    时间复杂度：O（V + E）

2.  Traverse the list for every node and then increment the in-degree of all the nodes connected to it by 1.

    ```
        for each node in Nodes
            If (list[node].size()!=0) then
            for each dest in list
                indegree[dest]++;
    ```

    时间复杂度：外层 for 循环将执行 V 次，内层 for 循环将执行 E 次，因此总时间复杂度为 O（V + E）。

    该算法的总时间复杂度为 O（V + E）

下面是上述算法的 C ++实现。 该实现使用上面讨论的方法 2 查找度数。

## C ++

```

// A C++ program to print topological 
// sorting of a graph using indegrees. 
#include <bits/stdc++.h> 
using namespace std; 

// Class to represent a graph 
class Graph { 
    // No. of vertices' 
    int V; 

    // Pointer to an array containing 
    // adjacency listsList 
    list<int>* adj; 

public: 
    // Constructor 
    Graph(int V); 

    // Function to add an edge to graph 
    void addEdge(int u, int v); 

    // prints a Topological Sort of 
    // the complete graph 
    void topologicalSort(); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int u, int v) 
{ 
    adj[u].push_back(v); 
} 

// The function to do 
// Topological Sort. 
void Graph::topologicalSort() 
{ 
    // Create a vector to store 
    // indegrees of all 
    // vertices. Initialize all 
    // indegrees as 0\. 
    vector<int> in_degree(V, 0); 

    // Traverse adjacency lists 
    // to fill indegrees of 
    // vertices.  This step 
    // takes O(V+E) time 
    for (int u = 0; u < V; u++) { 
        list<int>::iterator itr; 
        for (itr = adj[u].begin(); 
             itr != adj[u].end(); itr++) 
            in_degree[*itr]++; 
    } 

    // Create an queue and enqueue 
    // all vertices with indegree 0 
    queue<int> q; 
    for (int i = 0; i < V; i++) 
        if (in_degree[i] == 0) 
            q.push(i); 

    // Initialize count of visited vertices 
    int cnt = 0; 

    // Create a vector to store 
    // result (A topological 
    // ordering of the vertices) 
    vector<int> top_order; 

    // One by one dequeue vertices 
    // from queue and enqueue 
    // adjacents if indegree of 
    // adjacent becomes 0 
    while (!q.empty()) { 
        // Extract front of queue 
        // (or perform dequeue) 
        // and add it to topological order 
        int u = q.front(); 
        q.pop(); 
        top_order.push_back(u); 

        // Iterate through all its 
        // neighbouring nodes 
        // of dequeued node u and 
        // decrease their in-degree 
        // by 1 
        list<int>::iterator itr; 
        for (itr = adj[u].begin(); 
             itr != adj[u].end(); itr++) 

            // If in-degree becomes zero, 
            // add it to queue 
            if (--in_degree[*itr] == 0) 
                q.push(*itr); 

        cnt++; 
    } 

    // Check if there was a cycle 
    if (cnt != V) { 
        cout << "There exists a cycle in the graph\n"; 
        return; 
    } 

    // Print topological order 
    for (int i = 0; i < top_order.size(); i++) 
        cout << top_order[i] << " "; 
    cout << endl; 
} 

// Driver program to test above functions 
int main() 
{ 
    // Create a graph given in the 
    // above diagram 
    Graph g(6); 
    g.addEdge(5, 2); 
    g.addEdge(5, 0); 
    g.addEdge(4, 0); 
    g.addEdge(4, 1); 
    g.addEdge(2, 3); 
    g.addEdge(3, 1); 

    cout << "Following is a Topological Sort of\n"; 
    g.topologicalSort(); 

    return 0; 
} 

```