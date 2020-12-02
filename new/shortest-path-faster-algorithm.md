# 最短路径更快算法

> 原文： [https://www.geeksforgeeks.org/shortest-path-faster-algorithm/](https://www.geeksforgeeks.org/shortest-path-faster-algorithm/)

**先决条件**：[Bellman-Ford 算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

给定具有`V`顶点的**有向加权图**，`E`边和源顶点`S`。 任务是找到给定图中从源顶点到所有其他顶点的最短路径。

**示例**：

> **输入**：V = 5，S = 1，arr = {{1,2,1}，{2，3，7}，{2，4，-2}，{1，3，8 }，{1，4，9}，{3，4，3}，{2，5，3}，{4，5，-3}}
> **输出**：
> 1 ，0
> 2，1
> 3，8
> 4，-1
> 5，-4
> **说明**：对于给定的输入，从 1 到 1 的最短路径 1 是 0，1 到 2 是 1，依此类推。
> 
> **输入**：V = 5，S = 1，arr = {{1，2，-1}，{1，3，4}，{2，3，3}，{2，4，2 }，{2，5，2}，{4，3，5}，{4，2，1}，{5，4，3}}
> **输出**：
> 1 0
> 2，-1
> 3，2
> 4，1
> 5，1

**方法**：最短路径更快算法基于 [Bellman-Ford](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/) 算法，其中每个顶点均用于松弛其相邻顶点，但在 SPF 算法中，将保​​留顶点队列并保留一个顶点 仅在该顶点松弛时才将其添加到队列中。 重复此过程，直到没有更多的顶点可以放宽为止。
可以执行以下步骤来计算结果：

1.  创建一个数组 **d []** ，以存储所有顶点到源顶点的最短距离。 除了 d [S] = 0（其中`S`是源顶点）外，通过无穷大初始化此数组。
2.  创建一个[队列](http://www.geeksforgeeks.org/queue-data-structure/)`Q`，并在其中推送起始源顶点。
    *   当队列不为空时，对图形中的每个边（u，v）执行以下操作
        *   如果 d [v]> d [u] +边的权重（u，v）
        *   d [v] = d [u] +边的权重（u，v）
        *   如果顶点 v 在队列中不存在，则将顶点 v 推入队列。

**注意**：术语**松弛**表示，如果可以通过包含通过顶点**的路径来改善与顶点`v`相关的所有顶点的成本， v** 。 从最短路径的估计值与不是为压缩而设计的螺旋拉伸弹簧的长度之间的类比可以更好地理解这一点。 最初，最短路径的成本被高估了，就像延伸的弹簧一样。 当找到更短的路径时，估计的成本会降低，弹簧会放松。 最终，找到了最短的路径（如果存在的话），并且弹簧已经松弛到其静止长度。

下面是上述方法的实现：

## C ++

```

// C++ implementation of SPFA 

#include <bits/stdc++.h> 
using namespace std; 

// Graph is stored as vector of vector of pairs 
// first element of pair store vertex 
// second element of pair store weight 
vector<pair<int, int> > graph[100000]; 

// Function to add edges in the graph 
// connecting a pair of vertex(frm) and weight 
// to another vertex(to) in graph 
void addEdge(int frm, int to, int weight) 
{ 

    graph[frm].push_back({ to, weight }); 
} 

// Function to print shortest distance from source 
void print_distance(int d[], int V) 
{ 
    cout << "Vertex \t\t Distance"
         << " from source" << endl; 

    for (int i = 1; i <= V; i++) { 
        printf("%d \t\t %d\n", i, d[i]); 
    } 
} 

// Function to compute the SPF algorithm 
void shortestPathFaster(int S, int V) 
{ 
    // Create array d to store shortest distance 
    int d[V + 1]; 

    // Boolean array to check if vertex 
    // is present in queue or not 
    bool inQueue[V + 1] = { false }; 

    // Initialize the distance from source to 
    // other vertex as INT_MAX(infinite) 
    for (int i = 0; i <= V; i++) { 
        d[i] = INT_MAX; 
    } 
    d[S] = 0; 

    queue<int> q; 
    q.push(S); 
    inQueue[S] = true; 

    while (!q.empty()) { 

        // Take the front vertex from Queue 
        int u = q.front(); 
        q.pop(); 
        inQueue[u] = false; 

        // Relaxing all the adjacent edges of 
        // vertex taken from the Queue 
        for (int i = 0; i < graph[u].size(); i++) { 

            int v = graph[u][i].first; 
            int weight = graph[u][i].second; 

            if (d[v] > d[u] + weight) { 
                d[v] = d[u] + weight; 

                // Check if vertex v is in Queue or not 
                // if not then push it into the Queue 
                if (!inQueue[v]) { 
                    q.push(v); 
                    inQueue[v] = true; 
                } 
            } 
        } 
    } 

    // Print the result 
    print_distance(d, V); 
} 

// Driver code 
int main() 
{ 
    int V = 5; 
    int S = 1; 

    // Connect vertex a to b with weight w 
    // addEdge(a, b, w) 

    addEdge(1, 2, 1); 
    addEdge(2, 3, 7); 
    addEdge(2, 4, -2); 
    addEdge(1, 3, 8); 
    addEdge(1, 4, 9); 
    addEdge(3, 4, 3); 
    addEdge(2, 5, 3); 
    addEdge(4, 5, -3); 

    // Calling shortestPathFaster function 
    shortestPathFaster(S, V); 

    return 0; 
} 

```