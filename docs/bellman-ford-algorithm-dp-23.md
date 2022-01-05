# 贝尔曼-福特算法| DP-23

> 原文:[https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

给定一个图和图中的源顶点 *src* ，找到从 *src* 到给定图中所有顶点的最短路径。该图可能包含负权重边。
我们已经讨论了这个问题的[迪克斯特拉算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)。Dijkstra 的算法是一个 Greedy 算法，时间复杂度为 O((V+E)LogV)(使用斐波那契堆)。*迪克斯特拉不适用于负权重*循环*的图表，贝尔曼-福特适用于此类图表。Bellman-Ford 也比 Dijkstra 简单，非常适合分布式系统。但贝尔曼-福特的时间复杂度是 O(VE)，比迪克斯特拉更高。*

**算法**
以下是详细步骤。
*输入:*图形和一个源顶点 *src*
*输出:*从 *src* 到所有顶点的最短距离。如果存在负重量循环，则不计算最短距离，而是报告负重量循环。
**1)** 此步骤将从源到所有顶点的距离初始化为无穷大，到源本身的距离初始化为 0。创建一个大小为|V|的数组 dist[]，除了 dist[src]以外，所有值都为无穷大，其中 src 是源顶点。
**2)** 此步骤计算最短距离。执行以下|V|-1 次，其中|V|是给定图中的顶点数。
….. **a)** 对每个边缘 u-v 执行以下操作
…………如果 dist[v] > dist[u] +边缘 uv 的权重，则更新 dist[v]
……………………。dist[v] = dist[u] +边缘 uv 的权重
**3)** 此步骤报告图形中是否存在负权重循环。对每个边 u-v
……如果 dist[v] > dist[u] +边 uv 的权重，那么“图形包含负权重循环”
步骤 3 的思想是，如果图形不包含负权重循环，步骤 2 保证最短距离。如果我们再迭代一次所有的边，得到任意顶点的更短的路径，那么就有一个负的权重循环
***这是怎么工作的？*** 与其他动态规划问题一样，该算法采用自下而上的方式计算最短路径。它首先计算路径中最多有一条边的最短距离。然后，它计算最多有 2 条边的最短路径，依此类推。在外环的第 I 次迭代之后，计算最多具有 I 条边的最短路径。在任何简单路径中最多可以有| V |–1 条边，这就是为什么外循环运行| V |–1 次。其思想是，假设不存在负权重循环，如果我们已经计算了最多有 I 条边的最短路径，那么对所有边的迭代保证给出最多有(i+1)条边的最短路径(证明很简单，可以参考[这个](http://courses.csail.mit.edu/6.006/spring11/lectures/lec15.pdf)或者[麻省理工视频讲座](http://www.youtube.com/watch?v=Ttezuzs39nk))
T39】示例 T41】让我们用下面的示例图来理解算法。图片来自[这个](http://www.cs.arizona.edu/classes/cs445/spring07/ShortestPath2.prn.pdf)来源。
让给定的源顶点为 0。将所有距离初始化为无穷大，到源本身的距离除外。图中顶点总数为 5，因此*所有边必须处理 4 次。*

![Bellman–Ford Algorithm Example Graph 1](img/566868a605baa6b2dadb4d9184a7c629.png)

让所有边按以下顺序处理:(B，E)，(D，B)，(B，D)，(A，B)，(A，C)，(D，C)，(B，C)，(E，D)。第一次处理所有边时，我们得到以下距离。第一行显示初始距离。第二行显示处理边(B，E)、(D，B)、(B，D)和(A，B)时的距离。第三行显示处理(A，C)时的距离。第四行显示处理(D，C)、(B，C)和(E，D)的时间。

![Bellman–Ford Algorithm Example Graph 2](img/27e4581ddb941b8bdb551d8ffb84321e.png)

第一次迭代保证给出所有最短路径，其长度最多为 1 条边。第二次处理所有边时，我们得到以下距离(最后一行显示最终值)。

![Bellman–Ford Algorithm Example Graph 3](img/c5fc23a47dc1ccc7a2de578ec1d30ee5.png)

第二次迭代保证给出所有最短路径，其长度最多为 2 条边。该算法将所有边再处理 2 次。距离在第二次迭代后被最小化，所以第三次和第四次迭代不会更新距离。
**执行:**

## C++

```
// A C++ program for Bellman-Ford's single source
// shortest path algorithm.
#include <bits/stdc++.h>

// a structure to represent a weighted edge in graph
struct Edge {
    int src, dest, weight;
};

// a structure to represent a connected, directed and
// weighted graph
struct Graph {
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges.
    struct Edge* edge;
};

// Creates a graph with V vertices and E edges
struct Graph* createGraph(int V, int E)
{
    struct Graph* graph = new Graph;
    graph->V = V;
    graph->E = E;
    graph->edge = new Edge[E];
    return graph;
}

// A utility function used to print the solution
void printArr(int dist[], int n)
{
    printf("Vertex   Distance from Source\n");
    for (int i = 0; i < n; ++i)
        printf("%d \t\t %d\n", i, dist[i]);
}

// The main function that finds shortest distances from src
// to all other vertices using Bellman-Ford algorithm.  The
// function also detects negative weight cycle
void BellmanFord(struct Graph* graph, int src)
{
    int V = graph->V;
    int E = graph->E;
    int dist[V];

    // Step 1: Initialize distances from src to all other
    // vertices as INFINITE
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX;
    dist[src] = 0;

    // Step 2: Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other vertex can have
    // at-most |V| - 1 edges
    for (int i = 1; i <= V - 1; i++) {
        for (int j = 0; j < E; j++) {
            int u = graph->edge[j].src;
            int v = graph->edge[j].dest;
            int weight = graph->edge[j].weight;
            if (dist[u] != INT_MAX
                && dist[u] + weight < dist[v])
                dist[v] = dist[u] + weight;
        }
    }

    // Step 3: check for negative-weight cycles.  The above
    // step guarantees shortest distances if graph doesn't
    // contain negative weight cycle.  If we get a shorter
    // path, then there is a cycle.
    for (int i = 0; i < E; i++) {
        int u = graph->edge[i].src;
        int v = graph->edge[i].dest;
        int weight = graph->edge[i].weight;
        if (dist[u] != INT_MAX
            && dist[u] + weight < dist[v]) {
            printf("Graph contains negative weight cycle");
            return; // If negative cycle is detected, simply
                    // return
        }
    }

    printArr(dist, V);

    return;
}

// Driver program to test above functions
int main()
{
    /* Let us create the graph given in above example */
    int V = 5; // Number of vertices in graph
    int E = 8; // Number of edges in graph
    struct Graph* graph = createGraph(V, E);

    // add edge 0-1 (or A-B in above figure)
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;
    graph->edge[0].weight = -1;

    // add edge 0-2 (or A-C in above figure)
    graph->edge[1].src = 0;
    graph->edge[1].dest = 2;
    graph->edge[1].weight = 4;

    // add edge 1-2 (or B-C in above figure)
    graph->edge[2].src = 1;
    graph->edge[2].dest = 2;
    graph->edge[2].weight = 3;

    // add edge 1-3 (or B-D in above figure)
    graph->edge[3].src = 1;
    graph->edge[3].dest = 3;
    graph->edge[3].weight = 2;

    // add edge 1-4 (or B-E in above figure)
    graph->edge[4].src = 1;
    graph->edge[4].dest = 4;
    graph->edge[4].weight = 2;

    // add edge 3-2 (or D-C in above figure)
    graph->edge[5].src = 3;
    graph->edge[5].dest = 2;
    graph->edge[5].weight = 5;

    // add edge 3-1 (or D-B in above figure)
    graph->edge[6].src = 3;
    graph->edge[6].dest = 1;
    graph->edge[6].weight = 1;

    // add edge 4-3 (or E-D in above figure)
    graph->edge[7].src = 4;
    graph->edge[7].dest = 3;
    graph->edge[7].weight = -3;

    BellmanFord(graph, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for Bellman-Ford's single source shortest path
// algorithm.
import java.util.*;
import java.lang.*;
import java.io.*;

// A class to represent a connected, directed and weighted graph
class Graph {
    // A class to represent a weighted edge in graph
    class Edge {
        int src, dest, weight;
        Edge()
        {
            src = dest = weight = 0;
        }
    };

    int V, E;
    Edge edge[];

    // Creates a graph with V vertices and E edges
    Graph(int v, int e)
    {
        V = v;
        E = e;
        edge = new Edge[e];
        for (int i = 0; i < e; ++i)
            edge[i] = new Edge();
    }

    // The main function that finds shortest distances from src
    // to all other vertices using Bellman-Ford algorithm. The
    // function also detects negative weight cycle
    void BellmanFord(Graph graph, int src)
    {
        int V = graph.V, E = graph.E;
        int dist[] = new int[V];

        // Step 1: Initialize distances from src to all other
        // vertices as INFINITE
        for (int i = 0; i < V; ++i)
            dist[i] = Integer.MAX_VALUE;
        dist[src] = 0;

        // Step 2: Relax all edges |V| - 1 times. A simple
        // shortest path from src to any other vertex can
        // have at-most |V| - 1 edges
        for (int i = 1; i < V; ++i) {
            for (int j = 0; j < E; ++j) {
                int u = graph.edge[j].src;
                int v = graph.edge[j].dest;
                int weight = graph.edge[j].weight;
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v])
                    dist[v] = dist[u] + weight;
            }
        }

        // Step 3: check for negative-weight cycles. The above
        // step guarantees shortest distances if graph doesn't
        // contain negative weight cycle. If we get a shorter
        // path, then there is a cycle.
        for (int j = 0; j < E; ++j) {
            int u = graph.edge[j].src;
            int v = graph.edge[j].dest;
            int weight = graph.edge[j].weight;
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                System.out.println("Graph contains negative weight cycle");
                return;
            }
        }
        printArr(dist, V);
    }

    // A utility function used to print the solution
    void printArr(int dist[], int V)
    {
        System.out.println("Vertex Distance from Source");
        for (int i = 0; i < V; ++i)
            System.out.println(i + "\t\t" + dist[i]);
    }

    // Driver method to test above function
    public static void main(String[] args)
    {
        int V = 5; // Number of vertices in graph
        int E = 8; // Number of edges in graph

        Graph graph = new Graph(V, E);

        // add edge 0-1 (or A-B in above figure)
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
        graph.edge[0].weight = -1;

        // add edge 0-2 (or A-C in above figure)
        graph.edge[1].src = 0;
        graph.edge[1].dest = 2;
        graph.edge[1].weight = 4;

        // add edge 1-2 (or B-C in above figure)
        graph.edge[2].src = 1;
        graph.edge[2].dest = 2;
        graph.edge[2].weight = 3;

        // add edge 1-3 (or B-D in above figure)
        graph.edge[3].src = 1;
        graph.edge[3].dest = 3;
        graph.edge[3].weight = 2;

        // add edge 1-4 (or B-E in above figure)
        graph.edge[4].src = 1;
        graph.edge[4].dest = 4;
        graph.edge[4].weight = 2;

        // add edge 3-2 (or D-C in above figure)
        graph.edge[5].src = 3;
        graph.edge[5].dest = 2;
        graph.edge[5].weight = 5;

        // add edge 3-1 (or D-B in above figure)
        graph.edge[6].src = 3;
        graph.edge[6].dest = 1;
        graph.edge[6].weight = 1;

        // add edge 4-3 (or E-D in above figure)
        graph.edge[7].src = 4;
        graph.edge[7].dest = 3;
        graph.edge[7].weight = -3;

        graph.BellmanFord(graph, 0);
    }
}
// Contributed by Aakash Hasija
```

## 蟒蛇 3

```
# Python3 program for Bellman-Ford's single source
# shortest path algorithm.

# Class to represent a graph
class Graph:

    def __init__(self, vertices):
        self.V = vertices # No. of vertices
        self.graph = []

    # function to add an edge to graph
    def addEdge(self, u, v, w):
        self.graph.append([u, v, w])

    # utility function used to print the solution
    def printArr(self, dist):
        print("Vertex Distance from Source")
        for i in range(self.V):
            print("{0}\t\t{1}".format(i, dist[i]))

    # The main function that finds shortest distances from src to
    # all other vertices using Bellman-Ford algorithm. The function
    # also detects negative weight cycle
    def BellmanFord(self, src):

        # Step 1: Initialize distances from src to all other vertices
        # as INFINITE
        dist = [float("Inf")] * self.V
        dist[src] = 0

        # Step 2: Relax all edges |V| - 1 times. A simple shortest
        # path from src to any other vertex can have at-most |V| - 1
        # edges
        for _ in range(self.V - 1):
            # Update dist value and parent index of the adjacent vertices of
            # the picked vertex. Consider only those vertices which are still in
            # queue
            for u, v, w in self.graph:
                if dist[u] != float("Inf") and dist[u] + w < dist[v]:
                        dist[v] = dist[u] + w

        # Step 3: check for negative-weight cycles. The above step
        # guarantees shortest distances if graph doesn't contain
        # negative weight cycle. If we get a shorter path, then there
        # is a cycle.

        for u, v, w in self.graph:
                if dist[u] != float("Inf") and dist[u] + w < dist[v]:
                        print("Graph contains negative weight cycle")
                        return

        # print all distance
        self.printArr(dist)

g = Graph(5)
g.addEdge(0, 1, -1)
g.addEdge(0, 2, 4)
g.addEdge(1, 2, 3)
g.addEdge(1, 3, 2)
g.addEdge(1, 4, 2)
g.addEdge(3, 2, 5)
g.addEdge(3, 1, 1)
g.addEdge(4, 3, -3)

# Print the solution
g.BellmanFord(0)

# Initially, Contributed by Neelam Yadav
# Later On, Edited by Himanshu Garg
```

## C#

```
// A C# program for Bellman-Ford's single source shortest path
// algorithm.

using System;

// A class to represent a connected, directed and weighted graph
class Graph {
    // A class to represent a weighted edge in graph
    class Edge {
        public int src, dest, weight;
        public Edge()
        {
            src = dest = weight = 0;
        }
    };

    int V, E;
    Edge[] edge;

    // Creates a graph with V vertices and E edges
    Graph(int v, int e)
    {
        V = v;
        E = e;
        edge = new Edge[e];
        for (int i = 0; i < e; ++i)
            edge[i] = new Edge();
    }

    // The main function that finds shortest distances from src
    // to all other vertices using Bellman-Ford algorithm. The
    // function also detects negative weight cycle
    void BellmanFord(Graph graph, int src)
    {
        int V = graph.V, E = graph.E;
        int[] dist = new int[V];

        // Step 1: Initialize distances from src to all other
        // vertices as INFINITE
        for (int i = 0; i < V; ++i)
            dist[i] = int.MaxValue;
        dist[src] = 0;

        // Step 2: Relax all edges |V| - 1 times. A simple
        // shortest path from src to any other vertex can
        // have at-most |V| - 1 edges
        for (int i = 1; i < V; ++i) {
            for (int j = 0; j < E; ++j) {
                int u = graph.edge[j].src;
                int v = graph.edge[j].dest;
                int weight = graph.edge[j].weight;
                if (dist[u] != int.MaxValue && dist[u] + weight < dist[v])
                    dist[v] = dist[u] + weight;
            }
        }

        // Step 3: check for negative-weight cycles. The above
        // step guarantees shortest distances if graph doesn't
        // contain negative weight cycle. If we get a shorter
        // path, then there is a cycle.
        for (int j = 0; j < E; ++j) {
            int u = graph.edge[j].src;
            int v = graph.edge[j].dest;
            int weight = graph.edge[j].weight;
            if (dist[u] != int.MaxValue && dist[u] + weight < dist[v]) {
                Console.WriteLine("Graph contains negative weight cycle");
                return;
            }
        }
        printArr(dist, V);
    }

    // A utility function used to print the solution
    void printArr(int[] dist, int V)
    {
        Console.WriteLine("Vertex Distance from Source");
        for (int i = 0; i < V; ++i)
            Console.WriteLine(i + "\t\t" + dist[i]);
    }

    // Driver method to test above function
    public static void Main()
    {
        int V = 5; // Number of vertices in graph
        int E = 8; // Number of edges in graph

        Graph graph = new Graph(V, E);

        // add edge 0-1 (or A-B in above figure)
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
        graph.edge[0].weight = -1;

        // add edge 0-2 (or A-C in above figure)
        graph.edge[1].src = 0;
        graph.edge[1].dest = 2;
        graph.edge[1].weight = 4;

        // add edge 1-2 (or B-C in above figure)
        graph.edge[2].src = 1;
        graph.edge[2].dest = 2;
        graph.edge[2].weight = 3;

        // add edge 1-3 (or B-D in above figure)
        graph.edge[3].src = 1;
        graph.edge[3].dest = 3;
        graph.edge[3].weight = 2;

        // add edge 1-4 (or B-E in above figure)
        graph.edge[4].src = 1;
        graph.edge[4].dest = 4;
        graph.edge[4].weight = 2;

        // add edge 3-2 (or D-C in above figure)
        graph.edge[5].src = 3;
        graph.edge[5].dest = 2;
        graph.edge[5].weight = 5;

        // add edge 3-1 (or D-B in above figure)
        graph.edge[6].src = 3;
        graph.edge[6].dest = 1;
        graph.edge[6].weight = 1;

        // add edge 4-3 (or E-D in above figure)
        graph.edge[7].src = 4;
        graph.edge[7].dest = 3;
        graph.edge[7].weight = -3;

        graph.BellmanFord(graph, 0);
    }
    // This code is contributed by Ryuga
}
```

**输出:**

```
Vertex   Distance from Source
0                0
1                -1
2                2
3                -2
4                1
```

**注释**
**1)** 负权重在图的各种应用中都有。例如，如果我们沿着这条路走，我们可能会获得一些优势，而不是为一条路付出成本。
**2)** Bellman-Ford 对分布式系统的工作效果更好(比 Dijkstra 的好)。与 Dijkstra 的我们需要找到所有顶点的最小值不同，在 Bellman-Ford 中，边被逐个考虑。
**3)** 贝尔曼-福特不适用于具有负边的无向图，因为它将被声明为负循环。
**练习**
**1)** 标准的贝尔曼-福特算法只有在没有负权重循环的情况下才会报告最短路径。修改它，使它报告最小距离，即使有一个负的重量周期。
**2)** 我们能不能用 Dijkstra 算法求负权重图的最短路径——一个思路可以是，计算最小权重值，给所有权重加一个正值(等于最小权重值的绝对值)，对修改后的图运行 Dijkstra 算法。这个算法行得通吗？
[**贝尔曼·福特算法(简单实现)**](https://www.geeksforgeeks.org/bellman-ford-algorithm-simple-implementation/)
**参考文献:**
[http://www.youtube.com/watch?v=Ttezuzs39nk](http://www.youtube.com/watch?v=Ttezuzs39nk)
T32】http://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm
T35】http://www . cs . Arizona . edu/class/cs 445/spring 07/shortestpath 2 . prn . pdf
如有不正确之处，或想分享以上讨论话题的更多信息，请写评论