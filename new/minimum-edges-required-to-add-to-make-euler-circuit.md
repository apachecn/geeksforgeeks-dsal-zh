# 建立欧拉电路

所需的最小边沿

> 原文： [https://www.geeksforgeeks.org/minimum-edges-required-to-add-to-make-euler-circuit/](https://www.geeksforgeeks.org/minimum-edges-required-to-add-to-make-euler-circuit/)

给定`n`个节点和`m`边的无向图。 任务是在给定图中找到制造[欧拉电路](https://www.geeksforgeeks.org/eulerian-path-and-circuit/)所需的最小边沿。

**示例**：

```
Input : n = 3, 
        m = 2
        Edges[] = {{1, 2}, {2, 3}}
Output : 1

By connecting 1 to 3, we can create a Euler Circuit.

```

为了使图中的欧拉回路存在，我们要求每个节点都应具有偶数度，因为在输入节点之后，存在一条可用于退出节点的边。

现在，有两种情况：

**1.图**

中只有一个连接的分量。在这种情况下，如果图中的所有节点都是偶数度，则我们说 图已经有一个欧拉电路，我们不需要在其中添加任何边。 但是，如果有任何奇数度的节点，则需要添加边。

图中可以有偶数个奇数度顶点。 这很容易通过以下事实证明：偶数度数节点的度数和奇数度数节点的度数之和应始终等于总度数，即使每个边沿都为该和贡献两个。 现在，如果我们将图中的随机奇数度节点配对并在它们之间添加一条边，我们可以使所有节点都具有偶数度，从而使欧拉电路存在。

**2.图形**

中存在断开连通组件。我们首先将组件标记为奇数和偶数。 奇数分量是其中至少具有一个奇数度节点的分量。 取所有偶数分量，并从每个分量中选择一个随机顶点，然后将它们线性排列。 现在，我们在相邻顶点之间添加一条边。 因此，我们已经连接了偶数分量，并制作了一个等效的奇数分量，该分量具有两个奇数度的节点。

现在处理奇数分量，即具有至少一个奇数度节点的分量。 我们可以使用边数等于未连通组件数的边来连接所有这些奇数组件。 这可以通过以下方式完成：将组件按循环顺序放置，并从每个组件中选择两个奇数度节点，然后使用它们将其连接到任一侧的组件。 现在，我们已经讨论了单个连通组件。

以下是此方法的实现：

## C++

```cpp

// C++ program to find minimum edge required 
// to make Euler Circuit 
#include <bits/stdc++.h> 
using namespace std; 

// Depth-First Search to find a connected 
// component 
void dfs(vector<int> g[], int vis[], int odd[], 
                    int deg[],  int comp, int v) 
{ 
    vis[v] = 1; 

    if (deg[v]%2 == 1) 
        odd[comp]++; 

    for (int u : g[v]) 
        if (vis[u] == 0) 
            dfs(g, vis, odd, deg, comp, u); 
} 

// Return minimum edge required to make Euler 
// Circuit 
int minEdge(int n, int m, int s[], int d[]) 
{ 
    // g : to store adjacency list 
    //     representation of graph. 
    // e : to store list of even degree vertices 
    // o : to store list of odd degree vertices 
    vector<int> g[n+1], e, o; 

    int deg[n+1];  // Degrees of vertices 
    int vis[n+1];  // To store visited in DFS 
    int odd[n+1];  // Number of odd nodes in components 
    memset(deg, 0, sizeof(deg)); 
    memset(vis, 0, sizeof(vis)); 
    memset(odd, 0, sizeof(odd)); 

    for (int i = 0; i < m; i++) 
    { 
        g[s[i]].push_back(d[i]); 
        g[d[i]].push_back(s[i]); 
        deg[s[i]]++; 
        deg[d[i]]++; 
    } 

    // 'ans' is result and 'comp' is component id 
    int ans = 0, comp = 0; 
    for (int i = 1; i <= n; i++) 
    { 
        if (vis[i]==0) 
        { 
            comp++; 
            dfs(g, vis, odd, deg, comp, i); 

            // Checking if connected component 
            // is odd. 
            if (odd[comp] == 0) 
                e.push_back(comp); 

            // Checking if connected component 
            // is even. 
            else
                o.push_back(comp); 
        } 
    } 

    // If whole graph is a single connected 
    // component with even degree. 
    if (o.size() == 0 && e.size() == 1) 
        return 0; 

    // If all connected component is even 
    if (o.size() == 0) 
        return e.size(); 

    // If graph have atleast one even connected 
    // component 
    if (e.size() != 0) 
        ans += e.size(); 

    // For all the odd connected component. 
    for (int i : o) 
        ans += odd[i]/2; 

    return ans; 
} 

// Driven Program 
int main() 
{ 
    int n = 3, m = 2; 
    int source[] = { 1, 2 }; 
    int destination[] = { 2, 3 }; 

    cout << minEdge(n, m, source, destination) << endl; 
    return 0; 
} 

```