# 最大派系问题| 递归解决方案

> 原文： [https://www.geeksforgeeks.org/maximal-clique-problem-recursive-solution/](https://www.geeksforgeeks.org/maximal-clique-problem-recursive-solution/)

给定一个带有`N`个节点和`E`边缘的小图，任务是在给定图中找到最大的**群体**。 集团是给定图的完整子图。 这意味着所述子图中的所有节点都直接相互连接，或者子图中的任何两个节点之间都有一条边。 最大派系是给定图的完整子图，其中包含最大数量的节点。

**示例**：

> **输入**：N = 4，边缘[] [] = {{1，2}，{2，3}，{3，1}，{4，3}，{4，1}，{ 4，2}}
> **输出**：4
> 
> **输入**：N = 5，边缘[] [] = {{1，2}，{2，3}，{3，1}，{4，3}，{4，5}，{ 5，3}}
> **输出**：3

**方法**：的想法是使用递归解决问题。

*   将边缘添加到当前列表后，检查是否通过将该边缘添加到当前列表中是否仍然形成集团。
*   将添加顶点，直到列表不形成集团为止。 然后，该列表被回溯以找到形成集团的更大子集。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 100; 

// Stores the vertices 
int store[MAX], n; 

// Graph 
int graph[MAX][MAX]; 

// Degree of the vertices 
int d[MAX]; 

// Function to check if the given set of 
// vertices in store array is a clique or not 
bool is_clique(int b) 
{ 

    // Run a loop for all set of edges 
    for (int i = 1; i < b; i++) { 
        for (int j = i + 1; j < b; j++) 

            // If any edge is missing 
            if (graph[store[i]][store[j]] == 0) 
                return false; 
    } 
    return true; 
} 

// Function to find all the sizes 
// of maximal cliques 
int maxCliques(int i, int l) 
{ 
    // Maximal clique size 
    int max_ = 0; 

    // Check if any vertices from i+1 
    // can be inserted 
    for (int j = i + 1; j <= n; j++) { 

        // Add the vertex to store 
        store[l] = j; 

        // If the graph is not a clique of size k then 
        // it cannot be a clique by adding another edge 
        if (is_clique(l + 1)) { 

            // Update max 
            max_ = max(max_, l); 

            // Check if another edge can be added 
            max_ = max(max_, maxCliques(j, l + 1)); 
        } 
    } 
    return max_; 
} 

// Driver code 
int main() 
{ 
    int edges[][2] = { { 1, 2 }, { 2, 3 }, { 3, 1 },  
                       { 4, 3 }, { 4, 1 }, { 4, 2 } }; 
    int size = sizeof(edges) / sizeof(edges[0]); 
    n = 4; 

    for (int i = 0; i < size; i++) { 
        graph[edges[i][0]][edges[i][1]] = 1; 
        graph[edges[i][1]][edges[i][0]] = 1; 
        d[edges[i][0]]++; 
        d[edges[i][1]]++; 
    } 

    cout << maxCliques(0, 1); 

    return 0; 
} 

```