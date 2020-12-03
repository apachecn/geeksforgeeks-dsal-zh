# 查找有向图

中两个顶点之间是否存在路径

> 原文： [https://www.geeksforgeeks.org/find-if-there-is-a-path-between-two-vertices-in-a-given-graph/](https://www.geeksforgeeks.org/find-if-there-is-a-path-between-two-vertices-in-a-given-graph/)

给定一个有向图和其中两个顶点，请检查是否存在从第一个给定顶点到第二个顶点的路径。

**示例**：

```
Consider the following Graph:
![](img/40ca76ea468053c881ac72e49e82f1e2.png "BFS")

Input : (u, v) = (1, 3)
Output: Yes
Explanation: There is a path from 1 to 3, 1 -> 2 -> 3

Input : (u, v) = (3, 6)
Output: No
Explanation: There is no path from 3 to 6

```

**方法**：[广度优先搜索（BFS）](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)或[深度优先搜索（DFS）](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)均可用于查找两个顶点之间的路径。 将第一个顶点作为 BFS（或 DFS）中的源，遵循标准 BFS（或 DFS）。 如果在我们的遍历中找到第二个顶点，则返回 true，否则返回 false。

**算法**：

1.  下面的实现使用 BFS。

2.  创建一个队列和一个初始填充为 0 的访问数组，大小为 V，其中 V 是顶点数。

3.  将起始节点插入队列中，即将 u 推入队列并将 u 标记为已访问。

4.  运行循环，直到队列不为空。

5.  使队列的前部元素出队。 迭代其所有相邻元素。 如果任何相邻元素是目标，则返回 true。 将队列中所有相邻的顶点和非可见顶点推入并标记为已访问。

6.  由于在 BFS 中未到达目标，因此返回 false。

**实现**：使用 BFS 从第一顶点查找第二顶点的可达性的 C ++，Java 和 Python 代码。

## C++

```cpp

// C++ program to check if there is exist a path between two vertices 
// of a graph. 
#include<iostream> 
#include <list> 
using namespace std; 

// This class represents a directed graph using adjacency list  
// representation 
class Graph 
{ 
    int V;    // No. of vertices 
    list<int> *adj;    // Pointer to an array containing adjacency lists 
public: 
    Graph(int V);  // Constructor 
    void addEdge(int v, int w); // function to add an edge to graph 
    bool isReachable(int s, int d);   
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 

// A BFS based function to check whether d is reachable from s. 
bool Graph::isReachable(int s, int d) 
{ 
    // Base case 
    if (s == d) 
      return true; 

    // Mark all the vertices as not visited 
    bool *visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    // Create a queue for BFS 
    list<int> queue; 

    // Mark the current node as visited and enqueue it 
    visited[s] = true; 
    queue.push_back(s); 

    // it will be used to get all adjacent vertices of a vertex 
    list<int>::iterator i; 

    while (!queue.empty()) 
    { 
        // Dequeue a vertex from queue and print it 
        s = queue.front(); 
        queue.pop_front(); 

        // Get all adjacent vertices of the dequeued vertex s 
        // If a adjacent has not been visited, then mark it visited 
        // and enqueue it 
        for (i = adj[s].begin(); i != adj[s].end(); ++i) 
        { 
            // If this adjacent node is the destination node, then  
            // return true 
            if (*i == d) 
                return true; 

            // Else, continue to do BFS 
            if (!visited[*i]) 
            { 
                visited[*i] = true; 
                queue.push_back(*i); 
            } 
        } 
    } 

    // If BFS is complete without visiting d 
    return false; 
} 

// Driver program to test methods of graph class 
int main() 
{ 
    // Create a graph given in the above diagram 
    Graph g(4); 
    g.addEdge(0, 1); 
    g.addEdge(0, 2); 
    g.addEdge(1, 2); 
    g.addEdge(2, 0); 
    g.addEdge(2, 3); 
    g.addEdge(3, 3); 

    int u = 1, v = 3; 
    if(g.isReachable(u, v)) 
        cout<< "\n There is a path from " << u << " to " << v; 
    else
        cout<< "\n There is no path from " << u << " to " << v; 

    u = 3, v = 1; 
    if(g.isReachable(u, v)) 
        cout<< "\n There is a path from " << u << " to " << v; 
    else
        cout<< "\n There is no path from " << u << " to " << v; 

    return 0; 
} 

```