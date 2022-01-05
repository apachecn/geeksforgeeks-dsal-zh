# 检查移除给定边是否会断开图形

> 原文:[https://www . geesforgeks . org/check-remove-给定-edge-disconnects-给定-graph/](https://www.geeksforgeeks.org/check-removing-given-edge-disconnects-given-graph/)

给定一个无向图和一条边，任务是找出给定的边是否是图中的[桥](https://www.geeksforgeeks.org/bridge-in-a-graph/)，即移除边会断开图。

以下是一些带有红色突出显示的桥的示例图。

[![Bridge1](img/9b96ad4f3ba84ccea21701a8144a9b7c.png)](https://www.geeksforgeeks.org/wp-content/uploads/Bridge1.png)[![Bridge2](img/e02a14c309771a7d2bfcad3c3cf19370.png)](https://www.geeksforgeeks.org/wp-content/uploads/Bridge2.png)[![Bridge3](img/0e398ed2842367256c38e41388d4cc1e.png)](https://www.geeksforgeeks.org/wp-content/uploads/Bridge3.png)

一种解决方法是[找到给定图](https://www.geeksforgeeks.org/bridge-in-a-graph/)中的所有桥，然后检查给定边是否是桥。

一个更简单的解决方案是移除边，检查移除后图形是否保持连接，最后将边添加回来。通过从任意一个顶点寻找所有可达顶点，我们总能发现一个无向图是否连通。如果可达顶点数等于图中顶点数，则图是连通的，否则不是连通的。我们可以使用 BFS 或 DFS 找到所有可达顶点。以下是完整的步骤。

1)移除给定的边
2)从任意顶点找到所有可到达的顶点。我们在下面的实现中选择了第一个顶点。
3)如果可达节点数为 V，则返回 false[给定不是桥]。否则返回是。

## C++

```
// C++ program to check if removing an
// edge disconnects a graph or not.
#include<bits/stdc++.h>
using namespace std;

// Graph class represents a directed graph
// using adjacency list representation
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;
    void DFS(int v, bool visited[]);
public:
    Graph(int V);   // Constructor

    // function to add an edge to graph
    void addEdge(int v, int w);

    // Returns true if graph is connected
    bool isConnected();

    bool isBridge(int u, int v);
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int u, int v)
{
    adj[u].push_back(v); // Add w to v’s list.
    adj[v].push_back(u); // Add w to v’s list.
}

void Graph::DFS(int v, bool visited[])
{
    // Mark the current node as visited and print it
    visited[v] = true;

    // Recur for all the vertices adjacent to
    // this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFS(*i, visited);
}

// Returns true if given graph is connected, else false
bool Graph::isConnected()
{
    bool visited[V];
    memset(visited, false, sizeof(visited));

    // Find all reachable vertices from first vertex
    DFS(0, visited);

    // If set of reachable vertices includes all,
    // return true.
    for (int i=1; i<V; i++)
       if (visited[i] == false)
           return false;

    return true;
}

// This function assumes that edge (u, v)
// exists in graph or not,
bool Graph::isBridge(int u, int v)
{
    // Remove edge from undirected graph
    adj[u].remove(v);
    adj[v].remove(u);

    bool res = isConnected();

    // Adding the edge back
    addEdge(u, v);

    // Return true if graph becomes disconnected
    // after removing the edge.
    return (res == false);
}

// Driver code
int main()
{
    // Create a graph given in the above diagram
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    g.isBridge(1, 2)? cout << "Yes" : cout << "No";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to check if removing 
# an edge disconnects a graph or not. 

# Graph class represents a directed graph 
# using adjacency list representation 
class Graph:

    def __init__(self, V):
        self.V = V 
        self.adj = [[] for i in range(V)]

    def addEdge(self, u, v):
        self.adj[u].append(v) # Add w to v’s list. 
        self.adj[v].append(u) # Add w to v’s list.

    def DFS(self, v, visited):

        # Mark the current node as 
        # visited and print it 
        visited[v] = True

        # Recur for all the vertices 
        # adjacent to this vertex
        i = 0
        while i != len(self.adj[v]):
            if (not visited[self.adj[v][i]]): 
                self.DFS(self.adj[v][i], visited)
            i += 1

    # Returns true if given graph is 
    # connected, else false 
    def isConnected(self):
        visited = [False] * self.V

        # Find all reachable vertices 
        # from first vertex 
        self.DFS(0, visited) 

        # If set of reachable vertices 
        # includes all, return true.
        for i in range(1, self.V):
            if (visited[i] == False): 
                return False

        return True

    # This function assumes that edge  
    # (u, v) exists in graph or not, 
    def isBridge(self, u, v):

        # Remove edge from undirected graph
        indU = self.adj[v].index(u)
        indV = self.adj[u].index(v)
        del self.adj[u][indV] 
        del self.adj[v][indU] 

        res = self.isConnected() 

        # Adding the edge back 
        self.addEdge(u, v) 

        # Return true if graph becomes 
        # disconnected after removing 
        # the edge. 
        return (res == False)

# Driver code 
if __name__ == '__main__':

    # Create a graph given in the
    # above diagram 
    g = Graph(4)
    g.addEdge(0, 1) 
    g.addEdge(1, 2) 
    g.addEdge(2, 3) 

    if g.isBridge(1, 2):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

**Output :**

```
Yes
```

**时间复杂度:** O(V + E)

本文由 **Pankaj Sharma** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论