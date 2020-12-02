# 形成三角形需要增加的最小边数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-edges-that-need-to-be-added-to-form-a-triangle/](https://www.geeksforgeeks.org/minimum-number-of-edges-that-need-to-be-added-to-form-a-triangle/)

给定具有`N`个顶点和`N`边的无向图。 没有两个边连接同一对顶点。 三角形是一组三个不同的顶点，这样，每对顶点通过一条边连接，即，三个不同的顶点`u`，`v`和`w`是 如果图形包含边线**（u，v）**，**（v，w）**和**（v，u）**则为三角形。
该任务是找到需要添加到给定图形的最小边数，以使该图形包含至少一个三角形。

**示例**：

```
Input:
  1
 / \
2   3
Output: 1

Input:
  1     3
 /     /
2     4
Output: 2

```

**方法**：初始化 **ans = 3** ，这是形成三角形所需的最大边数。 现在，对于每个可能的顶点三元组，有四种情况：

1.  **情况 1**：如果存在节点`i`，`j`和`k`，使得从**（i，j ）**，**（j，k）**和**（k，i）**，则答案为`0`。
2.  **情况 2**：如果存在节点`i`，`j`和`k`，使得仅连接了两对顶点，则单个边为 需要形成一个三角形。 因此，更新 **ans = min（ans，1）**。
3.  **情况 3**：否则，如果仅连接一对顶点，则 **ans = min（ans，2）**。
4.  **情况 4**：当没有边缘时，则 **ans = min（ans，3）**。

最后打印**和**。

下面是上述方法的实现。

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the minimum number 
// of edges that need to be added to 
// the given graph such that it 
// contains at least one triangle 
int minEdges(vector<pair<int, int> > v, int n) 
{ 

    // adj is the adjacency matrix such that 
    // adj[i][j] = 1 when there is an 
    // edge between i and j 
    vector<vector<int> > adj; 
    adj.resize(n + 1); 
    for (int i = 0; i < adj.size(); i++) 
        adj[i].resize(n + 1, 0); 

    // As the graph is undirected 
    // so there will be an edge 
    // between (i, j) and (j, i) 
    for (int i = 0; i < v.size(); i++) { 
        adj[v[i].first][v[i].second] = 1; 
        adj[v[i].second][v[i].first] = 1; 
    } 

    // To store the required 
    // count of edges 
    int edgesNeeded = 3; 

    // For every possible vertex triplet 
    for (int i = 1; i <= n; i++) { 
        for (int j = i + 1; j <= n; j++) { 
            for (int k = j + 1; k <= n; k++) { 

                // If the vertices form a triangle 
                if (adj[i][j] && adj[j][k] && adj[k][i]) 
                    return 0; 

                // If no edges are present 
                if (!(adj[i][j] || adj[j][k] || adj[k][i])) 
                    edgesNeeded = min(edgesNeeded, 3); 

                else { 

                    // If only 1 edge is required 
                    if ((adj[i][j] && adj[j][k]) 
                        || (adj[j][k] && adj[k][i]) 
                        || (adj[k][i] && adj[i][j])) { 
                        edgesNeeded = 1; 
                    } 

                    // Two edges are required 
                    else
                        edgesNeeded = min(edgesNeeded, 2); 
                } 
            } 
        } 
    } 
    return edgesNeeded; 
} 

// Driver code 
int main() 
{ 

    // Number of nodes 
    int n = 3; 

    // Storing the edges in a vector of pairs 
    vector<pair<int, int> > v = { { 1, 2 }, { 1, 3 } }; 

    cout << minEdges(v, n); 

    return 0; 
} 

```