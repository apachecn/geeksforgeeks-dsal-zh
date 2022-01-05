# 给定图形中从节点 1 到 N 的第 1 到第 k 条最短路径长度

> 原文:[https://www . geesforgeks . org/1st-to-kth-最短路径长度-给定图中从节点 1 到 n 的距离/](https://www.geeksforgeeks.org/1st-to-kth-shortest-path-lengths-from-node-1-to-n-in-given-graph/)

给定 **N** 节点和 **M** 边的有向加权[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，任务是找到从节点 **1** 到 **N** 的**第 1 到 K <sup>第</sup>** **最短路径**长度。

**示例:**

> **输入:** N = 4，M = 6，K = 3，边= {{1，2，1}，{1，3，3}，{2，3，2}，{2，4，6}，{3，2，8}，{3，4，1 } }
> T3】输出:4 4 7
> T6】解释:从 1 到 N 最短路径长度为 4，第二最短长度也为 4，第三最短长度为 7。
> 
> **输入:** N = 3，M = 3，K = 2，边= {{1，2，2}，{2，3，2}，{1，3，1}}
> 输出: 1 4

**方法:**思路是使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 遍历[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)的所有顶点，使用[优先级队列](https://www.geeksforgeeks.org/min-heap-in-java/)存储尚未最终确定最短距离的顶点，同时得到**最小**距离顶点。按照以下步骤进行操作。

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如说 **pq** 大小 **N** 来存储顶点数和距离值。
*   初始化一个 2d[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说， **dis** 的大小 **N*K** 并用一个非常大的数字初始化所有的值，比如说，1e9。
*   将 **dis[1][0]** 设置为**零，**源顶点的距离值。
*   当 **pq** 不为空时迭代。
    *   弹出 **pq、**的值，将顶点值存储在变量 **u** 中，将顶点距离存储在变量**d**中
    *   如果 **d** 大于距离 **u** ，则**继续。**
    *   对于每一个相邻的 **u** 的顶点 **v** ，检查 **Kth** 距离值是否大于 **u-v** 加上 **u、**的距离值，然后更新 **Kth** 距离值 **v** 和[排序](https://www.geeksforgeeks.org/sort-c-stl/)顶点 **k** 距离**v**

下面是上述方法的实现:

## C++14

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find K shortest path lengths
void findKShortest(int edges[][3], int n, int m, int k)
{

    // Initialize graph
    vector<vector<pair<int, int> > > g(n + 1);
    for (int i = 0; i < m; i++) {
        // Storing edges
        g[edges[i][0]].push_back({ edges[i][1], edges[i][2] });
    }

    // Vector to store distances
    vector<vector<int> > dis(n + 1, vector<int>(k, 1e9));

    // Initialization of priority queue
    priority_queue<pair<int, int>,
                   vector<pair<int, int> >,
                   greater<pair<int, int> > >
        pq;
    pq.push({ 0, 1 });
    dis[1][0] = 0;

    // while pq has elements
    while (!pq.empty()) {
        // Storing the node value
        int u = pq.top().second;

        // Storing the distance value
        int d = (pq.top().first);
        pq.pop();
        if (dis[u][k - 1] < d)
            continue;
        vector<pair<int, int> > v = g[u];

        // Traversing the adjacency list
        for (int i = 0; i < v.size(); i++) {
            int dest = v[i].first;
            int cost = v[i].second;

            // Checking for the cost
            if (d + cost < dis[dest][k - 1]) {
                dis[dest][k - 1] = d + cost;

                // Sorting the distances
                sort(dis[dest].begin(), dis[dest].end());

                // Pushing elements to priority queue
                pq.push({ (d + cost), dest });
            }
        }
    }

    // Printing K shortest paths
    for (int i = 0; i < k; i++) {
        cout << dis[n][i] << " ";
    }
}

// Driver Code
int main()
{

    // Given Input
    int N = 4, M = 6, K = 3;
    int edges[][3] = { { 1, 2, 1 }, { 1, 3, 3 },
                       { 2, 3, 2 }, { 2, 4, 6 },
                       { 3, 2, 8 }, { 3, 4, 1 } };

    // Function Call
    findKShortest(edges, N, M, K);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find K shortest path lengths
function findKShortest(edges, n, m, k)
{

    // Initialize graph
    var g = Array.from(Array(n + 1), ()=>new Array());
    for (var i = 0; i < m; i++)
    {

        // Storing edges
        g[edges[i][0]].push([edges[i][1], edges[i][2]]);
    }

    // Vector to store distances
    var dis = Array.from(Array(n+1), ()=> Array(k).fill(1000000000));

    // Initialization of priority queue
    var pq = [];
    pq.push([0, 1]);
    dis[1][0] = 0;

    // while pq has elements
    while (pq.length != 0)
    {

        // Storing the node value
        var u = pq[pq.length-1][1];

        // Storing the distance value
        var d = (pq[pq.length-1][0]);
        pq.pop();
        if (dis[u][k - 1] < d)
            continue;
        var v = g[u];

        // Traversing the adjacency list
        for (var i = 0; i < v.length; i++) {
            var dest = v[i][0];
            var cost = v[i][1];

            // Checking for the cost
            if (d + cost < dis[dest][k - 1]) {
                dis[dest][k - 1] = d + cost;

                // Sorting the distances
                dis[dest].sort((a,b)=>a-b);

                // Pushing elements to priority queue
                pq.push([(d + cost), dest ]);
                pq.sort();
            }
        }
    }

    // Printing K shortest paths
    for (var i = 0; i < k; i++) {
        document.write(dis[n][i] + " ");
    }
}

// Driver Code

// Given Input
var N = 4, M = 6, K = 3;
var edges = [ [ 1, 2, 1 ], [ 1, 3, 3 ],
                   [ 2, 3, 2 ], [ 2, 4, 6 ],
                   [ 3, 2, 8 ], [ 3, 4, 1 ] ];

// Function Call
findKShortest(edges, N, M, K);

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
4 4 7 
```

***时间复杂度:**O((N+M)* KlogK)*
***辅助空间:** O(NK)*