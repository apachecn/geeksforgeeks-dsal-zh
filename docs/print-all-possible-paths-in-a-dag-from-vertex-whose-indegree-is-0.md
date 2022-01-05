# 打印从索引为 0 的顶点开始的 DAG 中所有可能的路径

> 原文:[https://www . geesforgeks . org/print-所有可能的路径-从顶点开始-其索引为-0/](https://www.geeksforgeeks.org/print-all-possible-paths-in-a-dag-from-vertex-whose-indegree-is-0/)

给定一个有向无环图(DAG)，它有 **N** 个顶点和 **M** 条边，任务是打印从内角为零的顶点开始的所有路径。

> 顶点的度数是一个顶点的引入边的总数。

**示例:**

> **输入:** N = 6，边[] = {{5，0}，{5，2}，{4，0}，{4，1}，{2，3}，{3，1}}
> **输出:**所有可能的路径:
> 4 0
> 4 1
> 5 0
> 5 2 3 1
> **解释:**
> 给定的图形可以表示为:
> 
> ![](img/7d0dd3600bc879e60d2864710a2aab68.png)
> 
> 有两个顶点的度数为零，即顶点 5 和 4，在探索这些顶点后，我们得到了以下路径:
> 4->0
> 4->1
> 5->0
> 5->2->3->1
> 
> **输入:** N = 6，边[] = {{0，5}}
> **输出:**所有可能路径:
> 0 5
> **说明:**
> 图中只会有一条可能路径。

**进场:**

1.  创建一个布尔数组 **indeg0** ，该数组为所有索引为零的顶点存储一个真值。
2.  将[离散傅立叶变换](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)应用于所有指数为 0 的顶点。
3.  打印从索引为 0 的顶点到超出度为零的顶点的所有路径。

> **图解:**
> 对于上图:
> indeg0[] = {False，False，False，False，True，True}
> 由于 indeg[4] = True，因此在顶点 4 上应用 DFS 并打印终止于 0 度外顶点的所有路径如下:
> T6】4->0
> T9】4->1
> 同样 indeg[5] = True，因此在顶点 5 上应用 DFS 并打印终止于的所有路径

下面是上述方法的实现:

## C++

```
// C++ program to print
// all possible paths in a DAG

#include <bits/stdc++.h>
using namespace std;

vector<int> path;

vector<bool> indeg0, outdeg0;

vector<vector<int> > adj;

vector<bool> visited;

// Recursive function to print all paths
void dfs(int s)
{
    // Append the node in path
    // and set visited
    path.push_back(s);
    visited[s] = true;

    //  Path started with a node
    //  having in-degree 0 and
    //  current node has out-degree 0,
    //  print current path
    if (outdeg0[s] && indeg0[path[0]]) {
        for (auto x : path)
            cout << x << " ";
        cout << '\n';
    }

    for (auto node : adj[s]) {
        if (!visited[node])
            dfs(node);
    }

    path.pop_back();
    visited[s] = false;
}

void print_all_paths(int n)
{
    for (int i = 0; i < n; i++) {
        // for each node with in-degree 0
        // print all possible paths
        if (indeg0[i] && !adj[i].empty()) {
            dfs(i);
        }
    }
}

// Driver Code
int main()
{
    int n;
    n = 6;

    // set all nodes unvisited
    visited = vector<bool>(n, false);

    // adjacency list for nodes
    adj = vector<vector<int> >(n);

    // indeg0 and outdeg0 arrays
    indeg0 = vector<bool>(n, true);
    outdeg0 = vector<bool>(n, true);

    // edges
    vector<pair<int, int> > edges
        = { { 5, 0 }, { 5, 2 }, { 2, 3 },
            { 4, 0 }, { 4, 1 }, { 3, 1 } };

    for (int i = 0; i < edges.size(); i++) {
        int u = edges[i].first;
        int v = edges[i].second;

        adj[u].push_back(v);

        // set indeg0[v] <- false
        indeg0[v] = false;

        // set outdeg0[u] <- false
        outdeg0[u] = false;
    }
    cout << "All possible paths:\n";
    print_all_paths(n);
    return 0;
}
```

## 蟒蛇 3

```
# Python program to print all
# possible paths in a DAG

# Recursive function to print all paths
def dfs(s):
    # Append the node in path
    # and set visited
    path.append(s)
    visited[s] = True

    # Path started with a node
    # having in-degree 0 and
    # current node has out-degree 0,
    # print current path
    if outdeg0[s] and indeg0[path[0]]:
        print(*path)

    # Recursive call to print all paths
    for node in adj[s]:
        if not visited[node]:
            dfs(node)

    # Remove node from path
    # and set unvisited
    path.pop()
    visited[s] = False

def print_all_paths(n):
    for i in range(n):

        # for each node with in-degree 0
        # print all possible paths
        if indeg0[i] and adj[i]:
            path = []
            visited = [False] * (n + 1)
            dfs(i)

# Driver code
from collections import defaultdict

n = 6
# set all nodes unvisited
visited = [False] * (n + 1)
path = []

# edges = (a, b): a -> b
edges = [(5, 0), (5, 2), (2, 3),
         (4, 0), (4, 1), (3, 1)]

# adjacency list for nodes
adj = defaultdict(list)

# indeg0 and outdeg0 arrays
indeg0 = [True]*n
outdeg0 = [True]*n

for edge in edges:
    u, v = edge[0], edge[1]
    # u -> v
    adj[u].append(v)

    # set indeg0[v] <- false
    indeg0[v] = False

    # set outdeg0[u] <- false
    outdeg0[u] = False

print('All possible paths:')
print_all_paths(n)
```

**Output:** 

```
All possible paths:
4 0
4 1
5 0
5 2 3 1
```

***时间复杂度:**O(N+E)<sup>2</sup>T5
T7**辅助空间:**O(N)*T11】