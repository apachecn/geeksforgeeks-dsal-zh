# 查找相等距离处的一对节点数

> 原文： [https://www.geeksforgeeks.org/find-count-of-pair-of-nodes-at-even-distance/](https://www.geeksforgeeks.org/find-count-of-pair-of-nodes-at-even-distance/)

给定一个具有 **N 个**节点和 **N-1 个边**的连接的非循环图，找出一对彼此等距的节点。

**示例**：

```
Input:
3
1 2 
2 3
Output: 1
Explanation:
    1
   /
  2
 /
3
Input:
5
1 2
2 3
1 4
4 5
Output: 4

```

**方法**：

*   假设一个图形有 6 个级别（0 到 5），级别 0、2、4 处于偶数距离，而级别 1、3、5 也处于偶数距离，因为它们的差为 2，这是偶数，因此我们必须同时注意 条件，即同时计算偶数和奇数两个级别。
*   给定的问题可以通过执行 dfs 遍历来解决
*   选择任何源节点作为根，并执行 dfs 遍历并维护访问的
    数组，以执行 dfs 和 dist 数组以计算到根的距离
*   现在遍历偏差数组并保留偶数级和奇数级的计数
*   计算总计为（（（even_count *（even_count-1））+（odd_count *（odd_count-1））/ 2）

以下是上述方法的实现：

## C ++

```

// C++ program to find 
// the count of nodes 
// at even distance 
#include <bits/stdc++.h> 
using namespace std; 

// Dfs function to find count of nodes at 
// even distance 
void dfs(vector<int> graph[], int node, int dist[],  
                                    bool vis[], int c) 
{ 
    if (vis[node]) { 
        return; 
    } 
    // Set flag as true for current 
    // node in visited array 
    vis[node] = true; 

    // Insert the distance in 
    // dist array for current 
    // visited node u 
    dist[node] = c; 

    for (int i = 0; i < graph[node].size(); i++) { 
        // If its neighbours are not vis, 
        // run dfs for them 
        if (!vis[graph[node][i]]) { 
            dfs(graph, graph[node][i], dist, vis, c + 1); 
        } 
    } 
} 

int countOfNodes(vector<int> graph[], int n) 
{ 
    // bool array to 
    // mark visited nodes 
    bool vis[n + 1] = { false }; 

    // Integer array to 
    // compute distance 
    int dist[n + 1] = { 0 }; 

    dfs(graph, 1, dist, vis, 0); 

    int even = 0, odd = 0; 

    // Traverse the distance array 
    // and count the even and odd levels 
    for (int i = 1; i <= n; i++) { 
        if (dist[i] % 2 == 0) { 
            even++; 
        } 
        else { 
            odd++; 
        } 
    } 

    int ans = ((even * (even - 1)) + (odd * (odd - 1))) / 2; 

    return ans; 
} 

// Driver code 
int main() 
{ 

    int n = 5; 
    vector<int> graph[n + 1] = { {}, 
                                 { 2 }, 
                                 { 1, 3 }, 
                                 { 2 } }; 

    int ans = countOfNodes(graph, n); 
    cout << ans << endl; 

    return 0; 
} 

```