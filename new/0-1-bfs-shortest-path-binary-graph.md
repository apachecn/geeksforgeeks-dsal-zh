# 0-1 BFS（二进制权重图中的最短路径）

> 原文： [https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/)

给定一个图，其中每个边的权重为 0 或 1。在图中还给出了源顶点。 查找从源顶点到其他每个顶点的最短路径。
**例如**：

```
Input : Source Vertex = 0 and below graph 
![0-1-bfs](img/771ea439d119b7f44e08642018f21a8d.png)

Output : Shortest distances from given source
         0 0 1 1 2 1 2 1 2

Explanation : 
Shortest distance from 0 to 0 is 0
Shortest distance from 0 to 1 is 0
Shortest distance from 0 to 2 is 1
..................

```

在图形的正常 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 中，所有边缘的权重均等，但在 0-1 BFS 中，某些边缘的权重为 0，而某些边缘的权重为 1。 在这种情况下，我们将不使用布尔数组来标记访问的节点，但是在每一步中，我们都会检查最佳距离条件。 我们使用[双端队列](http://quiz.geeksforgeeks.org/deque-set-1-introduction-applications/)存储该节点。 在执行 BFS 时，如果找到权重= 0 的边，则将节点推入双头队列的前面，如果找到权重= 1 的边，则将其推入双头队列的后面。

该方法类似于 [Dijkstra](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/) ，如果到节点的最短距离被前一个节点放宽，则仅将其推入队列。

上面的想法在所有情况下都有效，当弹出一个顶点（如 Dijkstra）时，它是剩余顶点中最小的权重顶点。 如果相邻的权重顶点为 0，则该相邻顶点的距离相同。 如果相邻的权重为 1，则该相邻的对象在出队的所有顶点之间具有最大距离（因为所有其他顶点都与当前弹出的顶点相邻或与先前弹出的顶点相邻）。

以下是上述想法的实现。

## C++

```cpp

// C++ program to implement single source 
// shortest path for a Binary Graph 
#include<bits/stdc++.h> 
using namespace std; 

/* no.of vertices */
#define V 9 

// a structure to represent edges 
struct node 
{ 
    // two variable one denote the node 
    // and other the weight 
    int to, weight; 
}; 

// vector to store edges 
vector <node> edges[V]; 

// Prints shortest distance from given source to 
// every other vertex 
void zeroOneBFS(int src) 
{ 
    // Initialize distances from given source 
    int dist[V]; 
    for (int i=0; i<V; i++) 
        dist[i] = INT_MAX; 

    // double ende queue to do BFS. 
    deque <int> Q; 
    dist[src] = 0; 
    Q.push_back(src); 

    while (!Q.empty()) 
    { 
        int v = Q.front(); 
        Q.pop_front(); 

        for (int i=0; i<edges[v].size(); i++) 
        { 
            // checking for the optimal distance 
            if (dist[edges[v][i].to] > dist[v] + edges[v][i].weight) 
            { 
                dist[edges[v][i].to] = dist[v] + edges[v][i].weight; 

                // Put 0 weight edges to front and 1 weight 
                // edges to back so that vertices are processed 
                // in increasing order of weights. 
                if (edges[v][i].weight == 0) 
                    Q.push_front(edges[v][i].to); 
                else
                    Q.push_back(edges[v][i].to); 
            } 
        } 
    } 

    // printing the shortest distances 
    for (int i=0; i<V; i++) 
        cout << dist[i] << " "; 
} 

void addEdge(int u, int v, int wt) 
{ 
   edges[u].push_back({v, wt}); 
   edges[v].push_back({u, wt}); 
} 

// Driver function 
int main() 
{ 
    addEdge(0, 1, 0); 
    addEdge(0, 7, 1); 
    addEdge(1, 7, 1); 
    addEdge(1, 2, 1); 
    addEdge(2, 3, 0); 
    addEdge(2, 5, 0); 
    addEdge(2, 8, 1); 
    addEdge(3, 4, 1); 
    addEdge(3, 5, 1); 
    addEdge(4, 5, 1); 
    addEdge(5, 6, 1); 
    addEdge(6, 7, 1); 
    addEdge(7, 8, 1); 
    int src = 0;//source node 
    zeroOneBFS(src); 
    return 0; 
} 

```