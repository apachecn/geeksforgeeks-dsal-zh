# 计算不可访问的节点数

> 原文： [https://www.geeksforgeeks.org/count-number-non-reachable-nodes/](https://www.geeksforgeeks.org/count-number-non-reachable-nodes/)

给定一个无向图和一组顶点，我们必须使用深度优先搜索来计算给定头节点中不可访问节点的数量。

考虑以下具有两个断开连接的组件的无向图：

![not-reachable](img/8a3668ad4c4e9b59ac1f2a405507159d.png)

在此图中，如果我们将 0 视为头节点，则节点 0、1 和 2 是可到达的。 我们将所有可达节点标记为已访问。 所有未标记为已访问的节点，即节点 3 和 4 都是不可访问的节点。 因此，它们的数量为 2。

**示例**：

```
Input :   5
          0 1
          0 2
          1 2
          3 4
Output : 2

```

为此，我们可以使用 BFS 或 DFS。 在以下实现中，使用 DFS。 我们从给定的来源进行 DFS。 由于给定的图是无向的，所以属于断开连接的组件的所有顶点都是不可访问的节点。 为此，我们使用访问数组，该数组用于跟踪 DFS 中未访问的顶点。 在 DFS 中，如果我们从头节点开始，它将把连接到头节点的所有节点标记为已访问。 然后，遍历该图之后，我们计算未标记为从头节点访问的节点数。

## C++

```cpp

// C++ program to count non-reachable nodes 
// from a given source using DFS. 
#include <iostream> 
#include <list> 
using namespace std; 

// Graph class represents a directed graph 
// using adjacency list representation 
class Graph { 
    int V; // No. of vertices 

    // Pointer to an array containing 
    // adjacency lists 
    list<int>* adj; 

    // A recursive function used by DFS 
    void DFSUtil(int v, bool visited[]); 

public: 
    Graph(int V); // Constructor 

    // function to add an edge to graph 
    void addEdge(int v, int w); 

    // DFS traversal of the vertices 
    // reachable from v 
    int countNotReach(int v); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
    adj[w].push_back(v); // Add v to w's list. 
} 

void Graph::DFSUtil(int v, bool visited[]) 
{ 
    // Mark the current node as visited and 
    // print it 
    visited[v] = true; 

    // Recur for all the vertices adjacent 
    // to this vertex 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
        if (!visited[*i]) 
            DFSUtil(*i, visited); 
} 

// Returns count of not reachable nodes from 
// vertex v. 
// It uses recursive DFSUtil() 
int Graph::countNotReach(int v) 
{ 
    // Mark all the vertices as not visited 
    bool* visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    // Call the recursive helper function 
    // to print DFS traversal 
    DFSUtil(v, visited); 

    // Return count of not visited nodes 
    int count = 0; 
    for (int i = 0; i < V; i++) { 
        if (visited[i] == false) 
            count++; 
    } 
    return count; 
} 

int main() 
{ 
    // Create a graph given in the above diagram 
    Graph g(8); 
    g.addEdge(0, 1); 
    g.addEdge(0, 2); 
    g.addEdge(1, 2); 
    g.addEdge(3, 4); 
    g.addEdge(4, 5); 
    g.addEdge(6, 7); 

    cout << g.countNotReach(2); 

    return 0; 
} 

```

## Python

```py

# Python3 program to count non-reachable  
# nodes from a given source using DFS.  

# Graph class represents a directed graph  
# using adjacency list representation  
class Graph: 
    def __init__(self, V): 
        self.V = V 
        self.adj = [[] for i in range(V)] 

    def addEdge(self, v, w): 
        self.adj[v].append(w) # Add w to v’s list.  
        self.adj[w].append(v) # Add v to w's list. 

    def DFSUtil(self, v, visited): 

        # Mark the current node as  
        # visited and print it  
        visited[v] = True

        # Recur for all the vertices  
        # adjacent to this vertex 
        i = self.adj[v][0] 
        for i in self.adj[v]: 
            if (not visited[i]):  
                self.DFSUtil(i, visited)  

    # Returns count of not reachable  
    # nodes from vertex v.  
    # It uses recursive DFSUtil()  
    def countNotReach(self, v): 

        # Mark all the vertices as not visited  
        visited = [False] * self.V 

        # Call the recursive helper  
        # function to prDFS traversal  
        self.DFSUtil(v, visited)  

        # Return count of not visited nodes  
        count = 0
        for i in range(self.V): 
            if (visited[i] == False):  
                count += 1
        return count 

# Driver Code 
if __name__ == '__main__': 

    # Create a graph given in the 
    # above diagram  
    g = Graph(8)  
    g.addEdge(0, 1)  
    g.addEdge(0, 2)  
    g.addEdge(1, 2)  
    g.addEdge(3, 4)  
    g.addEdge(4, 5)  
    g.addEdge(6, 7)  

    print(g.countNotReach(2)) 

# This code is contributed by PranchalK 

```

**Output:**

```
 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。