# Bellman-Ford 算法| DP-23

> 原文： [https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

给定一个图和图中的源顶点 *src* ，找到从 *src* 到给定图中所有顶点的最短路径。 该图可能包含负权重边。

我们已经讨论了 [Dijkstra 算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)。 Dijkstra 算法是贪婪算法，时间复杂度为 O（VLogV）（使用斐波那契堆）。 *Dijkstra 不适用于负负边的图表，Bellman-Ford 可以处理此类图表。 Bellman-Ford 也比 Dijkstra 简单，并且非常适合分布式系统。 但是 Bellman-Ford 的时间复杂度是 O（VE），比 Dijkstra 大。*

**算法**

以下是详细步骤。

*输入：*图和源顶点 *src*

*输出：*从 *src* 到所有顶点的最短距离。 如果存在负重量循环，则不会计算最短距离，而是报告负重量循环。

**1）**此步骤初始化从源到所有顶点的距离为无穷大，到源本身的距离为 0。创建大小为| V |的数组 dist []。 除了 dist [src]（其中 src 是源顶点）之外的所有值都为无穷大。

**2）**此步骤计算最短距离。 跟随| V | -1 次，其中| V | 是给定图中的顶点数。

….. **a）**对每个边 uv 执行以下操作

………………如果 dist [v] > dist [u] +边 uv 的权重，则更新 dist [v]

…………………….dist [v] = dist [u] +边 uv 的权重

**3）**此步骤报告图表中是否存在负重量循环。 对每个边 uv

执行以下操作…………如果 dist [v] > dist [u] +边 uv 的权重，则“图形包含负权重循环”

步骤 3 的思想是，步骤 2 保证了 如果图形不包含负权重周期，则表示最短距离。 如果我们再遍历所有边一次，并且获得任意顶点的较短路径，那么负周期就会变负

***如何运作？*** 与其他动态规划问题一样，该算法以自下而上的方式计算最短路径。 它首先计算路径中最多具有一个边的最短距离。 然后，它计算最多具有 2 条边的最短路径，依此类推。 在外循环的第 i 次迭代之后，将计算最多 i 个边的最短路径。 可以有最大| V |。 –在任何简单路径中都有 1 条边，这就是为什么外循环运行| v |的原因 – 1 次。 这个想法是，假设不存在负权重周期，如果我们计算出最多具有 i 个边的最短路径，那么对所有边进行的迭代保证给出最多具有（i + 1）个边的最短路径（证明很简单 ，您可以参考[此](http://courses.csail.mit.edu/6.006/spring11/lectures/lec15.pdf)或 [MIT 视频讲座](http://www.youtube.com/watch?v=Ttezuzs39nk)）

**示例**

让我们用以下示例图来了解算法。 图像是从来源的[拍摄的。](http://www.cs.arizona.edu/classes/cs445/spring07/ShortestPath2.prn.pdf)

假设给定的源顶点为 0。将所有距离初始化为无限，除了到源本身的距离。 图中的顶点总数为 5，因此*所有边必须处理 4 次。*

![Example Graph](img/566868a605baa6b2dadb4d9184a7c629.png "bellman2")

让所有边按以下顺序处理：（B，E），（D，B），（B，D），（A，B），（A，C），（D，C），（B，C ），（E，D）。 第一次处理所有边时，我们得到以下距离。 第一行显示初始距离。 第二行显示处理边（B，E），（D，B），（B，D）和（A，B）时的距离。 第三行显示处理（A，C）时的距离。 第四行显示何时处理（D，C），（B，C）和（E，D）。

![](img/27e4581ddb941b8bdb551d8ffb84321e.png "After1stIteration")

第一次迭代保证给出最长为 1 个边长的所有最短路径。 第二次处理所有边时，我们得到以下距离（最后一行显示最终值）。

![](img/c5fc23a47dc1ccc7a2de578ec1d30ee5.png "seconditeration")

第二次迭代保证给出最长为 2 个边长的所有最短路径。 该算法将所有边再处理 2 次。 在第二次迭代后将距离最小化，因此第三次和第四次迭代不会更新距离。

**实施**：

## C++

```cpp

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

// The main function that finds shortest distances from src to 
// all other vertices using Bellman-Ford algorithm.  The function 
// also detects negative weight cycle 
void BellmanFord(struct Graph* graph, int src) 
{ 
    int V = graph->V; 
    int E = graph->E; 
    int dist[V]; 

    // Step 1: Initialize distances from src to all other vertices 
    // as INFINITE 
    for (int i = 0; i < V; i++) 
        dist[i] = INT_MAX; 
    dist[src] = 0; 

    // Step 2: Relax all edges |V| - 1 times. A simple shortest 
    // path from src to any other vertex can have at-most |V| - 1 
    // edges 
    for (int i = 1; i <= V - 1; i++) { 
        for (int j = 0; j < E; j++) { 
            int u = graph->edge[j].src; 
            int v = graph->edge[j].dest; 
            int weight = graph->edge[j].weight; 
            if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) 
                dist[v] = dist[u] + weight; 
        } 
    } 

    // Step 3: check for negative-weight cycles.  The above step 
    // guarantees shortest distances if graph doesn't contain 
    // negative weight cycle.  If we get a shorter path, then there 
    // is a cycle. 
    for (int i = 0; i < E; i++) { 
        int u = graph->edge[i].src; 
        int v = graph->edge[i].dest; 
        int weight = graph->edge[i].weight; 
        if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) { 
            printf("Graph contains negative weight cycle"); 
            return; // If negative cycle is detected, simply return 
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

    // add edge 1-4 (or A-E in above figure) 
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