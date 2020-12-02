# 要从无向图上移除的最小标记节点，使得不存在循环

> 原文： [https://www.geeksforgeeks.org/minimum-labelled-node-to-be-removed-from-undirected-graph-such-that-there-is-no-cycle/](https://www.geeksforgeeks.org/minimum-labelled-node-to-be-removed-from-undirected-graph-such-that-there-is-no-cycle/)

给定从 1 到 N 标记的`N`个节点的**无向图**，任务是找到应从图中删除的最小标记节点，以使所得图没有循环。

**注意**：如果初始图形没有循环，即不需要删除任何节点，则打印-1。

**示例**：

> **输入**：N = 5，边缘[] [] = {{5，1}，{5，2}，{1，2}，{2，3}，{2，4}}}
> **输出**：1
> **说明**：
> 如果除去节点 1，则结果图没有循环。 同样，也可以通过删除节点 2 来避免该周期。
> 由于我们必须找到标记为最小的节点，因此答案为 1。
> 
> **输入**：N = 5，边缘[] [] = {{4，5}，{4，1}，{4，2}，{4，3}，{5，1}，{ 5，2}}
> **输出**：4

**天真的方法**：针对此问题的天真的方法是分别删除每个顶点并检查所得图形是否具有循环。 这种方法的时间复杂度是二次的。

**高效方法**：想法是在给定图上应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并观察形成的 dfs 树。

*   [后边缘](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)被称为不是构建的 DFS 树的一部分的边缘，并且是某个节点 v 与 v 的祖先之一之间的边缘。
*   显然，图的所有那些不属于 DFS 树的边缘都是后边缘。
*   如果图中没有后沿，则图中没有循环。 因此，在这种情况下，答案将是`-1`。

如果图中有[个后边缘](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)，则我们需要找到最小边缘。 为此，我们需要检查在从图形中删除特定边时是否删除了循环。 因此，让`v`是我们当前正在检查的顶点。 因此，必须在**以下条件之后加上顶点 v** ，以便在移除时不会导致循环：

*  `v`必须位于连接图中每个[后边缘](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)端点的树路径上。
    **证明**：假设存在一些后沿 x-y，使得 v 不在树路径上。 如果删除 v，我们仍然可以从 x 遍历到 y，并通过后边缘返回 x，表明该循环没有删除。
*   v 的子树必须具有至 v 的任何祖先的至多一个后边缘。 和 z 是 v 的祖先。如果删除 v，显然仍然存在一个循环，该循环包括 w 到 y 之间的路径，x 到 z 的路径以及两个后边缘 wx 和 yz，即，不删除循环。

因此，其思想是跟踪后边缘，并为节点的任何祖先节点的子树中的后边缘数量提供指示器。 为了跟踪后边缘，我们将使用[修改的 DFS 图形着色算法](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)。

为了检查子树 v 是否具有至 v 的任何祖代的至多一个后边缘，我们实现 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 使其返回 v 的子树的两个最高边缘的深度。 一个数组，如果节点“ i”是否满足上述条件 2，则存储数组中的每个索引“ i”。 类似地，实现了两个数组，一个用于子级，另一个用于父级，以查看节点 v 是否位于连接端点的树路径上。

下面是上述方法的实现：

```

// C++ implementation to find the 
// minimum labelled node to be 
// removed such that there is no 
// cycle in the undirected graph 

#include <bits/stdc++.h> 

using namespace std; 

const int MAX = 100005; 

int totBackEdges; 
int countAdj[MAX], small[MAX]; 

// Variables to store if a node V has 
// at-most one back edge and store the 
// depth of the node for the edge 
int isPossible[MAX], depth[MAX]; 

vector<int> adj[MAX]; 
int vis[MAX]; 

// Function to swap the pairs of the graph 
void change(pair<int, int>& p, int x) 
{ 
    // If the second value is 
    // greater than x 
    if (p.second > x) 
        p.second = x; 

    // Put the pair in the ascending 
    // order internally 
    if (p.first > p.second) 
        swap(p.first, p.second); 
} 

// Function to perform the DFS 
pair<int, int> dfs(int v, int p = -1, int de = 0) 
{ 
    // Initialise with the large value 
    pair<int, int> answer(100000000, 100000000); 

    // Storing the depth of this vertex 
    depth[v] = de; 

    // Mark the vertex as visited 
    vis[v] = 1; 
    isPossible[v] = 1; 

    // Iterating through the graph 
    for (int u : adj[v]) { 

        // If the node is a child node 
        if (u ^ p) { 

            // If the child node is unvisited 
            if (!vis[u]) { 

                // Move to the child and increase 
                // the depth 
                auto x = dfs(u, v, de + 1); 

                // increase according to algorithm 
                small[v] += small[u]; 

                change(answer, x.second); 
                change(answer, x.first); 

                // If the node is not having 
                // exactly K backedges 
                if (x.second < de) 
                    isPossible[v] = 0; 
            } 

            // If the child is already visited 
            // and in current dfs 
            // (because colour is 1) 
            // then this is a back edge 
            else if (vis[u] == 1) { 
                totBackEdges++; 

                // Increase the countAdj values 
                countAdj[v]++; 
                countAdj[u]++; 
                small[p]++; 
                small[u]--; 
                change(answer, depth[u]); 
            } 
        } 
    } 

    // Colour this vertex 2 as 
    // we are exiting out of 
    // dfs for this node 
    vis[v] = 2; 
    return answer; 
} 

// Function to find the minimum labelled 
// node to be removed such that 
// there is no cycle in the undirected graph 
int minNodetoRemove( 
    int n, 
    vector<pair<int, int> > edges) 
{ 

    // Construct the graph 
    for (int i = 0; i < edges.size(); i++) { 
        adj[edges[i].first] 
            .push_back(edges[i].second); 
        adj[edges[i].second] 
            .push_back(edges[i].first); 
    } 

    // Mark visited as false for each node 
    memset(vis, 0, sizeof(vis)); 

    totBackEdges = 0; 

    // Apply dfs on all unmarked nodes 
    for (int v = 1; v <= n; v++) { 
        if (!vis[v]) 
            dfs(v); 
    } 

    // If no backedges in the initial graph 
    // this means that there is no cycle 
    // So, return -1 
    if (totBackEdges == 0) 
        return -1; 

    int node = -1; 

    // Iterate through the vertices and 
    // return the first node that 
    // satisfies the condition 
    for (int v = 1; v <= n; v++) { 

        // Check whether the count sum of 
        // small[v] and count is the same as 
        // the total back edges and 
        // if the vertex v can be removed 
        if (countAdj[v] + small[v] 
                == totBackEdges 
            && isPossible[v]) { 
            node = v; 
        } 
        if (node != -1) 
            break; 
    } 

    return node; 
} 

// Driver code 
int main() 
{ 
    int N = 5; 
    vector<pair<int, int> > edges; 
    edges.push_back(make_pair(5, 1)); 
    edges.push_back(make_pair(5, 2)); 
    edges.push_back(make_pair(1, 2)); 
    edges.push_back(make_pair(2, 3)); 
    edges.push_back(make_pair(2, 4)); 

    cout << minNodetoRemove(N, edges); 
} 

```

**Output:**

```
1

```

**时间复杂度**：*O（N + M）*，其中 N 是节点数，M 是边数。

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。