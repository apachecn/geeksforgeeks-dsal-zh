# 查找两个不同的良好节点之间的最短距离

> 原文： [https://www.geeksforgeeks.org/find-the-shortest-distance-between-any-pair-of-two-different-good-nodes/](https://www.geeksforgeeks.org/find-the-shortest-distance-between-any-pair-of-two-different-good-nodes/)

给定一个具有 N 个节点和 M 个边的加权无向连通图。 一些节点被标记为良好。 任务是找到两个不同的良好节点之间的最短距离。

**注意**：在以下示例中标记为黄色的节点被视为*良好节点*。

**示例**：

```
Input : 

Output : 7
Explanation : 
Pairs of Good Nodes and distance between them are:
(1 to 3) -> distance: 7, 
(3 to 5) -> distance: 9, 
(1 to 5) -> distance: 16, 
out of which 7 is the minimum.

Input : 

Output : 4

```

**方法**：让我们首先考虑一种算法，该算法可以解决给定问题的更简单版本，其中所有边的权重均为 1。

*   从此处选择一个随机的好节点并执行 BFS，并在第一级停下来，说![s](img/27afaf2b0e3eaea3d7e963f3f9a730e2.png "Rendered by QuickLaTeX.com")，它包含另一个好节点。
*   我们知道，两个好节点之间的最小距离不能超过**的**。 因此，我们再次随机选择了一个之前未取的好节点，然后再次执行 BFS。 如果在**的**距离内找不到任何特殊节点，我们将终止搜索。 如果这样做，那么我们将更新**的值**，并使用随机获取的其他一些特殊节点重复该过程。

当权重为多个时，我们可以应用类似的算法。

下面是上述方法的实现：

```

// CPP program to find the shortest pairwise 
// distance between any two different good nodes. 
#include <bits/stdc++.h> 
using namespace std; 

#define N 100005 
const int MAXI = 99999999; 

// Function to add edges 
void add_edge(vector<pair<int, int> > gr[], int x, 
              int y, int weight) 
{ 
    gr[x].push_back({ y, weight }); 
    gr[y].push_back({ x, weight }); 
} 

// Function to find the shortest 
// distance between any pair of 
// two different good nodes 
int minDistance(vector<pair<int, int> > gr[], int n, 
                int dist[], int vis[], int a[], int k) 
{ 
    // Keeps minimum element on top 
    priority_queue<pair<int, int>, vector<pair<int, int> >, 
                   greater<pair<int, int> > > q; 

    // To keep required answer 
    int ans = MAXI; 

    for (int i = 1; i <= n; i++) { 
        // If it is not good vertex 
        if (!a[i]) 
            continue; 

        // Keep all vertices not visited 
        // and distance as MAXI 
        for (int j = 1; j <= n; j++) { 
            dist[j] = MAXI; 
            vis[j] = 0; 
        } 

        // Distance from ith vertex to ith is zero 
        dist[i] = 0; 

        // Make queue empty 
        while (!q.empty()) 
            q.pop(); 

        // Push the ith vertex 
        q.push({ 0, i }); 

        // Count the good vertices 
        int good = 0; 

        while (!q.empty()) { 
            // Take the top element 
            int v = q.top().second; 

            // Remove it 
            q.pop(); 

            // If it is already visited 
            if (vis[v]) 
                continue; 
            vis[v] = 1; 

            // Count good vertices 
            good += a[v]; 

            // If distance from vth vertex 
            // is greater than ans 
            if (dist[v] > ans) 
                break; 

            // If two good vertices are found 
            if (good == 2 and a[v]) { 
                ans = min(ans, dist[v]); 
                break; 
            } 

            // Go to all adjacent vertices 
            for (int j = 0; j < gr[v].size(); j++) { 
                int to = gr[v][j].first; 
                int weight = gr[v][j].second; 

                // if distance is less 
                if (dist[v] + weight < dist[to]) { 
                    dist[to] = dist[v] + weight; 
                    q.push({ dist[to], to }); 
                } 
            } 
        } 
    } 

    // Return the required answer 
    return ans; 
} 

// Driver code 
int main() 
{ 
    // Number of vertices and edges 
    int n = 5, m = 5; 

    vector<pair<int, int> > gr[N]; 

    // Function call to add edges 
    add_edge(gr, 1, 2, 3); 
    add_edge(gr, 1, 2, 3); 
    add_edge(gr, 2, 3, 4); 
    add_edge(gr, 3, 4, 1); 
    add_edge(gr, 4, 5, 8); 

    // Number of good nodes 
    int k = 3; 

    int a[N], vis[N], dist[N]; 

    // To keep good vertices 
    a[1] = a[3] = a[5] = 1; 

    cout << minDistance(gr, n, dist, vis, a, k); 

    return 0; 
} 

```

**Output:**

```
7

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。