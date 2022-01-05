# 利用顶点的离开时间对图进行拓扑排序

> 原文:[https://www . geesforgeks . org/拓扑排序-使用-出发-顶点时间/](https://www.geeksforgeeks.org/topological-sorting-using-departure-time-of-vertex/)

给定一个有向无环图，求该图的拓扑排序。
**有向无环图(DAG)的拓扑排序**是顶点的线性排序，使得对于每个有向边 uv，顶点 u 在排序中位于 v 之前。如果图形不是 DAG，则不可能对图形进行拓扑排序。
例如，下图的拓扑排序为“5 4 2 3 1 0”。一个图可以有多个拓扑排序。例如，下图的另一种拓扑排序是“4 5 2 3 1 0”。

![Topological Sort](img/31b4664cf71d036d9996a080b294e13a.png)

请注意，拓扑排序中的第一个顶点总是一个入度为 0 的顶点(一个没有引入边的顶点)。对于上面的图，顶点 4 和 5 没有引入边。

我们已经讨论了一个基于离散傅立叶变换的算法，使用堆栈和[卡恩算法](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)进行拓扑排序。我们还讨论了如何打印所有拓扑类型的 DAG [在这里](https://www.geeksforgeeks.org/all-topological-sorts-of-a-directed-acyclic-graph/)。本文讨论了另一种基于离散傅立叶变换的方法，通过在离散傅立叶变换中引入顶点到达和离开时间的概念来寻找图的拓扑排序。

**什么是 DFS 中顶点的到达时间&离开时间？**
在 DFS 中，**到达时间**是第一次探索顶点的时间，**出发时间**是我们已经探索了顶点的所有邻居，准备回溯的时间。

**如何利用出发时间求图的拓扑排序？**
为了找到图的拓扑排序，我们从所有未访问的顶点开始一个接一个地运行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。对于任何顶点，在探索它的任何邻居之前，我们记录该顶点的到达时间，在探索该顶点的所有邻居之后，我们记录它的离开时间。请注意，找到图的拓扑排序只需要出发时间，所以我们可以跳过顶点的到达时间。最后，在我们访问了图的所有顶点之后，我们按照顶点离开时间的递减顺序打印这些顶点，这是我们想要的顶点拓扑顺序。
以下是上述思路的 C++实现–

## C++

```
// A C++ program to print topological sorting of a DAG
#include <bits/stdc++.h>
using namespace std;

// Graph class represents a directed graph using adjacency
// list representation
class Graph {
    int V; // No. of vertices
    // Pointer to an array containing adjacency lists
    list<int>* adj;

public:
    Graph(int); // Constructor
    ~Graph(); // Destructor

    // function to add an edge to graph
    void addEdge(int, int);

    // The function to do DFS traversal
    void DFS(int, vector<bool>&, vector<int>&, int&);

    // The function to do Topological Sort.
    void topologicalSort();
};

Graph::Graph(int V)
{
    this->V = V;
    this->adj = new list<int>[V];
}

Graph::~Graph() { delete[] this->adj; }

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w); // Add w to v's list.
}

// The function to do DFS() and stores departure time
// of all vertex
void Graph::DFS(int v, vector<bool>& visited,
                vector<int>& departure, int& time)
{
    visited[v] = true;
    // time++;    // arrival time of vertex v

    for (int i : adj[v])
        if (!visited[i])
            DFS(i, visited, departure, time);

    // set departure time of vertex v
    departure[time++] = v;
}

// The function to do Topological Sort. It uses DFS().
void Graph::topologicalSort()
{
    // vector to store departure time of vertex.
    vector<int> departure(V, -1);

    // Mark all the vertices as not visited
    vector<bool> visited(V, false);
    int time = 0;

    // perform DFS on all unvisited vertices
    for (int i = 0; i < V; i++) {
        if (visited[i] == 0) {
            DFS(i, visited, departure, time);
        }
    }
    // print the topological sort
    for (int i = V - 1; i >= 0; i--)
        cout << departure[i] << " ";
}

// Driver program to test above functions
int main()
{
    // Create a graph given in the above diagram
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    cout << "Topological Sort of the given graph is \n";
    g.topologicalSort();

    return 0;
}
```

## 蟒蛇 3

```
# A Python3 program to print topological sorting of a DAG
def addEdge(u, v):
    global adj
    adj[u].append(v)

# The function to do DFS() and stores departure time
# of all vertex
def DFS(v):
    global visited, departure, time
    visited[v] = 1
    for i in adj[v]:
        if visited[i] == 0:
            DFS(i)
    departure[time] = v
    time += 1

# The function to do Topological Sort. It uses DFS().
def topologicalSort():

    # perform DFS on all unvisited vertices
    for i in range(V):
        if(visited[i] == 0):
            DFS(i)

    # Print vertices in topological order
    for i in range(V - 1, -1, -1):
        print(departure[i], end = " ")

# Driver code
if __name__ == '__main__':

    # Create a graph given in the above diagram
    V,time, adj, visited, departure = 6, 0, [[] for i in range(7)], [0 for i in range(7)],[-1 for i in range(7)]
    addEdge(5, 2)
    addEdge(5, 0)
    addEdge(4, 0)
    addEdge(4, 1)
    addEdge(2, 3)
    addEdge(3, 1)

    print("Topological Sort of the given graph is")
    topologicalSort()

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// A JavaScript program to print topological
// sorting of a DAG

    let adj=new Array(7);
    for(let i=0;i<adj.length;i++)
    {
        adj[i]=[];
    }
    let V=6;
    let time=0;
    let visited=new Array(7);
    let departure =new Array(7);
    for(let i=0;i<7;i++)
    {
        visited[i]=0;
        departure[i]=-1;
    }
    function addEdge(u, v)
    {
        adj[u].push(v)
    }

    // The function to do DFS() and
    // stores departure time
    // of all vertex
    function DFS(v)
    {
        visited[v] = 1;
        for(let i=0;i<adj[v].length;i++)
        {
            if(visited[adj[v][i]]==0)
                DFS(adj[v][i]);
        }
        departure[time] = v
        time += 1
    }
    // The function to do Topological
    // Sort. It uses DFS().
    function topologicalSort()
    {
    //perform DFS on all unvisited vertices
        for(let i=0;i<V;i++)
        {
            if(visited[i] == 0)
                DFS(i)
        }
        //perform DFS on all unvisited vertices
        for(let i=V-1;i>=0;i--)
        {           
            document.write(departure[i]+" ");
        }
    }

    // Create a graph given in the above diagram

    addEdge(5, 2);
    addEdge(5, 0);
    addEdge(4, 0);
    addEdge(4, 1);
    addEdge(2, 3);
    addEdge(3, 1);
    document.write(
    "Topological Sort of the given graph is<br>"
    );
    topologicalSort()

    // This code is contributed by unknown2108

</script>
```

**Output**

```
Topological Sort of the given graph is 
5 4 2 3 1 0 
```

**上述解的时间复杂度**为 O(V + E)。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。