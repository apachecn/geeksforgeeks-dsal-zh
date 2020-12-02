# 矩阵中不可访问的位置对数

> 原文： [https://www.geeksforgeeks.org/number-pair-positions-matrix-not-accessible/](https://www.geeksforgeeks.org/number-pair-positions-matrix-not-accessible/)

给定正整数 **N** 。 考虑 **N X N** 的矩阵。 除了（x1，y1），（x2，y2）形式的给定配对单元格外，其他任何单元格都无法访问任何单元格，即在（x2，y2）到（x1，y1）之间存在一条路径（可访问） 。 任务是找到对（a1，b1），（a2，b2）的计数，以使无法从（a1，b1）访问单元（a2，b2）。

**示例：**

```
Input : N = 2
Allowed path 1: (1, 1) (1, 2)
Allowed path 2: (1, 2) (2, 2)
Output : 6
Cell (2, 1) is not accessible from any cell
and no cell is accessible from it.

(1, 1) - (2, 1)
(1, 2) - (2, 1)
(2, 2) - (2, 1)
(2, 1) - (1, 1)
(2, 1) - (1, 2)
(2, 1) - (2, 2)

```

将每个像元视为一个节点，编号从 1 到 N * N。 可以使用（x – 1）* N + y 将每个像元（x，y）映射到数字。 现在，将每个给定的允许路径视为节点之间的一条边。 这将形成连接组件的不相交集合。 现在，使用[深度优先遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)或[宽度优先遍历](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)，我们可以轻松地找到节点的数量或连接组件的大小，例如 x。 现在，不可访问的路径数为 x *（N * N – x）。 这样，我们可以找到每个连接路径的不可访问路径。

以下是此方法的实现：

## C ++

```

// C++ program to count number of pair of positions 
// in matrix which are not accessible 
#include<bits/stdc++.h> 
using namespace std; 

// Counts number of vertices connected in a component 
// containing x. Stores the count in k. 
void dfs(vector<int> graph[], bool visited[], 
                               int x, int *k) 
{ 
    for (int i = 0; i < graph[x].size(); i++) 
    { 
        if (!visited[graph[x][i]]) 
        { 
            // Incrementing the number of node in 
            // a connected component. 
            (*k)++; 

            visited[graph[x][i]] = true; 
            dfs(graph, visited, graph[x][i], k); 
        } 
    } 
} 

// Return the number of count of non-accessible cells. 
int countNonAccessible(vector<int> graph[], int N) 
{ 
    bool visited[N*N + N]; 
    memset(visited, false, sizeof(visited)); 

    int ans = 0; 
    for (int i = 1; i <= N*N; i++) 
    { 
        if (!visited[i]) 
        { 
            visited[i] = true; 

            // Initialize count of connected 
            // vertices found by DFS starting 
            // from i. 
            int k = 1; 
            dfs(graph, visited, i, &k); 

            // Update result 
            ans += k * (N*N - k); 
        } 
    } 
    return ans; 
} 

// Inserting the edge between edge. 
void insertpath(vector<int> graph[], int N, int x1, 
                             int y1, int x2, int y2) 
{ 
    // Mapping the cell coordinate into node number. 
    int a = (x1 - 1) * N + y1; 
    int b = (x2 - 1) * N + y2; 

    // Inserting the edge. 
    graph[a].push_back(b); 
    graph[b].push_back(a); 
} 

// Driven Program 
int main() 
{ 
    int N = 2; 

    vector<int> graph[N*N + 1]; 

    insertpath(graph, N, 1, 1, 1, 2); 
    insertpath(graph, N, 1, 2, 2, 2); 

    cout << countNonAccessible(graph, N) << endl; 
    return 0; 
} 

```