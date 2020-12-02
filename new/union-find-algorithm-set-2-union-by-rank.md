# 联合查找算法| 第 2 组（按等级和路径压缩合并）

> 原文： [https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)

在[之前的文章](https://www.geeksforgeeks.org/union-find/)中，我们介绍了*联合查找算法*，并将其用于检测图中的循环。 我们对子集使用以下 *union（）*和 *find（）*操作。

## CPP

```

// Naive implementation of find
int find(int parent[], int i)
{
    if (parent[i] == -1)
        return i;
    return find(parent, parent[i]);
}

// Naive implementation of union()
void Union(int parent[], int x, int y)
{
    int xset = find(parent, x);
    int yset = find(parent, y);
    parent[xset] = yset;
}

```

上面的 *union（）*和 *find（）*天真，最坏的情况下时间复杂度是线性的。 创建用来表示子集的树可能会倾斜，并且可能变得像链表一样。 以下是最坏情况的示例。

```
Let there be 4 elements 0, 1, 2, 3

Initially, all elements are single element subsets.
0 1 2 3 

Do Union(0, 1)
   1   2   3  
  /
 0

Do Union(1, 2)
     2   3   
    /
   1
 /
0

Do Union(2, 3)
         3    
        /
      2
     /
   1
 /
0

```

在最坏的情况下，可以将上述操作优化为 *O（Log n）*。 想法是始终将较小的深度树附加在较深树的根下。 将该技术按等级 称为 ***联合。 首选*等级*而不是高度，因为如果使用路径压缩技术（我们在下面进行了讨论），则*等级*并不总是等于高度。 此外，树木的大小（代替高度）也可以用作*等级*。 使用大小作为*等级*也会产生最坏情况的时间复杂度，即 O（Logn）（请参见[此](http://www.brpreiss.com/books/opus4/html/page411.html#theoremsetsi)作为证据）***

```
Let us see the above example with union by rank
Initially, all elements are single element subsets.
0 1 2 3 

Do Union(0, 1)
   1   2   3  
  /
 0

Do Union(1, 2)
   1    3
 /  \
0    2

Do Union(2, 3)
    1    
 /  |  \
0   2   3

```

天真的方法的第二个优化是 ***路径压缩*** 。 想法是在调用 *find（）*时将树展平。 当为元素 x 调用 *find（）*时，返回树的根。 *find（）*操作从 x 向上遍历以查找根。 路径压缩的想法是使找到的根成为 x 的父级，这样我们就不必再次遍历所有中间节点。 如果 x 是子树的根，则 x 下所有节点的路径（到根）也会压缩。

```
Let the subset {0, 1, .. 9} be represented as below and find() is called
for element 3.
              9
         /    |    \  
        4     5      6
     /     \        /  \
    0        3     7    8
            /  \
           1    2  

When *find()* is called for 3, we traverse up and find 9 as representative
of this subset. With path compression, we also make 3 as the child of 9 so 
that when find() is called next time for 1, 2 or 3, the path to root is reduced.

               9
         /    /  \    \
        4    5    6     3 
     /           /  \   /  \
    0           7    8  1   2           

```

两种技术相辅相成。 每个操作的时间复杂度甚至小于 O（Logn）。 实际上，摊销的时间复杂度实际上变为小的常数。
以下是基于等级和路径压缩的实现，以在图中查找循环。

## C++

```cpp

// A union by rank and path compression based program to
// detect cycle in a graph
#include <stdio.h>
#include <stdlib.h>

// a structure to represent an edge in the graph
struct Edge {
    int src, dest;
};

// a structure to represent a graph
struct Graph {
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges
    struct Edge* edge;
};

struct subset {
    int parent;
    int rank;
};

// Creates a graph with V vertices and E edges
struct Graph* createGraph(int V, int E)
{
    struct Graph* graph
        = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->E = E;

    graph->edge = (struct Edge*)malloc(
        graph->E * sizeof(struct Edge));

    return graph;
}

// A utility function to find set of an element i
// (uses path compression technique)
int find(struct subset subsets[], int i)
{
    // find root and make root as parent of i (path
    // compression)
    if (subsets[i].parent != i)
        subsets[i].parent
            = find(subsets, subsets[i].parent);

    return subsets[i].parent;
}

// A function that does union of two sets of x and y
// (uses union by rank)
void Union(struct subset subsets[], int xroot, int yroot)
{

    // Attach smaller rank tree under root of high rank tree
    // (Union by Rank)
    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;

    // If ranks are same, then make one as root and
    // increment its rank by one
    else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// The main function to check whether a given graph contains
// cycle or not
int isCycle(struct Graph* graph)
{
    int V = graph->V;
    int E = graph->E;

    // Allocate memory for creating V sets
    struct subset* subsets
        = (struct subset*)malloc(V * sizeof(struct subset));

    for (int v = 0; v < V; ++v) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    // Iterate through all edges of graph, find sets of both
    // vertices of every edge, if sets are same, then there
    // is cycle in graph.
    for (int e = 0; e < E; ++e) {
        int x = find(subsets, graph->edge[e].src);
        int y = find(subsets, graph->edge[e].dest);

        if (x == y)
            return 1;

        Union(subsets, x, y);
    }
    return 0;
}

// Driver code
int main()
{
    /* Let us create the following graph
         0
        |  \
        |    \
        1-----2 */

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
        printf("Graph contains cycle");
    else
        printf("Graph doesn't contain cycle");

    return 0;
}

```

## Java

```java

// A union by rank and path compression
// based program to detect cycle in a graph
class Graph 
{
    int V, E;
    Edge[] edge;

    Graph(int nV, int nE)
    {
        V = nV;
        E = nE;
        edge = new Edge[E];
        for (int i = 0; i < E; i++) 
        {
            edge[i] = new Edge();
        }
    }

    // class to represent edge
    class Edge 
    {
        int src, dest;
    }

    // class to represent Subset
    class subset 
    {
        int parent;
        int rank;
    }

    // A utility function to find
    // set of an element i (uses
    // path compression technique)
    int find(subset[] subsets, int i)
    {
        if (subsets[i].parent != i)
            subsets[i].parent
                = find(subsets, subsets[i].parent);
        return subsets[i].parent;
    }

    // A function that does union
    // of two sets of x and y
    // (uses union by rank)
    void Union(subset[] subsets, int x, int y)
    {
        int xroot = find(subsets, x);
        int yroot = find(subsets, y);

        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[yroot].rank < subsets[xroot].rank)
            subsets[yroot].parent = xroot;
        else {
            subsets[xroot].parent = yroot;
            subsets[yroot].rank++;
        }
    }

    // The main function to check whether
    // a given graph contains cycle or not
    int isCycle(Graph graph)
    {
        int V = graph.V;
        int E = graph.E;

        subset[] subsets = new subset[V];
        for (int v = 0; v < V; v++) {

            subsets[v] = new subset();
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        for (int e = 0; e < E; e++) {
            int x = find(subsets, graph.edge[e].src);
            int y = find(subsets, graph.edge[e].dest);
            if (x == y)
                return 1;
            Union(subsets, x, y);
        }
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        /* Let us create the following graph
            0
            | \
            | \
            1-----2 */

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
            System.out.println("Graph contains cycle");
        else
            System.out.println(
                "Graph doesn't contain cycle");
    }
}

// This code is contributed
// by ashwani khemani

```

## Python

```py

# A union by rank and path compression based
# program to detect cycle in a graph
from collections import defaultdict

# a structure to represent a graph

class Graph:

    def __init__(self, num_of_v):
        self.num_of_v = num_of_v
        self.edges = defaultdict(list)

    # graph is represented as an
    # array of edges
    def add_edge(self, u, v):
        self.edges[u].append(v)

class Subset:
    def __init__(self, parent, rank):
        self.parent = parent
        self.rank = rank

# A utility function to find set of an element
# node(uses path compression technique)

def find(subsets, node):
    if subsets[node].parent != node:
        subsets[node].parent = find(subsets, subsets[node].parent)
    return subsets[node].parent

# A function that does union of two sets
# of u and v(uses union by rank)

def union(subsets, u, v):

    # Attach smaller rank tree under root
    # of high rank tree(Union by Rank)
    if subsets[u].rank > subsets[v].rank:
        subsets[v].parent = u
    elif subsets[v].rank > subsets[u].rank:
        subsets[u].parent = v

    # If ranks are same, then make one as
    # root and increment its rank by one
    else:
        subsets[v].parent = u
        subsets[u].rank += 1

# The main function to check whether a given
# graph contains cycle or not

def isCycle(graph):

    # Allocate memory for creating sets
    subsets = []

    for u in range(graph.num_of_v):
        subsets.append(Subset(u, 0))

    # Iterate through all edges of graph,
    # find sets of both vertices of every
    # edge, if sets are same, then there
    # is cycle in graph.
    for u in graph.edges:
        u_rep = find(subsets, u)

        for v in graph.edges[u]:
            v_rep = find(subsets, v)

            if u_rep == v_rep:
                return True
            else:
                union(subsets, u_rep, v_rep)

# Driver Code
g = Graph(3)

# add edge 0-1
g.add_edge(0, 1)

# add edge 1-2
g.add_edge(1, 2)

# add edge 0-2
g.add_edge(0, 2)

if isCycle(g):
    print('Graph contains cycle')
else:
    print('Graph does not contain cycle')

# This code is contributed by
# Sampath Kumar Surine

```

## C#

```cs

// A union by rank and path compression
// based program to detect cycle in a graph
using System;

class Graph {
    public int V, E;
    public Edge[] edge;

    public Graph(int nV, int nE)
    {
        V = nV;
        E = nE;
        edge = new Edge[E];
        for (int i = 0; i < E; i++)
        {
            edge[i] = new Edge();
        }
    }

    // class to represent edge
    public class Edge {
        public int src, dest;
    }

    // class to represent Subset
    class subset 
    {
        public int parent;
        public int rank;
    }

    // A utility function to find
    // set of an element i (uses
    // path compression technique)
    int find(subset[] subsets, int i)
    {
        if (subsets[i].parent != i)
            subsets[i].parent
                = find(subsets, subsets[i].parent);
        return subsets[i].parent;
    }

    // A function that does union
    // of two sets of x and y
    // (uses union by rank)
    void Union(subset[] subsets, int x, int y)
    {
        int xroot = find(subsets, x);
        int yroot = find(subsets, y);

        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[yroot].rank < subsets[xroot].rank)
            subsets[yroot].parent = xroot;
        else {
            subsets[xroot].parent = yroot;
            subsets[yroot].rank++;
        }
    }

    // The main function to check whether
    // a given graph contains cycle or not
    int isCycle(Graph graph)
    {
        int V = graph.V;
        int E = graph.E;

        subset[] subsets = new subset[V];
        for (int v = 0; v < V; v++) 
        {
            subsets[v] = new subset();
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        for (int e = 0; e < E; e++) 
        {
            int x = find(subsets, graph.edge[e].src);
            int y = find(subsets, graph.edge[e].dest);
            if (x == y)
                return 1;
            Union(subsets, x, y);
        }
        return 0;
    }

    // Driver Code
    static public void Main(String[] args)
    {
        /* Let us create the following graph
            0
            | \
            | \
            1-----2 */

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
            Console.WriteLine("Graph contains cycle");
        else
            Console.WriteLine(
                "Graph doesn't contain cycle");
    }
}

// This code is contributed
// by Arnab Kundu

```

输出：

```
Graph contains cycle
```

**相关文章**：
[联合查找算法| 集合 1（无向图中的检测周期）](https://www.geeksforgeeks.org/union-find/)
[脱节集数据结构（Java 实现）](https://www.geeksforgeeks.org/disjoint-set-data-structures-java-implementation/)
[贪婪算法| 第 2 组（Kruskal 的最小生成树算法）](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)，
[作业排序问题| 组 2（使用不交集）](https://www.geeksforgeeks.org/job-sequencing-using-disjoint-set-union/)

**参考**：
[http://en.wikipedia.org/wiki/Disjoint-set_data_structure](http://en.wikipedia.org/wiki/Disjoint-set_data_structure)
[IITD 视频讲座](http://www.youtube.com/watch?v=kajZRdXi6fA)
请写评论 如果发现任何不正确的内容，或者想共享有关上述主题的更多信息。

