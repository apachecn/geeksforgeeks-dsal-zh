# 图形中的关节点(或切割顶点)

> 原文:[https://www . geesforgeks . org/articulation-points-or-cut-折点在图中/](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/)

无向连通图中的顶点是一个连接点(或割顶点)，如果移除它(和通过它的边)会断开该图。连接点代表连接网络中的漏洞——单点故障会将网络分成两个或更多组件。它们对于设计可靠的网络很有用。

对于一个断开的无向图，连接点是一个顶点删除，这增加了连接组件的数量。

下面是一些用红色圈起来的连接点的示例图。

![Articulation Points or Cut Vertices in a Graph](img/f1b197bb8b5729c62f4c541d89e6709f.png) ![Articulation Points or Cut Vertices in a Graph](img/7c944d4d5150205a8bc4d6aca844bacc.png)

![Articulation Points or Cut Vertices in a Graph](img/89ed6835ec967248fb20636c277f3cdb.png)

**如何找到给定图形中的所有关节点？**
一个简单的方法是逐个移除所有顶点，看看移除一个顶点是否会导致图断开。以下是连通图的简单方法步骤。
1)对于每个顶点 v，执行以下操作
…..a)从图表中删除 v
..…b)查看图形是否保持连接(我们可以使用 BFS 或 DFS)
…..c)将 V 加回图中
对于使用邻接表表示的图，上述方法的时间复杂度为 O(V*(V+E))。我们能做得更好吗？

**一种 O(V+E)算法来寻找所有的关节点(APs)**
其思想是使用 DFS(深度优先搜索)。在 DFS 中，我们以树的形式跟随顶点，称为 DFS 树。在 DFS 树中，一个顶点 u 是另一个顶点 v 的父，如果 v 被 u 发现(显然 v 是图中 u 的一个邻)。在 DFS 树中，如果以下两个条件之一成立，则顶点 u 是铰接点。
**1)** u 是 DFS 树的根，它至少有两个孩子。
**2)** u 不是 DFS 树的根，并且它有一个子 v，使得以 v 为根的子树中没有顶点具有到 u 的祖先之一(在 DFS 树中)的后边缘。

下图显示了与上面相同的点，还有一点，即 DFS 树中的一片叶子永远不能成为铰接点。

![leaf in DFS Tree can never be an articulation point](img/c96e154952f2b49adf69a5d2590ea4bb.png)

我们用额外的代码对给定的图进行 DFS 遍历，找出连接点。在 DFS 遍历中，我们维护一个 parent[]数组，其中 parent[u]存储顶点 u 的 parent，在上面提到的两种情况中，第一种情况检测起来很简单。对于每个顶点，计算子顶点。如果当前访问的顶点 u 是根(父[u]是 NIL)并且有两个以上的子顶点，打印它。

第二种情况怎么处理？第二种情况更棘手。我们维护一个数组磁盘[]来存储顶点的发现时间。对于每个节点 u，我们需要找出从以 u 为根的子树可以到达的最早访问的顶点(发现时间最短的顶点)，因此我们维护一个额外的数组 low[]，定义如下。

```
low[u] = min(disc[u], disc[w]) 
where w is an ancestor of u and there is a back edge from 
some descendant of u to w.
```

以下是塔尔扬算法的实现，用于寻找关节点。

## C++

```
// C++ program to find articulation points in an undirected graph
#include <bits/stdc++.h>
using namespace std;

// A recursive function that find articulation 
// points using DFS traversal
// adj[] --> Adjacency List representation of the graph
// u --> The vertex to be visited next
// visited[] --> keeps track of visited vertices
// disc[] --> Stores discovery times of visited vertices
// low[] -- >> earliest visited vertex (the vertex with minimum
// discovery time) that can be reached from subtree
// rooted with current vertex
// parent --> Stores the parent vertex in DFS tree
// isAP[] --> Stores articulation points
void APUtil(vector<int> adj[], int u, bool visited[],
            int disc[], int low[], int& time, int parent,
            bool isAP[])
{
    // Count of children in DFS Tree
    int children = 0;

    // Mark the current node as visited
    visited[u] = true;

    // Initialize discovery time and low value
    disc[u] = low[u] = ++time;

    // Go through all vertices adjacent to this
    for (auto v : adj[u]) {
        // If v is not visited yet, then make it a child of u
        // in DFS tree and recur for it
        if (!visited[v]) {
            children++;
            APUtil(adj, v, visited, disc, low, time, u, isAP);

            // Check if the subtree rooted with v has
            // a connection to one of the ancestors of u
            low[u] = min(low[u], low[v]);

            // If u is not root and low value of one of
            // its child is more than discovery value of u.
            if (parent != -1 && low[v] >= disc[u])
                isAP[u] = true;
        }

        // Update low value of u for parent function calls.
        else if (v != parent)
            low[u] = min(low[u], disc[v]);
    }

    // If u is root of DFS tree and has two or more children.
    if (parent == -1 && children > 1)
        isAP[u] = true;
}

void AP(vector<int> adj[], int V)
{
    int disc[V] = { 0 };
    int low[V];
    bool visited[V] = { false };
    bool isAP[V] = { false };
    int time = 0, par = -1;

    // Adding this loop so that the
    // code works even if we are given
    // disconnected graph
    for (int u = 0; u < V; u++)
        if (!visited[u])
            APUtil(adj, u, visited, disc, low,
                   time, par, isAP);

    // Printing the APs
    for (int u = 0; u < V; u++)
        if (isAP[u] == true)
            cout << u << " ";
}

// Utility function to add an edge
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

int main()
{
    // Create graphs given in above diagrams
    cout << "Articulation points in first graph \n";
    int V = 5;
    vector<int> adj1[V];
    addEdge(adj1, 1, 0);
    addEdge(adj1, 0, 2);
    addEdge(adj1, 2, 1);
    addEdge(adj1, 0, 3);
    addEdge(adj1, 3, 4);
    AP(adj1, V);

    cout << "\nArticulation points in second graph \n";
    V = 4;
    vector<int> adj2[V];
    addEdge(adj2, 0, 1);
    addEdge(adj2, 1, 2);
    addEdge(adj2, 2, 3);
    AP(adj2, V);

    cout << "\nArticulation points in third graph \n";
    V = 7;
    vector<int> adj3[V];
    addEdge(adj3, 0, 1);
    addEdge(adj3, 1, 2);
    addEdge(adj3, 2, 0);
    addEdge(adj3, 1, 3);
    addEdge(adj3, 1, 4);
    addEdge(adj3, 1, 6);
    addEdge(adj3, 3, 5);
    addEdge(adj3, 4, 5);
    AP(adj3, V);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find articulation 
// points in an undirected graph
import java.util.*;

class Graph {

    static int time;

    static void addEdge(ArrayList<ArrayList<Integer> > adj, int u, int v)
    {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static void APUtil(ArrayList<ArrayList<Integer> > adj, int u,
                       boolean visited[], int disc[], int low[],
                       int parent, boolean isAP[])
    {
        // Count of children in DFS Tree
        int children = 0;

        // Mark the current node as visited
        visited[u] = true;

        // Initialize discovery time and low value
        disc[u] = low[u] = ++time;

        // Go through all vertices aadjacent to this
        for (Integer v : adj.get(u)) {
            // If v is not visited yet, then make it a child of u
            // in DFS tree and recur for it
            if (!visited[v]) {
                children++;
                APUtil(adj, v, visited, disc, low, u, isAP);

                // Check if the subtree rooted with v has
                // a connection to one of the ancestors of u
                low[u] = Math.min(low[u], low[v]);

                // If u is not root and low value of one of
                // its child is more than discovery value of u.
                if (parent != -1 && low[v] >= disc[u])
                    isAP[u] = true;
            }

            // Update low value of u for parent function calls.
            else if (v != parent)
                low[u] = Math.min(low[u], disc[v]);
        }

        // If u is root of DFS tree and has two or more children.
        if (parent == -1 && children > 1)
            isAP[u] = true;
    }

    static void AP(ArrayList<ArrayList<Integer> > adj, int V)
    {
        boolean[] visited = new boolean[V];
        int[] disc = new int[V];
        int[] low = new int[V];
        boolean[] isAP = new boolean[V];
        int time = 0, par = -1;

        // Adding this loop so that the
        // code works even if we are given
        // disconnected graph
        for (int u = 0; u < V; u++)
            if (visited[u] == false)
                APUtil(adj, u, visited, disc, low, par, isAP);

        for (int u = 0; u < V; u++)
            if (isAP[u] == true)
                System.out.print(u + " ");
        System.out.println();
    }

    public static void main(String[] args)
    {

        // Creating first example graph
        int V = 5;
        ArrayList<ArrayList<Integer> > adj1 = 
                         new ArrayList<ArrayList<Integer> >(V);
        for (int i = 0; i < V; i++)
            adj1.add(new ArrayList<Integer>());
        addEdge(adj1, 1, 0);
        addEdge(adj1, 0, 2);
        addEdge(adj1, 2, 1);
        addEdge(adj1, 0, 3);
        addEdge(adj1, 3, 4);
        System.out.println("Articulation points in first graph");
        AP(adj1, V);

        // Creating second example graph
        V = 4;
        ArrayList<ArrayList<Integer> > adj2 = 
                         new ArrayList<ArrayList<Integer> >(V);
        for (int i = 0; i < V; i++)
            adj2.add(new ArrayList<Integer>());

        addEdge(adj2, 0, 1);
        addEdge(adj2, 1, 2);
        addEdge(adj2, 2, 3);

        System.out.println("Articulation points in second graph");
        AP(adj2, V);

        // Creating third example graph
        V = 7;
        ArrayList<ArrayList<Integer> > adj3 = 
                            new ArrayList<ArrayList<Integer> >(V);
        for (int i = 0; i < V; i++)
            adj3.add(new ArrayList<Integer>());

        addEdge(adj3, 0, 1);
        addEdge(adj3, 1, 2);
        addEdge(adj3, 2, 0);
        addEdge(adj3, 1, 3);
        addEdge(adj3, 1, 4);
        addEdge(adj3, 1, 6);
        addEdge(adj3, 3, 5);
        addEdge(adj3, 4, 5);

        System.out.println("Articulation points in third graph");

        AP(adj3, V);
    }
}
```

## 计算机编程语言

```
# Python program to find articulation points in an undirected graph

from collections import defaultdict

# This class represents an undirected graph 
# using adjacency list representation
class Graph:

    def __init__(self, vertices):
        self.V = vertices # No. of vertices
        self.graph = defaultdict(list) # default dictionary to store graph
        self.Time = 0

    # function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)
        self.graph[v].append(u)

    '''A recursive function that find articulation points 
    using DFS traversal
    u --> The vertex to be visited next
    visited[] --> keeps track of visited vertices
    disc[] --> Stores discovery times of visited vertices
    parent[] --> Stores parent vertices in DFS tree
    ap[] --> Store articulation points'''
    def APUtil(self, u, visited, ap, parent, low, disc):

        # Count of children in current node 
        children = 0

        # Mark the current node as visited and print it
        visited[u]= True

        # Initialize discovery time and low value
        disc[u] = self.Time
        low[u] = self.Time
        self.Time += 1

        # Recur for all the vertices adjacent to this vertex
        for v in self.graph[u]:
            # If v is not visited yet, then make it a child of u
            # in DFS tree and recur for it
            if visited[v] == False :
                parent[v] = u
                children += 1
                self.APUtil(v, visited, ap, parent, low, disc)

                # Check if the subtree rooted with v has a connection to
                # one of the ancestors of u
                low[u] = min(low[u], low[v])

                # u is an articulation point in following cases
                # (1) u is root of DFS tree and has two or more children.
                if parent[u] == -1 and children > 1:
                    ap[u] = True

                #(2) If u is not root and low value of one of its child is more
                # than discovery value of u.
                if parent[u] != -1 and low[v] >= disc[u]:
                    ap[u] = True    

                # Update low value of u for parent function calls    
            elif v != parent[u]: 
                low[u] = min(low[u], disc[v])

    # The function to do DFS traversal. It uses recursive APUtil()
    def AP(self):

        # Mark all the vertices as not visited 
        # and Initialize parent and visited, 
        # and ap(articulation point) arrays
        visited = [False] * (self.V)
        disc = [float("Inf")] * (self.V)
        low = [float("Inf")] * (self.V)
        parent = [-1] * (self.V)
        ap = [False] * (self.V) # To store articulation points

        # Call the recursive helper function
        # to find articulation points
        # in DFS tree rooted with vertex 'i'
        for i in range(self.V):
            if visited[i] == False:
                self.APUtil(i, visited, ap, parent, low, disc)

        for index, value in enumerate (ap):
            if value == True: print index,

 # Create a graph given in the above diagram
g1 = Graph(5)
g1.addEdge(1, 0)
g1.addEdge(0, 2)
g1.addEdge(2, 1)
g1.addEdge(0, 3)
g1.addEdge(3, 4)

print "\nArticulation points in first graph "
g1.AP()

g2 = Graph(4)
g2.addEdge(0, 1)
g2.addEdge(1, 2)
g2.addEdge(2, 3)
print "\nArticulation points in second graph "
g2.AP()

g3 = Graph (7)
g3.addEdge(0, 1)
g3.addEdge(1, 2)
g3.addEdge(2, 0)
g3.addEdge(1, 3)
g3.addEdge(1, 4)
g3.addEdge(1, 6)
g3.addEdge(3, 5)
g3.addEdge(4, 5)
print "\nArticulation points in third graph "
g3.AP()

# This code is contributed by Neelam Yadav
```

## C#

```
// A C# program to find articulation
// points in an undirected graph
using System;
using System.Collections.Generic;

// This class represents an undirected graph
// using adjacency list representation
public class Graph {
    private int V; // No. of vertices

    // Array of lists for Adjacency List Representation
    private List<int>[] adj;
    int time = 0;
    static readonly int NIL = -1;

    // Constructor
    Graph(int v)
    {
        V = v;
        adj = new List<int>[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new List<int>();
    }

    // Function to add an edge into the graph
    void addEdge(int v, int w)
    {
        adj[v].Add(w); // Add w to v's list.
        adj[w].Add(v); // Add v to w's list
    }

    // A recursive function that find articulation points using DFS
    // u --> The vertex to be visited next
    // visited[] --> keeps track of visited vertices
    // disc[] --> Stores discovery times of visited vertices
    // parent[] --> Stores parent vertices in DFS tree
    // ap[] --> Store articulation points
    void APUtil(int u, bool[] visited, int[] disc,
                int[] low, int[] parent, bool[] ap)
    {

        // Count of children in DFS Tree
        int children = 0;

        // Mark the current node as visited
        visited[u] = true;

        // Initialize discovery time and low value
        disc[u] = low[u] = ++time;

        // Go through all vertices aadjacent to this
        foreach(int i in adj[u])
        {
            int v = i; // v is current adjacent of u

            // If v is not visited yet, then make it a child of u
            // in DFS tree and recur for it
            if (!visited[v]) {
                children++;
                parent[v] = u;
                APUtil(v, visited, disc, low, parent, ap);

                // Check if the subtree rooted with v has
                // a connection to one of the ancestors of u
                low[u] = Math.Min(low[u], low[v]);

                // u is an articulation point in following cases

                // (1) u is root of DFS tree and has two or more children.
                if (parent[u] == NIL && children > 1)
                    ap[u] = true;

                // (2) If u is not root and low value of one of its child
                // is more than discovery value of u.
                if (parent[u] != NIL && low[v] >= disc[u])
                    ap[u] = true;
            }

            // Update low value of u for parent function calls.
            else if (v != parent[u])
                low[u] = Math.Min(low[u], disc[v]);
        }
    }

    // The function to do DFS traversal.
    // It uses recursive function APUtil()
    void AP()
    {
        // Mark all the vertices as not visited
        bool[] visited = new bool[V];
        int[] disc = new int[V];
        int[] low = new int[V];
        int[] parent = new int[V];
        bool[] ap = new bool[V]; // To store articulation points

        // Initialize parent and visited, and
        // ap(articulation point) arrays
        for (int i = 0; i < V; i++) {
            parent[i] = NIL;
            visited[i] = false;
            ap[i] = false;
        }

        // Call the recursive helper function to find articulation
        // points in DFS tree rooted with vertex 'i'
        for (int i = 0; i < V; i++)
            if (visited[i] == false)
                APUtil(i, visited, disc, low, parent, ap);

        // Now ap[] contains articulation points, print them
        for (int i = 0; i < V; i++)
            if (ap[i] == true)
                Console.Write(i + " ");
    }

    // Driver method
    public static void Main(String[] args)
    {
        // Create graphs given in above diagrams
        Console.WriteLine("Articulation points in first graph ");
        Graph g1 = new Graph(5);
        g1.addEdge(1, 0);
        g1.addEdge(0, 2);
        g1.addEdge(2, 1);
        g1.addEdge(0, 3);
        g1.addEdge(3, 4);
        g1.AP();
        Console.WriteLine();

        Console.WriteLine("Articulation points in Second graph");
        Graph g2 = new Graph(4);
        g2.addEdge(0, 1);
        g2.addEdge(1, 2);
        g2.addEdge(2, 3);
        g2.AP();
        Console.WriteLine();

        Console.WriteLine("Articulation points in Third graph ");
        Graph g3 = new Graph(7);
        g3.addEdge(0, 1);
        g3.addEdge(1, 2);
        g3.addEdge(2, 0);
        g3.addEdge(1, 3);
        g3.addEdge(1, 4);
        g3.addEdge(1, 6);
        g3.addEdge(3, 5);
        g3.addEdge(4, 5);
        g3.AP();
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// A Javascript program to find articulation points in an undirected graph

// This class represents an undirected graph using adjacency list
// representation
class Graph
{
    // Constructor
    constructor(v)
    {
        this.V = v;
        this.adj = new Array(v);
        this.NIL = -1;
        this.time = 0;
        for (let i=0; i<v; ++i)
            this.adj[i] = [];
    }

    //Function to add an edge into the graph
    addEdge(v, w)
    {
        this.adj[v].push(w);  // Add w to v's list.
        this.adj[w].push(v);    //Add v to w's list
    }

    // A recursive function that find articulation points using DFS
    // u --> The vertex to be visited next
    // visited[] --> keeps track of visited vertices
    // disc[] --> Stores discovery times of visited vertices
    // parent[] --> Stores parent vertices in DFS tree
    // ap[] --> Store articulation points
    APUtil(u, visited, disc, low, parent, ap)
    {
        // Count of children in DFS Tree
        let children = 0;

        // Mark the current node as visited
        visited[u] = true;

        // Initialize discovery time and low value
        disc[u] = low[u] = ++this.time;

        // Go through all vertices adjacent to this

        for(let i of this.adj[u])
        {
            let v = i;  // v is current adjacent of u

            // If v is not visited yet, then make it a child of u
            // in DFS tree and recur for it
            if (!visited[v])
            {
                children++;
                parent[v] = u;
                this.APUtil(v, visited, disc, low, parent, ap);

                // Check if the subtree rooted with v has a connection to
                // one of the ancestors of u
                low[u]  = Math.min(low[u], low[v]);

                // u is an articulation point in following cases

                // (1) u is root of DFS tree and has two or more children.
                if (parent[u] == this.NIL && children > 1)
                    ap[u] = true;

                // (2) If u is not root and low value of one of its child
                // is more than discovery value of u.
                if (parent[u] != this.NIL && low[v] >= disc[u])
                    ap[u] = true;
            }

            // Update low value of u for parent function calls.
            else if (v != parent[u])
                low[u]  = Math.min(low[u], disc[v]);
        }
    }

    // The function to do DFS traversal. It uses recursive function APUtil()
    AP()
    {
        // Mark all the vertices as not visited
        let visited = new Array(this.V);
        let disc = new Array(this.V);
        let low = new Array(this.V);
        let parent = new Array(this.V);
        let ap = new Array(this.V); // To store articulation points

        // Initialize parent and visited, and ap(articulation point)
        // arrays
        for (let i = 0; i < this.V; i++)
        {
            parent[i] = this.NIL;
            visited[i] = false;
            ap[i] = false;
        }

        // Call the recursive helper function to find articulation
        // points in DFS tree rooted with vertex 'i'
        for (let i = 0; i < this.V; i++)
            if (visited[i] == false)
                this.APUtil(i, visited, disc, low, parent, ap);

        // Now ap[] contains articulation points, print them
        for (let i = 0; i < this.V; i++)
            if (ap[i] == true)
                document.write(i+" ");
    }
}

// Driver method
// Create graphs given in above diagrams
document.write("Articulation points in first graph  <br>");
let g1 = new Graph(5);
g1.addEdge(1, 0);
g1.addEdge(0, 2);
g1.addEdge(2, 1);
g1.addEdge(0, 3);
g1.addEdge(3, 4);
g1.AP();
document.write("<br>");

document.write("Articulation points in Second graph <br>");
let g2 = new Graph(4);
g2.addEdge(0, 1);
g2.addEdge(1, 2);
g2.addEdge(2, 3);
g2.AP();
document.write("<br>");

document.write("Articulation points in Third graph  <br>");
let g3 = new Graph(7);
g3.addEdge(0, 1);
g3.addEdge(1, 2);
g3.addEdge(2, 0);
g3.addEdge(1, 3);
g3.addEdge(1, 4);
g3.addEdge(1, 6);
g3.addEdge(3, 5);
g3.addEdge(4, 5);
g3.AP();

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Articulation points in first graph
0 3
Articulation points in second graph
1 2
Articulation points in third graph
1
```

**时间复杂度:**上面的函数是带有附加数组的简单 DFS。因此时间复杂度与图的邻接表表示的 O(V+E)的 DFS 相同。

**参考文献:**
[https://www . cs . Washington . edu/education/courses/421/04su/slides/artic . pdf](https://www.cs.washington.edu/education/courses/421/04su/slides/artic.pdf)
[http://www . slide share . net/traianrebeda/algorithm-design-and-complex-course-8](http://www.slideshare.net/TraianRebedea/algorithm-design-and-complexity-course-8)
[http://facility . Simpson . edu/Lydia . sinapova/www/cmsc 250/ln 250 _ Weiss/L25-connectivity . HTS](http://faculty.simpson.edu/lydia.sinapova/www/cmsc250/LN250_Weiss/L25-Connectivity.htm)