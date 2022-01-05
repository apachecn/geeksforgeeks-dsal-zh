# 使用 DFS 的图的传递闭包

> 原文:[https://www . geeksforgeeks . org/transitive-图的闭包-使用-dfs/](https://www.geeksforgeeks.org/transitive-closure-of-a-graph-using-dfs/)

给定一个有向图，对于给定图中的所有顶点对(u，v)，找出一个顶点 v 是否可以从另一个顶点 u 到达。这里的可达是指从顶点 u 到 v 有一条路径，可达能力矩阵称为图的传递闭包。

```
For example, consider below graph

Transitive closure of above graphs is 
     1 1 1 1 
     1 1 1 1 
     1 1 1 1 
     0 0 0 1 
```

我们在这里讨论了这个[的 O(V <sup>3</sup> )解。解决方案基于](https://www.geeksforgeeks.org/transitive-closure-of-a-graph/)[弗洛伊德·沃肖尔算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)。在这篇文章中，我们讨论了一个 O(V(V+E))算法。所以对于密集图，会变成 O(V <sup>3</sup> )，对于稀疏图，会变成 O(V <sup>2</sup> )。
下面是算法的抽象步骤。

1.  创建一个矩阵 tc[V][V]，它将最终拥有给定图的传递闭包。将 tc[][]的所有条目初始化为 0。
2.  调用图的每个节点的 DFS 来标记 tc[][]中的可达顶点。在对 DFS 的递归调用中，如果相邻顶点在 tc[][]中已经被标记为可达，我们就不为它调用 DFS。

以下是上述想法的实现。该代码使用输入图的邻接表表示，并建立一个矩阵 tc[V][V]，使得 tc[u][v]为真，如果 V 可从 u
到达

## C++

```
// C++ program to print transitive closure of a graph
#include<bits/stdc++.h>
using namespace std;

class Graph
{
    int V; // No. of vertices
    bool **tc; // To store transitive closure
    list<int> *adj; // array of adjacency lists
    void DFSUtil(int u, int v);
public:
    Graph(int V); // Constructor

    // function to add an edge to graph
    void addEdge(int v, int w) { adj[v].push_back(w); }

    // prints transitive closure matrix
    void transitiveClosure();
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];

    tc = new bool* [V];
    for (int i = 0; i < V; i++)
    {
        tc[i] = new bool[V];
        memset(tc[i], false, V*sizeof(bool));
    }
}

// A recursive DFS traversal function that finds
// all reachable vertices for s.
void Graph::DFSUtil(int s, int v)
{
    // Mark reachability from s to t as true.
     if(s==v){
        if(find(adj[v].begin(),adj[v].end(),v)!=adj[v].end())
          tc[s][v] = true;
          }
      else
            tc[s][v] = true;

    // Find all the vertices reachable through v
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
    {
        if (tc[s][*i] == false)
        {
           if(*i==s)
           {
              tc[s][*i]=1;
             }
            else
            {
              DFSUtil(s, *i);
            }
        }
    }
}

// The function to find transitive closure. It uses
// recursive DFSUtil()
void Graph::transitiveClosure()
{
    // Call the recursive helper function to print DFS
    // traversal starting from all vertices one by one
    for (int i = 0; i < V; i++)
        DFSUtil(i, i); // Every vertex is reachable from self.

    for (int i=0; i<V; i++)
    {
        for (int j=0; j<V; j++)
            cout << tc[i][j] << " ";
        cout << endl;
    }
}

// Driver code
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
    cout << "Transitive closure matrix is \n";
    g.transitiveClosure();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print transitive
// closure of a graph.

import java.util.ArrayList;
import java.util.Arrays;

// A directed graph using
// adjacency list representation
public class Graph {

        // No. of vertices in graph
    private int vertices;

        // adjacency list
    private ArrayList<Integer>[] adjList;

        // To store transitive closure
    private int[][] tc;

    // Constructor
    public Graph(int vertices) {

             // initialise vertex count
             this.vertices = vertices;
             this.tc = new int[this.vertices][this.vertices];

             // initialise adjacency list
             initAdjList();
    }

    // utility method to initialise adjacency list
    @SuppressWarnings("unchecked")
    private void initAdjList() {

        adjList = new ArrayList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjList[i] = new ArrayList<>();
        }
    }

    // add edge from u to v
    public void addEdge(int u, int v) {

      // Add v to u's list.
        adjList[u].add(v);
    }

    // The function to find transitive
    // closure. It uses
    // recursive DFSUtil()
    public void transitiveClosure() {

        // Call the recursive helper
        // function to print DFS
        // traversal starting from all
        // vertices one by one
        for (int i = 0; i < vertices; i++) {
            dfsUtil(i, i);
        }

        for (int i = 0; i < vertices; i++) {
          System.out.println(Arrays.toString(tc[i]));
        }
    }

    // A recursive DFS traversal
    // function that finds
    // all reachable vertices for s
    private void dfsUtil(int s, int v) {

        // Mark reachability from
        // s to v as true.
       if(s==v){
        if(adjList[v].contains(v))
          tc[s][v] = 1;
          }
      else
        tc[s][v] = 1;

        // Find all the vertices reachable
        // through v
        for (int adj : adjList[v]) {           
            if (tc[s][adj]==0) {
                dfsUtil(s, adj);
            }
        }
    }

    // Driver Code
    public static void main(String[] args) {

        // Create a graph given
        // in the above diagram
        Graph g = new Graph(4);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 3);
        System.out.println("Transitive closure " +
                "matrix is");

        g.transitiveClosure();

    }
}

// This code is contributed
// by Himanshu Shekhar
```

## 计算机编程语言

```
# Python program to print transitive
# closure of a graph.
from collections import defaultdict

class Graph:

    def __init__(self,vertices):
        # No. of vertices
        self.V = vertices

        # default dictionary to store graph
        self.graph = defaultdict(list)

        # To store transitive closure
        self.tc = [[0 for j in range(self.V)] for i in range(self.V)]

    # function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)

    # A recursive DFS traversal function that finds
    # all reachable vertices for s
    def DFSUtil(self, s, v):

        # Mark reachability from s to v as true.
        if(s == v):
            if( v in self.graph[s]):
              self.tc[s][v] = 1
        else:
            self.tc[s][v] = 1

        # Find all the vertices reachable through v
        for i in self.graph[v]:
            if self.tc[s][i] == 0:
                if s==i:
                   self.tc[s][i]=1
                else:
                   self.DFSUtil(s, i)

    # The function to find transitive closure. It uses
    # recursive DFSUtil()
    def transitiveClosure(self):

        # Call the recursive helper function to print DFS
        # traversal starting from all vertices one by one
        for i in range(self.V):
            self.DFSUtil(i, i)

        print(self.tc)

# Create a graph given in the above diagram
g = Graph(4)
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(1, 2)
g.addEdge(2, 0)
g.addEdge(2, 3)
g.addEdge(3, 3)

g.transitiveClosure()
```

## C#

```
// C# program to print transitive
// closure of a graph.
using System;
using System.Collections.Generic;

// A directed graph using
// adjacency list representation
public class Graph
{

  // No. of vertices in graph
  private int vertices;

  // adjacency list
  private List<int>[] adjList;

  // To store transitive closure
  private int[,] tc;

  // Constructor
  public Graph(int vertices)
  {

    // initialise vertex count
    this.vertices = vertices;
    this.tc = new int[this.vertices, this.vertices];

    // initialise adjacency list
    initAdjList();
  }

  // utility method to initialise adjacency list
  private void initAdjList()
  {

    adjList = new List<int>[vertices];
    for (int i = 0; i < vertices; i++)
    {
      adjList[i] = new List<int>();
    }
  }

  // add edge from u to v
  public void addEdge(int u, int v)
  {

    // Add v to u's list.
    adjList[u].Add(v);
  }

  // The function to find transitive
  // closure. It uses
  // recursive DFSUtil()
  public void transitiveClosure() {

    // Call the recursive helper
    // function to print DFS
    // traversal starting from all
    // vertices one by one
    for (int i = 0; i < vertices; i++) {
      dfsUtil(i, i);
    }

    for (int i = 0; i < vertices; i++) {
      for(int j = 0; j < vertices; j++)
        Console.Write(tc[i, j] + " ");
      Console.WriteLine();
    }
  }

  // A recursive DFS traversal
  // function that finds
  // all reachable vertices for s
  private void dfsUtil(int s, int v) {

    // Mark reachability from
    // s to v as true.
     if(s==v){
        if(adjList[v].contains(v))
          tc[s][v] = 1;
          }
      else
    tc[s, v] = 1;

    // Find all the vertices reachable
    // through v
    foreach (int adj in adjList[v])
    {           
      if (tc[s, adj] == 0) {
        dfsUtil(s, adj);
      }
    }
  }

  // Driver Code
  public static void Main(String[] args) {

    // Create a graph given
    // in the above diagram
    Graph g = new Graph(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);
    Console.WriteLine("Transitive closure " +
                      "matrix is");
    g.transitiveClosure();
  }
}

// This code is contributed by Rajput-Ji
```

**Output**

```
Transitive closure matrix is 
1 1 1 1 
1 1 1 1 
1 1 1 1 
0 0 0 1 

```

输出:

```
Transitive closure matrix is 
1 1 1 1 
1 1 1 1 
1 1 1 1 
0 0 0 1 
```

**参考文献:**
[http://www . cs . Princeton . edu/courses/archive/SPR 03/cs 226/讲座/digraph.4up.pdf](http://www.cs.princeton.edu/courses/archive/spr03/cs226/lectures/digraph.4up.pdf)
本文由 **Aditya Goel** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息