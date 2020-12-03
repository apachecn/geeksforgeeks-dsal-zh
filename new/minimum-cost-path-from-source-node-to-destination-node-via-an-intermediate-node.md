# 通过中间节点从源节点到目标节点的最小成本路径

> 原文： [https://www.geeksforgeeks.org/minimum-cost-path-from-source-node-to-destination-node-via-an-intermediate-node/](https://www.geeksforgeeks.org/minimum-cost-path-from-source-node-to-destination-node-via-an-intermediate-node/)

给定无向加权图。 任务是找到通过中间节点从源节点到目标节点的路径的最小开销。

**注意**：如果一条边走了两次，则仅计算一次重量即可。

![](img/8c09c9360b881a5422eb2a7c5c7081ce.png)

例子：

> **输入**：源= 0，目标= 2，中间= 3；
> **输出**：6
> 最小成本路径 0- > 1- > 3- > 1- > 2
> 边（1-3） 在路径中出现两次，但其权重为
> 仅添加一次。
> 
> **输入**：源= 0，目标= 2，中间= 1；
> **输出**：3
> 最小成本路径为 0- > 1 > 2

**方法**：假设采用从源到中间的路径 P1，以及从中间到目标的路径 P2。 这两个路径之间可能存在一些共同的边。 因此，最佳路径将始终具有以下形式：对于任何节点 U，步行都包括从源到 U，从中间到 U，从目的地到 U 的最短路径上的边。因此，如果 dist（a，b ）是节点 a 和节点 b 之间的最短路径的成本，所需的最小成本路径为 ***min {dist（Source，U）+ dist（intermediate，U）+ dist（destination，U）} [ 所有 U 的 HTG4]*** 。通过对这 3 个节点执行 [Dijkstra 最短路径算法](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)，可以找到所有节点距源，中间和目标的最小距离。

下面是上述方法的实现。

```

// CPP program to find minimum distance between 
// source and destination node and visiting 
// of intermediate node is compulsory 
#include <bits/stdc++.h> 
using namespace std; 
#define MAXN 100005 

// to strore maped values of graph 
vector<pair<int, int> > v[MAXN]; 

// to store distance of 
// all nodes from the source node 
int dist[MAXN]; 

// Dijkstra's algorithm to find 
// shortest path from source to node 
void dijkstra(int source, int n) 
{ 
    // set all the vertices 
    // distances as infinity 
    for (int i = 0; i < n; i++) 
        dist[i] = INT_MAX; 

    // set all vertex as unvisited 
    bool vis[n]; 
    memset(vis, false, sizeof vis); 

    // make distance from source 
    // vertex to source vertex is zero 
    dist = 0; 

    // // multiset do the job 
    // as a min-priority queue 
    multiset<pair<int, int> > s; 

    // insert the source node with distance = 0 
    s.insert({ 0, source }); 

    while (!s.empty()) { 
        pair<int, int> p = *s.begin(); 
        // pop the vertex with the minimum distance 
        s.erase(s.begin()); 

        int x = p.second; 
        int wei = p.first; 

        // check if the popped vertex 
        // is visited before 
        if (vis[x]) 
            continue; 

        vis[x] = true; 

        for (int i = 0; i < v[x].size(); i++) { 
            int e = v[x][i].first; 
            int w = v[x][i].second; 

            // check if the next vertex 
            // distance could be minimized 
            if (dist[x] + w < dist[e]) { 

                dist[e] = dist[x] + w; 

                // insert the next vertex 
                // with the updated distance 
                s.insert({ dist[e], e }); 
            } 
        } 
    } 
} 

// function to add edges in graph 
void add_edge(int s, int t, int weight) 
{ 
    v[s].push_back({ t, weight }); 
    v[t].push_back({ s, weight }); 
} 

// function to find the minimum shortest path 
int solve(int source, int destination,  
               int intermediate, int n) 
{ 
    int ans = INT_MAX; 

    dijkstra(source, n); 

    // store distance from source to 
    // all other vertices 
    int dsource[n]; 
    for (int i = 0; i < n; i++) 
        dsource[i] = dist[i]; 

    dijkstra(destination, n); 
    // store distance from destination 
    // to all other vertices 
    int ddestination[n]; 
    for (int i = 0; i < n; i++) 
        ddestination[i] = dist[i]; 

    dijkstra(intermediate, n); 
    // store distance from intermediate 
    // to all other vertices 
    int dintermediate[n]; 
    for (int i = 0; i < n; i++) 
        dintermediate[i] = dist[i]; 

    // find required answer 
    for (int i = 0; i < n; i++) 
        ans = min(ans, dsource[i] + ddestination[i] 
                                  + dintermediate[i]); 

    return ans; 
} 

// Driver code 
int main() 
{ 

    int n = 4; 
    int source = 0, destination = 2, intermediate = 3; 

    // add edges in graph 
    add_edge(0, 1, 1); 
    add_edge(1, 2, 2); 
    add_edge(1, 3, 3); 

    // function call for minimum shortest path 
    cout << solve(source, destination, intermediate, n); 

    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度**：O（（N + M）* logN），其中 N 是节点数，M 是边数。
**辅助空间**：O（N + M）

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。