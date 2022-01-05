# 无向图所有连通分支中最小元素的和

> 原文:[https://www . geesforgeks . org/无向图的所有连通分量中的最小元素之和/](https://www.geeksforgeeks.org/sum-of-the-minimum-elements-in-all-connected-components-of-an-undirected-graph/)

给定一个由 N 个数字组成的数组，其中 A <sub>i</sub> 代表第(i+1) <sup>个</sup>节点的值。还给出了 M 对边，其中 u 和 v 表示由一条边连接的节点。任务是求给定无向图的所有连通分支中最小元素的和。如果一个节点没有与任何其他节点的连接，则将其视为具有一个节点的组件。

**示例:**

> **输入:** a[] = {1，6，2，7，3，8，4，9，5，10 } m = 5
> 1 2
> 3 4
> 5 6
> 7 8
> 9 10
> 
> **输出:** 15
> 连接的元件有:1–2、3–4、5–6、7–8 和 9–10
> 所有元件的最小值之和:1 + 2 + 3 + 4 + 5 = 15
> 
> **输入:** a[] = {2，5，3，4，8 } m = 2
> 1 4
> 4 5
> T5】输出:10
> T8】

**方法:**寻找无向图的连通分支是一个更容易的任务。从每个未访问的顶点开始做一个 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 或者 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 会给我们连接的组件。创建一个**访问过的[]** 阵列，该阵列最初将所有节点标记为假。迭代所有节点，如果该节点未被访问，调用 **DFS()** 函数，使所有直接或间接连接到该节点的节点都被标记为已访问。在访问所有直接或间接连接的节点时，存储所有节点的最小值。创建一个变量 **sum** ，它存储所有这些连接组件的最小值之和。一旦访问了所有节点，*求和*就有了问题的答案。

下面是上述方法的实现:

```
// C++ program to find the sum
// of the minimum elements in all
// connected components of an undirected graph
#include <bits/stdc++.h>
using namespace std;
const int N = 10000;
vector<int> graph[N];

// Initially all nodes
// marked as unvisited
bool visited[N];

// DFS function that visits all
// connected nodes from a given node
void dfs(int node, int a[], int mini)
{
    // Stores the minimum
    mini = min(mini, a[node]);

    // Marks node as visited
    visited[node] = true;

    // Traversed in all the connected nodes
    for (int i : graph[node]) {
        if (!visited[i])
            dfs(i, a, mini);
    }
}

// Function to add the edges
void addedge(int u, int v)
{
    graph[u - 1].push_back(v - 1);
    graph[v - 1].push_back(u - 1);
}

// Function that returns the sum of all minimums
// of connected componenets of graph
int minimumSumConnectedComponents(int a[], int n)
{
    // Initially sum is 0
    int sum = 0;

    // Traverse for all nodes
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            int mini = a[i];
            dfs(i, a, mini);
            sum += mini;
        }
    }

    // Returns the answer
    return sum;
}

// Driver Code
int main()
{
    int a[] = {1, 6, 2, 7, 3, 8, 4, 9, 5, 10};

    // Add edges
    addedge(1, 2);
    addedge(3, 4);
    addedge(5, 6);
    addedge(7, 8);
    addedge(9, 10);

    int n = sizeof(a) / sizeof(a[0]);

    // Calling Function
    cout << minimumSumConnectedComponents(a, n);
    return 0;
}
```

**Output:**

```
15

```