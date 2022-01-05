# 从源到目的地的最短路径，使得沿路径的边权重交替增加和减少

> 原文:[https://www . geeksforgeeks . org/从源到目的地的最短路径，使得沿路径的边权重交替增加和减少/](https://www.geeksforgeeks.org/shortest-path-from-source-to-destination-such-that-edge-weights-along-path-are-alternatively-increasing-and-decreasing/)

给定一个有 **N** 个顶点和 **M** 条边的连通图。任务是找到从源顶点到目的顶点的最短路径，以便最短路径中相邻边权重之间的差异从正变为负，反之亦然(权重(E1) >权重(E2) <权重(E3) …)。).如果不存在这样的路径，则打印 **-1** 。

**示例:**

> **输入:**源= 4，目的地= 3
> ![](img/8259bc2eade831ee25298e4ac6be135e.png)
> **输出:**19
> 4–2–1–3(边权重:8，3，10)和 4–1–2–3(边权重:6，3，10)是唯一有效的路径。
> 第二条路径花费最小，即 19。
> 
> **输入:**源= 2，目的地= 4
> ![](img/53d03e0cc89167dfe7027d37c075c629.png)
> **输出:** -1
> 不存在这样的路径。

**方法:**这里，我们需要保留两个相邻列表的副本，一个用于正差，另一个用于负差。像在[迪克斯特拉算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)中一样取一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，一次保留四个变量，即，

1.  **成本:**存储路径到当前节点的成本。
2.  **阶段:**一个整数变量，告诉接下来需要取什么元素，如果前一个值是负值，那么需要取正值，否则取负值。
3.  **权重:**上次访问节点的权重。
4.  **顶点:**上次访问的顶点。

对于每个顶点，根据所需条件(阶段值)推相邻顶点。请参阅代码以获得更好的理解。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// To store the graph
vector<pair<int, int> > incr[N], decr[N];
int _incr[N], _decr[N], shortest[N];

int n, m, src, dest, MAXI = 1LL << 30;

// Function to add edges
void Add_edge(int x, int y, int w)
{
    incr[x].push_back({ w, y });
    incr[y].push_back({ w, x });
    decr[x].push_back({ -w, y });
    decr[y].push_back({ -w, x });
}

// Function to find the shortest distance from
// source to destination
int Modified_Dijkstra()
{

    // Total cost, stage, weight of previous, vertex
    priority_queue<pair<pair<int, int>, pair<int, int> > > q;

    // Sort the edges
    for (int i = 1; i <= n; i++) {
        sort(incr[i].begin(), incr[i].end());
        sort(decr[i].begin(), decr[i].end());
    }

    for (int i = 1; i <= n; i++)
        shortest[i] = MAXI;

    // Push the source vertex
    q.push({ { 0, 0 }, { 0, src } });

    while (!q.empty()) {

        // Take the top element in the queue
        pair<pair<int, int>, pair<int, int> > FRONT = q.top();

        // Remove it from the queue
        q.pop();

        // Store all the values
        int cost = -FRONT.first.first;
        int stage = FRONT.first.second;
        int weight = FRONT.second.first;
        int v = FRONT.second.second;

        // Take the minimum cost for the vertex
        shortest[v] = min(shortest[v], cost);

        // If destination vertex has already been visited
        if (shortest[dest] != MAXI)
            break;

        // To make difference negative
        if (stage) {

            // Start from last not visited vertex
            for (int i = _incr[v]; i < incr[v].size(); i++) {

                // If we can take the ith vertex
                if (weight > incr[v][i].first)
                    q.push({ { -(cost + incr[v][i].first), 0 },
                             { incr[v][i].first, incr[v][i].second } });
                else {

                    // To keep the last not visited vertex
                    _incr[v] = i;
                    break;
                }
            }
        }

        // To make difference positive
        else {

            // Start from last not visited vertex
            for (int i = _decr[v]; i < decr[v].size(); i++) {

                // If we can take the ith vertex
                if (weight < -decr[v][i].first)
                    q.push({ { -(cost - decr[v][i].first), 1 },
                             { -decr[v][i].first, decr[v][i].second } });
                else {

                    // To keep the last not visited vertex
                    _decr[v] = i;
                    break;
                }
            }
        }
    }

    if (shortest[dest] == MAXI)
        return -1;

    return shortest[dest];
}

// Driver code
int main()
{
    n = 5, src = 4, dest = 3;

    // Adding edges
    Add_edge(4, 2, 8);
    Add_edge(1, 4, 6);
    Add_edge(2, 3, 10);
    Add_edge(3, 1, 10);
    Add_edge(1, 2, 3);
    Add_edge(3, 5, 3);

    cout << Modified_Dijkstra();

    return 0;
}
```

**Output:**

```
19

```