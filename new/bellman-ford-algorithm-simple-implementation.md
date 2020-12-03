# Bellman Ford 算法（简单实现）

> 原文： [https://www.geeksforgeeks.org/bellman-ford-algorithm-simple-implementation/](https://www.geeksforgeeks.org/bellman-ford-algorithm-simple-implementation/)

我们已经介绍了 Bellman Ford，并在此处讨论了实现[。](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

*输入：*图和源顶点 *src*
*输出：*从 *src* 到所有顶点的最短距离。 如果存在负重量循环，则不会计算最短距离，而是报告负重量循环。

**1）**此步骤初始化从源到所有顶点的距离为无穷大，到源自身的距离为 0。创建大小为| V |的数组 dist []。 除了 dist [src]（其中 src 是源顶点）之外的所有值都为无穷大。

**2）**此步骤计算最短距离。 跟随| V | -1 次，其中| V | 是给定图中的顶点数。
….. **a）**对每个边 uv 执行以下操作
………………如果 dist [v] > dist [u] +边 uv 的权重，则更新 dist [v]
…………………….dist [v] = dist [u] +边 uv 的权重

**3）**此步骤报告图表中是否存在负重量循环。 对每个边 uv
执行以下操作…………如果 dist [v] > dist [u] +边 uv 的权重，则“图形包含负权重循环”
步骤 3 的思想是，步骤 2 保证了 如果图形不包含负权重循环，则距离最短。 如果我们再遍历所有边一次，并且获得任意顶点的较短路径，那么负周期就会变负

**示例**
让我们用以下示例图来了解算法。 图像是从来源的[拍摄的。](http://www.cs.arizona.edu/classes/cs445/spring07/ShortestPath2.prn.pdf)

假设给定的源顶点为 0。将所有距离初始化为无限，除了到源本身的距离。 图中的顶点总数为 5，因此*所有边必须处理 4 次。*

![Example Graph](img/566868a605baa6b2dadb4d9184a7c629.png "bellman2")

让所有边按以下顺序处理：（B，E），（D，B），（B，D），（A，B），（A，C），（D，C），（B，C） ，（E，D）。 第一次处理所有边时，我们得到以下距离。 第一行显示初始距离。 第二行显示处理边（B，E），（D，B），（B，D）和（A，B）时的距离。 第三行显示处理（A，C）时的距离。 第四行显示何时处理（D，C），（B，C）和（E，D）。
![](img/27e4581ddb941b8bdb551d8ffb84321e.png "After1stIteration")

第一次迭代保证给出最长为 1 个边长的所有最短路径。 第二次处理所有边时，我们得到以下距离（最后一行显示最终值）。

![](img/c5fc23a47dc1ccc7a2de578ec1d30ee5.png "seconditeration")

第二次迭代保证给出最长为 2 个边长的所有最短路径。 该算法将所有边再处理 2 次。 在第二次迭代后将距离最小化，因此第三次和第四次迭代不会更新距离。

## C++

```cpp

// A C++ program for Bellman-Ford's single source 
// shortest path algorithm. 
#include <bits/stdc++.h> 
using namespace std; 

// The main function that finds shortest 
// distances from src to all other vertices 
// using Bellman-Ford algorithm. The function 
// also detects negative weight cycle 
// The row graph[i] represents i-th edge with 
// three values u, v and w. 
void BellmanFord(int graph[][3], int V, int E, 
                 int src) 
{ 
    // Initialize distance of all vertices as infinite. 
    int dis[V]; 
    for (int i = 0; i < V; i++) 
        dis[i] = INT_MAX; 

    // initialize distance of source as 0 
    dis[src] = 0; 

    // Relax all edges |V| - 1 times. A simple 
    // shortest path from src to any other 
    // vertex can have at-most |V| - 1 edges 
    for (int i = 0; i < V - 1; i++) { 

        for (int j = 0; j < E; j++) { 
            if (dis[graph[j][0]] + graph[j][2] < 
                               dis[graph[j][1]]) 
                dis[graph[j][1]] =  
                  dis[graph[j][0]] + graph[j][2]; 
        } 
    } 

    // check for negative-weight cycles. 
    // The above step guarantees shortest 
    // distances if graph doesn't contain 
    // negative weight cycle.  If we get a 
    // shorter path, then there is a cycle. 
    for (int i = 0; i < E; i++) { 
        int x = graph[i][0]; 
        int y = graph[i][1]; 
        int weight = graph[i][2]; 
        if (dis[x] != INT_MAX && 
                   dis[x] + weight < dis[y]) 
            cout << "Graph contains negative"
                    " weight cycle"
                 << endl; 
    } 

    cout << "Vertex Distance from Source" << endl; 
    for (int i = 0; i < V; i++) 
        cout << i << "\t\t" << dis[i] << endl; 
} 

// Driver program to test above functions 
int main() 
{ 
    int V = 5; // Number of vertices in graph 
    int E = 8; // Number of edges in graph 

    // Every edge has three values (u, v, w) where 
    // the edge is from vertex u to v. And weight 
    // of the edge is w. 
    int graph[][3] = { { 0, 1, -1 }, { 0, 2, 4 }, 
                       { 1, 2, 3 }, { 1, 3, 2 },  
                       { 1, 4, 2 }, { 3, 2, 5 },  
                       { 3, 1, 1 }, { 4, 3, -3 } }; 

    BellmanFord(graph, V, E, 0); 
    return 0; 
} 

```