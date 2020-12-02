# 图

中最远节点的距离的最小值

> 原文： [https://www.geeksforgeeks.org/minimum-value-of-distance-of-farthest-node-in-a-graph/](https://www.geeksforgeeks.org/minimum-value-of-distance-of-farthest-node-in-a-graph/)

给定一个无环无向图，它具有 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr [] []** 形式的 **N 个**节点和 **N-1 个**边缘。 其每行由两个数字 **L 和 R** 组成，表示 **L 和 R** 之间的边缘。 对于树中的每个节点 **X** ，令 **dis（X）**表示从 **X** 到最远节点的边数。 任务是找到给定图的 **dis（x）**的最小值。

**示例：**

> **输入：** N = 6，arr [] [] = {{1，4}，{2，3}，{3，4}，{4，5}，{5，6}}
> **输出：** 2
> **说明：**
> 下图是来自上述信息的图形：
> [![](img/fc16f9c3fc5220964c13895ca1fa15e9.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200327091323/DFSTraversal.jpg) 
> 从上图可以看到，距顶点 0 最远的节点位于距离 3 处。通过对图中所有节点重复进行 DFS 遍历，我们可以得出从源节点到最远节点的最大 distance []为：
> distance [ ] = {3，4，3，2，3，4}，距离的最小值是必需的结果。
> 
> **输入：** N = 6，arr [] [] = {{1，2}，{1，3}，{1，4}，{2，5}，{2，6}} [
> **输出：** 2
> **说明：**
> 上图从每个节点到最远节点的 distance []为：
> distance [] = {3 ，4，3，2，3，4}，距离的最小值为 1。

**方法：**
的想法是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)解决此问题。 步骤如下：

1.  对于任何节点（例如**或**），都使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历图，节点自身的距离为 0。
2.  对于节点**和**的每个递归调用，请不断更新[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中节点**和**的递归节点的距离（例如 **distance []** ）。
3.  通过在每次对 Node a 的递归调用中获取最大距离，可以给出**和**最远**节点之间的边数。**
4.  对图中的所有节点重复上述步骤，并继续更新距离[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)（ **distance []** ）中每个节点的最远节点距离。
5.  数组 **distance []** 的最小值是所需的结果。

下面是上述方法的实现：

## C ++

```

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Distance vector to find the distance of 
// a node to it's farthest node 
vector<int> dist; 

// To keep the track of visited array 
// while DFS Traversal 
vector<int> vis; 

// Function for DFS traversal to update 
// the distance vector 
void dfs(int u, vector<int> Adj[], int s) 
{ 
    // Mark the visited array for vertex u 
    vis[u] = true; 

    // Traverse the adjacency list for u 
    for (auto& it : Adj[u]) { 

        // If the any node is not visited, 
        // then recursively call for next 
        // vertex with distance increment 
        // by 1 
        if (vis[it] == false) { 
            dfs(it, Adj, s + 1); 
        } 
    } 

    // Update the maximum distance for the 
    // farthest vertex from node u 
    dist[u] = max(dist[u], s); 
} 

// Function to find the minimum of the 
// farthest vertex for every vertex in 
// the graph 
void minFarthestDistance(int arr[][2], int n) 
{ 

    // Resize distance vector 
    dist.resize(n + 1, 0); 

    // To create adjacency list for graph 
    vector<int> Adj[n + 1]; 

    // Create Adjacency list for every 
    // edge given in arr[][] 
    for (int i = 0; i < n - 1; i++) { 
        Adj[arr[i][0]].push_back(arr[i][1]); 
        Adj[arr[i][1]].push_back(arr[i][0]); 
    } 

    // DFS Traversal for every node in the 
    // graph to update the distance vector 
    for (int i = 1; i <= n; i++) { 

        // Clear and resize vis[] before 
        // DFS traversal for every vertex 
        vis.clear(); 
        vis.resize(n + 1, false); 

        // DFS Traversal for vertex i 
        dfs(i, Adj, 0); 
    } 

    cout << *min_element(dist.begin() + 1, 
                         dist.end()); 
} 

// Driver Code 
int main() 
{ 
    // Number of Nodes 
    int N = 6; 
    int arr[][2] = { { 1, 4 }, { 2, 3 }, { 3, 4 },  
                     { 4, 5 }, { 5, 6 } }; 

    minFarthestDistance(arr, N); 
    return 0; 
} 

```