# 不交集（或联合查找）| 设置 1（无向图中的检测周期）

> 原文： [https://www.geeksforgeeks.org/union-find/](https://www.geeksforgeeks.org/union-find/)

[*不相交集数据结构*](http://en.wikipedia.org/wiki/Disjoint-set_data_structure) 是一种数据结构，可跟踪划分为多个不相交（不重叠）子集的元素集。 [*联合查找算法*](http://en.wikipedia.org/wiki/Disjoint-set_data_structure) 是对这样的数据结构执行两个有用操作的算法：

***查找**：* 确定哪个 特定元素所在的子集。这可用于确定两个元素是否在同一子集中。

***联合**：* 将两个子集合并为一个子集。

在这篇文章中，我们将讨论不交集数据结构的应用。 该应用程序将检查给定图是否包含循环。

*联合查找算法*可用于检查无向图是否包含循环。 注意，我们已经讨论了用于检测周期的[算法。 这是基于*联合查找*的另一种方法。 此方法假定图表不包含任何自环。

我们可以跟踪一维数组中的子集，我们称其为父级[]。

让我们考虑下图：](http://www.geeksforgeeks.org/archives/18516) 

![cycle-in-graph](img/1ea01f69a0b830381c4c00cf41ed2aa6.png)

对于每个边，使用边的两个顶点制作子集。 如果两个顶点都在同一子集中，则会找到一个循环。

最初，父阵列的所有插槽均初始化为-1（意味着每个子集中只有一项）。

```
0   1   2
-1 -1  -1 

```

现在一一处理所有边。

*边 0-1：*查找顶点 0 和 1 所在的子集。 由于它们位于不同的子集中，因此我们将它们合并。 对于采用并集，请将节点 0 设为节点 1 的父级，反之亦然。

```
0   1   2    <----- 1 is made parent of 0 (1 is now representative of subset {0, 1})
1  -1  -1

```

*边 1-2：* 1 位于子集 1 中，2 位于子集 2 中。因此，取并集。

```
0   1   2    <----- 2 is made parent of 1 (2 is now representative of subset {0, 1, 2})
1   2  -1

```

*边沿 0-2：* 0 在子集 2 中，而 2 在子集 2 中。因此，包括此边沿将形成一个循环。

0 的子集如何与 2 相同？

0- > 1- > 2 // 1 是 0 的父级，2 是 1 的父级

根据以上说明，以下是实现：

## C++

```cpp

// A union-find algorithm to detect cycle in a graph
#include <bits/stdc++.h>
using namespace std;

// a structure to represent an edge in graph
class Edge 
{
public:
    int src, dest;
};

// a structure to represent a graph
class Graph 
{
public:
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges
    Edge* edge;
};

// Creates a graph with V vertices and E edges
Graph* createGraph(int V, int E)
{
    Graph* graph = new Graph();
    graph->V = V;
    graph->E = E;

    graph->edge = new Edge[graph->E * sizeof(Edge)];

    return graph;
}

// A utility function to find the subset of an element i
int find(int parent[], int i)
{
    if (parent[i] == -1)
        return i;
    return find(parent, parent[i]);
}

// A utility function to do union of two subsets
void Union(int parent[], int x, int y)
{
    parent[x] = y;
}

// The main function to check whether a given graph contains
// cycle or not
int isCycle(Graph* graph)
{
    // Allocate memory for creating V subsets
    int* parent = new int[graph->V * sizeof(int)];

    // Initialize all subsets as single element sets
    memset(parent, -1, sizeof(int) * graph->V);

    // Iterate through all edges of graph, find subset of
    // both vertices of every edge, if both subsets are
    // same, then there is cycle in graph.
    for (int i = 0; i < graph->E; ++i) {
        int x = find(parent, graph->edge[i].src);
        int y = find(parent, graph->edge[i].dest);

        if (x == y)
            return 1;

        Union(parent, x, y);
    }
    return 0;
}

// Driver code
int main()
{
    /* Let us create the following graph
        0
        | \
        |  \
        1---2 */
    int V = 3, E = 3;
    Graph* graph = createGraph(V, E);

    // add edge 0-1
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;

    // add edge 1-2
    graph->edge[1].src = 1;
    graph->edge[1].dest = 2;

    // add edge 0-2
    graph->edge[2].src = 0;
    graph->edge[2].dest = 2;

    if (isCycle(graph))
        cout << "graph contains cycle";
    else
        cout << "graph doesn't contain cycle";

    return 0;
}

// This code is contributed by rathbhupendra

```

## C

```c

// A union-find algorithm to detect cycle in a graph
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// a structure to represent an edge in graph
struct Edge
{
    int src, dest;
};

// a structure to represent a graph
struct Graph
{
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges
    struct Edge* edge;
};

// Creates a graph with V vertices and E edges
struct Graph* createGraph(int V, int E)
{
    struct Graph* graph = 
           (struct Graph*) malloc( sizeof(struct Graph) );
    graph->V = V;
    graph->E = E;

    graph->edge = 
        (struct Edge*) malloc( graph->E * sizeof( struct Edge ) );

    return graph;
}

// A utility function to find the subset of an element i
int find(int parent[], int i)
{
    if (parent[i] == -1)
        return i;
    return find(parent, parent[i]);
}

// A utility function to do union of two subsets 
void Union(int parent[], int x, int y)
{
    int xset = find(parent, x);
    int yset = find(parent, y);
    if(xset!=yset){
       parent[xset] = yset;
    }
}

// The main function to check whether a given graph contains 
// cycle or not
int isCycle( struct Graph* graph )
{
    // Allocate memory for creating V subsets
    int *parent = (int*) malloc( graph->V * sizeof(int) );

    // Initialize all subsets as single element sets
    memset(parent, -1, sizeof(int) * graph->V);

    // Iterate through all edges of graph, find subset of both
    // vertices of every edge, if both subsets are same, then 
    // there is cycle in graph.
    for(int i = 0; i < graph->E; ++i)
    {
        int x = find(parent, graph->edge[i].src);
        int y = find(parent, graph->edge[i].dest);

        if (x == y)
            return 1;

        Union(parent, x, y);
    }
    return 0;
}

// Driver program to test above functions
int main()
{
    /* Let us create the following graph 
        0 
        | \ 
        |  \ 
        1---2 */ 
    int V = 3, E = 3;
    struct Graph* graph = createGraph(V, E);

    // add edge 0-1
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;

    // add edge 1-2
    graph->edge[1].src = 1;
    graph->edge[1].dest = 2;

    // add edge 0-2
    graph->edge[2].src = 0;
    graph->edge[2].dest = 2;

    if (isCycle(graph))
        printf( "graph contains cycle" );
    else
        printf( "graph doesn't contain cycle" );

    return 0;
}

```

## Java

```java

// Java Program for union-find algorithm to detect cycle in a graph
import java.util.*;
import java.lang.*;
import java.io.*;

class Graph
{
    int V, E;    // V-> no. of vertices & E->no.of edges
    Edge edge[]; // /collection of all edges

    class Edge
    {
        int src, dest;
    };

    // Creates a graph with V vertices and E edges
    Graph(int v,int e)
    {
        V = v;
        E = e;
        edge = new Edge[E];
        for (int i=0; i<e; ++i)
            edge[i] = new Edge();
    }

    // A utility function to find the subset of an element i
    int find(int parent[], int i)
    {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    // A utility function to do union of two subsets
    void Union(int parent[], int x, int y)
    {
        int xset = find(parent, x);
        int yset = find(parent, y);
        parent[xset] = yset;
    }

    // The main function to check whether a given graph
    // contains cycle or not
    int isCycle( Graph graph)
    {
        // Allocate memory for creating V subsets
        int parent[] = new int[graph.V];

        // Initialize all subsets as single element sets
        for (int i=0; i<graph.V; ++i)
            parent[i]=-1;

        // Iterate through all edges of graph, find subset of both
        // vertices of every edge, if both subsets are same, then
        // there is cycle in graph.
        for (int i = 0; i < graph.E; ++i)
        {
            int x = graph.find(parent, graph.edge[i].src);
            int y = graph.find(parent, graph.edge[i].dest);

            if (x == y)
                return 1;

            graph.Union(parent, x, y);
        }
        return 0;
    }

    // Driver Method
    public static void main (String[] args)
    {
        /* Let us create the following graph 
        0 
        | \ 
        |  \ 
        1---2 */
        int V = 3, E = 3;
        Graph graph = new Graph(V, E);

        // add edge 0-1
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;

        // add edge 1-2
        graph.edge[1].src = 1;
        graph.edge[1].dest = 2;

        // add edge 0-2
        graph.edge[2].src = 0;
        graph.edge[2].dest = 2;

        if (graph.isCycle(graph)==1)
            System.out.println( "graph contains cycle" );
        else
            System.out.println( "graph doesn't contain cycle" );
    }
}

```

## Python

```py

# Python Program for union-find algorithm to detect cycle in a undirected graph
# we have one egde for any two vertex i.e 1-2 is either 1-2 or 2-1 but not both

from collections import defaultdict

#This class represents a undirected graph using adjacency list representation
class Graph:

    def __init__(self,vertices):
        self.V= vertices #No. of vertices
        self.graph = defaultdict(list) # default dictionary to store graph

    # function to add an edge to graph
    def addEdge(self,u,v):
        self.graph[u].append(v)

    # A utility function to find the subset of an element i
    def find_parent(self, parent,i):
        if parent[i] == -1:
            return i
        if parent[i]!= -1:
             return self.find_parent(parent,parent[i])

    # A utility function to do union of two subsets
    def union(self,parent,x,y):
        x_set = self.find_parent(parent, x)
        y_set = self.find_parent(parent, y)
        parent[x_set] = y_set

    # The main function to check whether a given graph
    # contains cycle or not
    def isCyclic(self):

        # Allocate memory for creating V subsets and
        # Initialize all subsets as single element sets
        parent = [-1]*(self.V)

        # Iterate through all edges of graph, find subset of both
        # vertices of every edge, if both subsets are same, then
        # there is cycle in graph.
        for i in self.graph:
            for j in self.graph[i]:
                x = self.find_parent(parent, i) 
                y = self.find_parent(parent, j)
                if x == y:
                    return True
                self.union(parent,x,y)

# Create a graph given in the above diagram
g = Graph(3)
g.addEdge(0, 1)
g.addEdge(1, 2)
g.addEdge(2, 0)

if g.isCyclic():
    print "Graph contains cycle"
else :
    print "Graph does not contain cycle "

#This code is contributed by Neelam Yadav

```

## C#

```cs

// C# Program for union-find 
// algorithm to detect cycle 
// in a graph
using System;
class Graph{

// V-> no. of vertices & 
// E->no.of edges  
public int V, E;    

// collection of all edges
public Edge []edge; 

class Edge
{
  public int src, dest;
};

// Creates a graph with V 
// vertices and E edges
public  Graph(int v,int e)
{
  V = v;
  E = e;
  edge = new Edge[E];

  for (int i = 0; i < e; ++i)
    edge[i] = new Edge();
}

// A utility function to find 
// the subset of an element i
int find(int []parent, int i)
{
  if (parent[i] == -1)
    return i;
  return find(parent, 
              parent[i]);
}

// A utility function to do 
// union of two subsets
void Union(int []parent, 
           int x, int y)
{
  int xset = find(parent, x);
  int yset = find(parent, y);
  parent[xset] = yset;
}

// The main function to check 
// whether a given graph
// contains cycle or not
int isCycle(Graph graph)
{
  // Allocate memory for 
  // creating V subsets
  int []parent = 
        new int[graph.V];

  // Initialize all subsets as 
  // single element sets
  for (int i = 0; i < graph.V; ++i)
    parent[i] =- 1;

  // Iterate through all edges of graph, 
  // find subset of both vertices of every 
  // edge, if both subsets are same, then 
  // there is cycle in graph.
  for (int i = 0; i < graph.E; ++i)
  {
    int x = graph.find(parent, 
                       graph.edge[i].src);
    int y = graph.find(parent, 
                       graph.edge[i].dest);

    if (x == y)
      return 1;

    graph.Union(parent, x, y);
  }
  return 0;
}

// Driver code
public static void Main(String[] args)
{
  /* Let us create the following graph 
        0 
        | \ 
        |  \ 
        1---2 */
  int V = 3, E = 3;
  Graph graph = new Graph(V, E);

  // add edge 0-1
  graph.edge[0].src = 0;
  graph.edge[0].dest = 1;

  // add edge 1-2
  graph.edge[1].src = 1;
  graph.edge[1].dest = 2;

  // add edge 0-2
  graph.edge[2].src = 0;
  graph.edge[2].dest = 2;

  if (graph.isCycle(graph) == 1)
    Console.WriteLine("graph contains cycle");
  else
    Console.WriteLine("graph doesn't contain cycle");
}
}

// This code is contributed by Princi Singh

```

**输出**：

```
graph contains cycle

```

请注意， *union（）*和 *find（）*的实现是幼稚的，在最坏的情况下需要 O（n）时间。 可以使用 *Union by Rank 或 Height* 将这些方法改进为 O（Logn）。 我们很快将在另一篇文章中讨论*排名*联盟。

https://youtu.be/mHz-mx-8lJ8?list=PLqM7alHXFySEaZgcg7uRYJFBnYMLti-nh

**相关文章**：

[联合查找算法| 集合 2（按等级和路径压缩的并集） 第 2 组（Kruskal 的最小生成树算法）](http://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)，

[作业排序问题| 第 2 组（使用不交集）](http://www.geeksforgeeks.org/job-sequencing-using-disjoint-set-union/)

本文由 [Aashish Barnwal](https://www.facebook.com/barnwal.aashish) 编译，并由 GeeksforGeeks 团队进行了审查。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

