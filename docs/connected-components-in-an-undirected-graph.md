# 无向图中的连通分量

> 原文:[https://www . geeksforgeeks . org/连接组件无向图/](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

给定一个无向图，逐行打印所有连接的组件。例如，考虑下面的图表。

![SCCUndirected](img/a79d2e5fa34c51c9a36a83b4578d9478.png)

**强烈建议尽量减少浏览器，先自己试试这个。**
我们在下面的文章中讨论了在有向图中寻找强连通分支的算法。
[小泽一郎的强连通分量算法](https://www.geeksforgeeks.org/strongly-connected-components/)。
[塔尔扬寻找强连通分支的算法](https://www.geeksforgeeks.org/tarjan-algorithm-find-strongly-connected-components/)
寻找无向图的连通分支是一个更容易的任务。我们只需要从每个未访问的顶点开始进行 BFS 或离散傅立叶变换，就可以得到所有强连通的分量。以下是基于 DFS 的步骤。

```
1) Initialize all vertices as not visited.
2) Do following for every vertex 'v'.
       (a) If 'v' is not visited before, call DFSUtil(v)
       (b) Print new line character

DFSUtil(v)
1) Mark 'v' as visited.
2) Print 'v'
3) Do following for every adjacent 'u' of 'v'.
     If 'u' is not visited, then recursively call DFSUtil(u)
```

下面是上述算法的实现。

## C++

```
// C++ program to print connected components in
// an undirected graph
#include <iostream>
#include <list>
using namespace std;

// Graph class represents a undirected graph
// using adjacency list representation
class Graph {
    int V; // No. of vertices

    // Pointer to an array containing adjacency lists
    list<int>* adj;

    // A function used by DFS
    void DFSUtil(int v, bool visited[]);

public:
    Graph(int V); // Constructor
    ~Graph();
    void addEdge(int v, int w);
    void connectedComponents();
};

// Method to print connected components in an
// undirected graph
void Graph::connectedComponents()
{
    // Mark all the vertices as not visited
    bool* visited = new bool[V];
    for (int v = 0; v < V; v++)
        visited[v] = false;

    for (int v = 0; v < V; v++) {
        if (visited[v] == false) {
            // print all reachable vertices
            // from v
            DFSUtil(v, visited);

            cout << "\n";
        }
    }
    delete[] visited;
}

void Graph::DFSUtil(int v, bool visited[])
{
    // Mark the current node as visited and print it
    visited[v] = true;
    cout << v << " ";

    // Recur for all the vertices
    // adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFSUtil(*i, visited);
}

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

Graph::~Graph() { delete[] adj; }

// method to add an undirected edge
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
    adj[w].push_back(v);
}

// Driver code
int main()
{
    // Create a graph given in the above diagram
    Graph g(5); // 5 vertices numbered from 0 to 4
    g.addEdge(1, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    cout << "Following are connected components \n";
    g.connectedComponents();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print connected components in
// an undirected graph
import java.util.ArrayList;
class Graph
{
    // A user define class to represent a graph.
    // A graph is an array of adjacency lists.
    // Size of array will be V (number of vertices
    // in graph)
    int V;
    ArrayList<ArrayList<Integer> > adjListArray;

    // constructor
    Graph(int V)
    {
        this.V = V;
        // define the size of array as
        // number of vertices
        adjListArray = new ArrayList<>();

        // Create a new list for each vertex
        // such that adjacent nodes can be stored

        for (int i = 0; i < V; i++) {
            adjListArray.add(i, new ArrayList<>());
        }
    }

    // Adds an edge to an undirected graph
    void addEdge(int src, int dest)
    {
        // Add an edge from src to dest.
        adjListArray.get(src).add(dest);

        // Since graph is undirected, add an edge from dest
        // to src also
        adjListArray.get(dest).add(src);
    }

    void DFSUtil(int v, boolean[] visited)
    {
        // Mark the current node as visited and print it
        visited[v] = true;
        System.out.print(v + " ");
        // Recur for all the vertices
        // adjacent to this vertex
        for (int x : adjListArray.get(v)) {
            if (!visited[x])
                DFSUtil(x, visited);
        }
    }
    void connectedComponents()
    {
        // Mark all the vertices as not visited
        boolean[] visited = new boolean[V];
        for (int v = 0; v < V; ++v) {
            if (!visited[v]) {
                // print all reachable vertices
                // from v
                DFSUtil(v, visited);
                System.out.println();
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Create a graph given in the above diagram
        Graph g = new Graph(
            5); // 5 vertices numbered from 0 to 4

        g.addEdge(1, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 4);
        System.out.println(
            "Following are connected components");
        g.connectedComponents();
    }
}
```

## 计算机编程语言

```
# Python program to print connected
# components in an undirected graph

class Graph:

    # init function to declare class variables
    def __init__(self, V):
        self.V = V
        self.adj = [[] for i in range(V)]

    def DFSUtil(self, temp, v, visited):

        # Mark the current vertex as visited
        visited[v] = True

        # Store the vertex to list
        temp.append(v)

        # Repeat for all vertices adjacent
        # to this vertex v
        for i in self.adj[v]:
            if visited[i] == False:

                # Update the list
                temp = self.DFSUtil(temp, i, visited)
        return temp

    # method to add an undirected edge
    def addEdge(self, v, w):
        self.adj[v].append(w)
        self.adj[w].append(v)

    # Method to retrieve connected components
    # in an undirected graph
    def connectedComponents(self):
        visited = []
        cc = []
        for i in range(self.V):
            visited.append(False)
        for v in range(self.V):
            if visited[v] == False:
                temp = []
                cc.append(self.DFSUtil(temp, v, visited))
        return cc

# Driver Code
if __name__ == "__main__":

    # Create a graph given in the above diagram
    # 5 vertices numbered from 0 to 4
    g = Graph(5)
    g.addEdge(1, 0)
    g.addEdge(2, 3)
    g.addEdge(3, 4)
    cc = g.connectedComponents()
    print("Following are connected components")
    print(cc)

# This code is contributed by Abhishek Valsan
```

## C#

```
// C++ program to print connected components in
// an undirected graph
#include <iostream>
#include <list>
using namespace std;

// Graph class represents a undirected graph
// using adjacency list representation
class Graph
{
    int V; // No. of vertices

    // Pointer to an array containing adjacency lists
    list<int>* adj;

    // A function used by DFS
    void DFSUtil(int v, bool visited[]);

    public : Graph(int V); // Constructor
    ~Graph();
    void addEdge(int v, int w);
    void connectedComponents();
};

// Method to print connected components in an
// undirected graph
void Graph::connectedComponents()
{
    // Mark all the vertices as not visited
    bool* visited = new bool[V];
    for (int v = 0; v < V; v++)
        visited[v] = false;

    for (int v = 0; v < V; v++) {
        if (visited[v] == false) {
            // print all reachable vertices
            // from v
            DFSUtil(v, visited);

            cout << "\n";
        }
    }
    delete[] visited;
}

void Graph::DFSUtil(int v, bool visited[])
{
    // Mark the current node as visited and print it
    visited[v] = true;
    cout << v << " ";

    // Recur for all the vertices
    // adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFSUtil(*i, visited);
}

Graph::Graph(int V)
{
    this -> V = V;
    adj = new list<int>[ V ];
}

Graph::~Graph() { delete[] adj; }

// method to add an undirected edge
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
    adj[w].push_back(v);
}

// Driver code
int main()
{
    // Create a graph given in the above diagram
    Graph g(5); // 5 vertices numbered from 0 to 4
    g.addEdge(1, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    cout << "Following are connected components \n";
    g.connectedComponents();

    return 0;
}
```

## java 描述语言

```
<script>
// Javascript program to print connected components in
// an undirected graph

// A user define class to represent a graph.
    // A graph is an array of adjacency lists.
    // Size of array will be V (number of vertices
    // in graph)
let V;
let adjListArray=[];

// constructor
function Graph(v)
{   
    V = v

        // define the size of array as
        // number of vertices

        // Create a new list for each vertex
        // such that adjacent nodes can be stored

        for (let i = 0; i < V; i++) {
            adjListArray.push([]);
        }
}

// Adds an edge to an undirected graph
function addEdge(src,dest)
{
    // Add an edge from src to dest.
        adjListArray[src].push(dest);

        // Since graph is undirected, add an edge from dest
        // to src also
        adjListArray[dest].push(src);
}

function DFSUtil(v,visited)
{
    // Mark the current node as visited and print it
        visited[v] = true;
        document.write(v + " ");

        // Recur for all the vertices
        // adjacent to this vertex
        for (let x = 0; x < adjListArray[v].length; x++)
        {
            if (!visited[adjListArray[v][x]])
                DFSUtil(adjListArray[v][x], visited);
        }
}

function connectedComponents()
{
    // Mark all the vertices as not visited
        let visited = new Array(V);
        for(let i = 0; i < V; i++)
        {
            visited[i] = false;
        }
        for (let v = 0; v < V; ++v)
        {
            if (!visited[v])
            {
                // print all reachable vertices
                // from v
                DFSUtil(v, visited);
                document.write("<br>");
            }
        }
}

// Driver code
Graph(5);

addEdge(1, 0);
addEdge(2, 3);
addEdge(3, 4);
document.write(
"Following are connected components<br>");
connectedComponents();

// This code is contributed by rag2127
</script>
```

**输出:**

```
0 1
2 3 4
```

上述解的时间复杂度为 O(V + E)，因为它对给定的图进行简单的离散傅立叶变换。

这可以使用时间复杂度为 O(N)的[不相交集并](https://www.geeksforgeeks.org/union-find/)来解决。DSU 解决方案更容易理解一个工具。

算法:

！。声明一个大小为 n 的数组 arr，其中 n 是节点总数。

2.对于数组 arr 的每个索引 I，该值表示第 I 个顶点的父节点是谁。例如 arr[0]=3，那么我们可以说顶点 0 的父顶点是 3。

3.将每个节点初始化为其父节点，然后在将它们添加到一起时，相应地更改它们的父节点。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int merge(int* parent, int x)
{
    if (parent[x] == x)
        return x;
    return merge(parent, parent[x]);
}
int connectedcomponents(int n, vector<vector<int> >& edges)
{
    int parent[n];
    for (int i = 0; i < n; i++) {
        parent[i] = i;
    }
    for (auto x : edges) {
        parent[merge(parent, x[0])] = merge(parent, x[1]);
    }
    int ans = 0;
    for (int i = 0; i < n; i++) {
        ans += (parent[i] == i);
    }
    for (int i = 0; i < n; i++) {
        parent[i] = merge(parent, parent[i]);
    }
    map<int, list<int> > m;
    for (int i = 0; i < n; i++) {
        m[parent[i]].push_back(i);
    }
    for (auto it = m.begin(); it != m.end(); it++) {
        list<int> l = it->second;
        for (auto x : l) {
            cout << x << " ";
        }
        cout << endl;
    }
    return ans;
}
int main()
{
    int n = 5;
    vector<int> e1 = { 0, 1 };
    vector<int> e2 = { 2, 3 };
    vector<int> e3 = { 3, 4 };
    vector<vector<int> > e;
    e.push_back(e1);
    e.push_back(e2);
    e.push_back(e3);
    int a = connectedcomponents(n, e);
    cout << "total no. of connected components are: " << a
         << endl;
    return 0;
}
```

**Output**

```
0 1 
2 3 4 
total no. of connected components are: 2
```

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论