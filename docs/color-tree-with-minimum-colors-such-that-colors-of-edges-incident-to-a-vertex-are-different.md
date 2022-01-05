# 颜色最小的颜色树，使得入射到顶点的边的颜色不同

> 原文:[https://www . geeksforgeeks . org/color-tree-with-minimum-colors-colors-of-edge-incident-to-a-vertex-is-different/](https://www.geeksforgeeks.org/color-tree-with-minimum-colors-such-that-colors-of-edges-incident-to-a-vertex-are-different/)

给定一个节点为 **N** 的树。任务是用最少数量的颜色( **K** )给树着色，使得入射到顶点的边的颜色不同。在第一行打印 **K** ，然后在下一行打印**N–1**用空格分隔的整数表示边缘的颜色。

**示例:**

```
Input: N = 3, edges[][] = {{0, 1}, {1, 2}}
                   0
                  /  
                 1
                /
               2  
Output:
2
1 2
                   0
                  / (1) 
                 1
                / (2)
               2

Input: N = 8, edges[][] = {{0, 1}, {1, 2}, 
                           {1, 3}, {1, 4}, 
                           {3, 6}, {4, 5}, 
                           {5, 7}}
                    0
                   /
                  1
                / \ \
               2   3 4
                  /   \
                 6     5
                        \
                         7
Output:
4
1 2 3 4 1 1 2

```

**进场:**首先我们来思考一下颜色的最小数量 **K** 。对于每个顶点 **v** ，**度(v) ≤ K** 应满足(其中**度(v)** 表示顶点 **v** 的度数)。事实上，存在一个所有 **K** 颜色都不同的顶点。首先选择一个顶点，让它成为根，这样 **T** 就会成为一棵有根的树。从根开始执行广度优先搜索。对于每个顶点，逐个确定其子顶点之间的边的颜色。对于每条边，使用那些不用作边颜色的边中索引最小的颜色，这些边的一个端点是当前顶点。那么颜色的各项指标不超过 **K** 。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Add an edge between the vertexes
void add_edge(vector<vector<int> >& gr, int x,
              int y, vector<pair<int, int> >& edges)
{
    gr[x].push_back(y);
    gr[y].push_back(x);
    edges.push_back({ x, y });
}

// Function to color the tree with minimum
// number of colors such that the colors of
// the edges incident to a vertex are different
int color_tree(int n, vector<vector<int> >& gr,
               vector<pair<int, int> >& edges)
{

    // To store the minimum colors
    int K = 0;

    // To store color of the edges
    map<pair<int, int>, int> color;

    // Color of edge between its parent
    vector<int> cs(n, 0);

    // To check if the vertex is
    // visited or not
    vector<int> used(n, 0);

    queue<int> que;
    used[0] = 1;
    que.emplace(0);

    while (!que.empty()) {

        // Take first element of the queue
        int v = que.front();
        que.pop();

        // Take the possible value of K
        if (K < (int)gr[v].size())
            K = gr[v].size();

        // Current color
        int cur = 1;

        for (int u : gr[v]) {

            // If vertex is already visited
            if (used[u])
                continue;

            // If the color is similar
            // to it's parent
            if (cur == cs[v])
                cur++;

            // Assign the color
            cs[u] = color[make_pair(u, v)]
                = color[make_pair(v, u)] = cur++;

            // Mark it visited
            used[u] = 1;

            // Push into the queue
            que.emplace(u);
        }
    }

    // Print the minimum required colors
    cout << K << endl;

    // Print the edge colors
    for (auto p : edges)
        cout << color[p] << " ";
}

// Driver code
int main()
{
    int n = 8;

    vector<vector<int> > gr(n);
    vector<pair<int, int> > edges;

    // Add edges
    add_edge(gr, 0, 1, edges);
    add_edge(gr, 1, 2, edges);
    add_edge(gr, 1, 3, edges);
    add_edge(gr, 1, 4, edges);
    add_edge(gr, 3, 6, edges);
    add_edge(gr, 4, 5, edges);
    add_edge(gr, 5, 7, edges);

    // Function call
    color_tree(n, gr, edges);

    return 0;
}
```

## 计算机编程语言

```
# Python3 implementation of the approach
from collections import deque as queue

gr = [[] for i in range(100)]
edges = []

# Add an edge between the vertexes
def add_edge(x, y):
    gr[x].append(y)
    gr[y].append(x)
    edges.append([x, y])

# Function to color the tree with minimum
# number of colors such that the colors of
# the edges incident to a vertex are different
def color_tree(n):

    # To store the minimum colors
    K = 0

    # To store color of the edges
    color = dict()

    # Color of edge between its parent
    cs = [0] * (n)

    # To check if the vertex is
    # visited or not
    used = [0] * (n)

    que = queue()
    used[0] = 1
    que.append(0)

    while (len(que) > 0):

        # Take first element of the queue
        v = que.popleft()

        # Take the possible value of K
        if (K < len(gr[v])):
            K = len(gr[v])

        # Current color
        cur = 1

        for u in gr[v]:

            # If vertex is already visited
            if (used[u]):
                continue

            # If the color is similar
            # to it's parent
            if (cur == cs[v]):
                cur += 1

            # Assign the color
            cs[u] = cur
            color[(u, v)] = color[(v, u)] = cur
            cur += 1

            # Mark it visited
            used[u] = 1

            # Push into the queue
            que.append(u)

    # Print minimum required colors
    print(K)

    # Print edge colors
    for p in edges:
        i = (p[0], p[1])
        print(color[i], end = " ")

# Driver code
n = 8

# Add edges
add_edge(0, 1)
add_edge(1, 2)
add_edge(1, 3)
add_edge(1, 4)
add_edge(3, 6)
add_edge(4, 5)
add_edge(5, 7)

# Function call
color_tree(n)

# This code is contributed by mohit kumar 29
```

**Output:**

```
4
1 2 3 4 1 1 2

```