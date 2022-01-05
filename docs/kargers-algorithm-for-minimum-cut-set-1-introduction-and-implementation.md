# 最小割集的卡尔格算法|集 1(介绍与实现)

> 原文:[https://www . geeksforgeeks . org/kar gers-算法求最小割集-1-介绍-实现/](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)

给定一个无向图和未加权图，找到最小割(将图分成两部分的最小边数)。
输入图形可能有平行边。
例如，考虑以下示例，最小的切口有 2 条边。

![Kargerfirst](img/bb64a670c03f0b38c6cf837cc5547987.png)

一个简单的解决方案使用[基于最大流的](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)T2 s-t 切割算法来寻找最小切割。将每对顶点视为源点和汇点，调用最小 s-t 割算法寻找 s-t 割。返回所有 s-t 切割的最小值。对于一个图，该算法的最佳时间复杂度是 0(T4 5)。[怎么做？总共有可能的 V <sup>2</sup> 对，一对的 s-t 切割算法需要 O(V*E)时间和 E = O(V <sup>2</sup> )。
下面是用于此目的的简单卡尔格算法。下面的卡尔格算法可以在 O(E) = O(V <sup>2</sup> )时间内实现。

```
1)  Initialize contracted graph CG as copy of original graph
2)  While there are more than 2 vertices.
      a) Pick a random edge (u, v) in the contracted graph.
      b) Merge (or contract) u and v into a single vertex (update 
         the contracted graph).
      c) Remove self-loops
3) Return cut represented by two vertices.
```

让我们通过给出的例子来理解上面的算法。
让第一个随机选择的顶点是连接顶点 0 和 1 的**一个**。我们移除这条边并收缩图(合并顶点 0 和 1)。我们得到下面的图表。

![Karger2](img/54e16daac2bd73e9a2a589b49555c826.png)

让下一个随机选取的边为“d”。我们移除这条边，合并顶点(0，1)和 3。

![Karger3](img/23c57a0319e902740a66b54a8eed6d0a.png)

我们需要消除图中的自循环。所以我们去掉边‘c’

![Karger4](img/452e44e3bac2aee39ceeeee07bd0ccac.png)

现在图有两个顶点，所以我们停止。结果图中的边数是由卡尔格算法产生的割。
***卡尔格的算法是一个*** [***蒙特卡罗算法***](http://en.wikipedia.org/wiki/Monte_Carlo_algorithm) ***而由它产生的切割可能不是最小的。*** 例如，下图显示了不同的随机边拾取顺序会产生大小为 3 的最小切割。

![Karger1](img/af87ad77e52cc6578d62038dab20cf19.png)

下面是上述算法的 C++实现。输入图形表示为边的集合，[联合查找数据结构](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)用于跟踪组件。

## C

```
// Karger's algorithm to find Minimum Cut in an
// undirected, unweighted and connected graph.
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// a structure to represent a unweighted edge in graph
struct Edge
{
    int src, dest;
};

// a structure to represent a connected, undirected
// and unweighted graph as a collection of edges.
struct Graph
{
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges.
    // Since the graph is undirected, the edge
    // from src to dest is also edge from dest
    // to src. Both are counted as 1 edge here.
    Edge* edge;
};

// A structure to represent a subset for union-find
struct subset
{
    int parent;
    int rank;
};

// Function prototypes for union-find (These functions are defined
// after kargerMinCut() )
int find(struct subset subsets[], int i);
void Union(struct subset subsets[], int x, int y);

// A very basic implementation of Karger's randomized
// algorithm for finding the minimum cut. Please note
// that Karger's algorithm is a Monte Carlo Randomized algo
// and the cut returned by the algorithm may not be
// minimum always
int kargerMinCut(struct Graph* graph)
{
    // Get data of given graph
    int V = graph->V, E = graph->E;
    Edge *edge = graph->edge;

    // Allocate memory for creating V subsets.
    struct subset *subsets = new subset[V];

    // Create V subsets with single elements
    for (int v = 0; v < V; ++v)
    {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    // Initially there are V vertices in
    // contracted graph
    int vertices = V;

    // Keep contracting vertices until there are
    // 2 vertices.
    while (vertices > 2)
    {
       // Pick a random edge
       int i = rand() % E;

       // Find vertices (or sets) of two corners
       // of current edge
       int subset1 = find(subsets, edge[i].src);
       int subset2 = find(subsets, edge[i].dest);

       // If two corners belong to same subset,
       // then no point considering this edge
       if (subset1 == subset2)
         continue;

       // Else contract the edge (or combine the
       // corners of edge into one vertex)
       else
       {
          printf("Contracting edge %d-%d\n",
                 edge[i].src, edge[i].dest);
          vertices--;
          Union(subsets, subset1, subset2);
       }
    }

    // Now we have two vertices (or subsets) left in
    // the contracted graph, so count the edges between
    // two components and return the count.
    int cutedges = 0;
    for (int i=0; i<E; i++)
    {
        int subset1 = find(subsets, edge[i].src);
        int subset2 = find(subsets, edge[i].dest);
        if (subset1 != subset2)
          cutedges++;
    }

    return cutedges;
}

// A utility function to find set of an element i
// (uses path compression technique)
int find(struct subset subsets[], int i)
{
    // find root and make root as parent of i
    // (path compression)
    if (subsets[i].parent != i)
      subsets[i].parent =
             find(subsets, subsets[i].parent);

    return subsets[i].parent;
}

// A function that does union of two sets of x and y
// (uses union by rank)
void Union(struct subset subsets[], int x, int y)
{
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    // Attach smaller rank tree under root of high
    // rank tree (Union by Rank)
    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;

    // If ranks are same, then make one as root and
    // increment its rank by one
    else
    {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Creates a graph with V vertices and E edges
struct Graph* createGraph(int V, int E)
{
    Graph* graph = new Graph;
    graph->V = V;
    graph->E = E;
    graph->edge = new Edge[E];
    return graph;
}

// Driver program to test above functions
int main()
{
    /* Let us create following unweighted graph
        0------1
        | \    |
        |   \  |
        |     \|
        2------3   */
    int V = 4;  // Number of vertices in graph
    int E = 5;  // Number of edges in graph
    struct Graph* graph = createGraph(V, E);

    // add edge 0-1
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;

    // add edge 0-2
    graph->edge[1].src = 0;
    graph->edge[1].dest = 2;

    // add edge 0-3
    graph->edge[2].src = 0;
    graph->edge[2].dest = 3;

    // add edge 1-3
    graph->edge[3].src = 1;
    graph->edge[3].dest = 3;

    // add edge 2-3
    graph->edge[4].src = 2;
    graph->edge[4].dest = 3;

    // Use a different seed value for every run.
    srand(time(NULL));

    printf("\nCut found by Karger's randomized algo is %d\n",
           kargerMinCut(graph));

    return 0;
}
```

输出:

```
Contracting edge 0-2
Contracting edge 0-3

Cut found by Karger's randomized algo is 2
```

***注意，上面的程序是基于一个随机函数的结果，可能会产生不同的输出。***
在这篇文章中，我们讨论了简单的卡尔格算法，并发现该算法并不总是产生最小割。上述算法产生的最小割概率大于或等于 1/(n <sup>2</sup> )。参见[下一篇文章《卡尔格算法的分析和应用》](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-2-analysis-and-applications/)，讨论了应用、该概率的证明和改进。
**参考文献:**
[http://en.wikipedia.org/wiki/Karger%27s_algorithm](http://en.wikipedia.org/wiki/Karger%27s_algorithm)
[https://www.youtube.com/watch?v=P0l8jMDQTEQ](https://www.youtube.com/watch?v=P0l8jMDQTEQ)
[https://www . cs . Princeton . edu/courses/archive/fall 13/cos 521/lecnotes/LEC 2 final . pdf](https://www.cs.princeton.edu/courses/archive/fall13/cos521/lecnotes/lec2final.pdf)
[http://web . Stanford . edu/class/archive/cs/cs161 . 1138/讲座/11/Small11.pdf](http://web.stanford.edu/class/archive/cs/cs161/cs161.1138/lectures/11/Small11.pdf)