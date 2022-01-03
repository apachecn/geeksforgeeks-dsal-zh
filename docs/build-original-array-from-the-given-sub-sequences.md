# 从给定的子序列

构建原始数组

> 原文： [https://www.geeksforgeeks.org/build-original-array-from-the-given-sub-sequences/](https://www.geeksforgeeks.org/build-original-array-from-the-given-sub-sequences/)

给定一个整数`N`以及一个整数数组的有效子序列，其中每个元素都是不同的并且在`[0, N – 1]`范围内，任务是找到原始数组。

**示例**：

> **输入**：`N = 6`
>
> ```
> v[] = {
>   {1, 2, 3}, 
>   {1, 2}, 
>   {3, 4}, 
>   {5, 2}, 
>   {0, 5, 4}
> }
> ```
> 
> **输出**：`0 1 5 2 3 4`
> 
> **输入**：`N = 10`
>
> ```
> v[] = {
>   {9, 1, 2, 8, 8}, 
>   {6, 1, 2}, 
>   {9, 6 , 3, 4}, 
>   {5, 2, 7}, 
>   {0, 9, 5, 4}
> }
> ```
> 
> **输出**：`0 9 6 5 1 2 8 7 3 4`

**方法**：从给定的子序列构建图。 逐个选择每个子序列，并在子序列中两个相邻元素之间添加一条边。 构建图之后，对图执行拓扑排序。

请参阅[拓扑排序](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)以了解拓扑排序。 此拓扑顺序是必需的数组。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to add edge to graph 
void addEdge(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
} 

// Function to calculate indegrees of all the vertices 
void getindeg(vector<int> adj[], int V, vector<int>& indeg) 
{ 
    // If there is an edge from i to x 
    // then increment indegree of x 
    for (int i = 0; i < V; i++) { 
        for (auto x : adj[i]) { 
            indeg[x]++; 
        } 
    } 
} 

// Function to perform topological sort 
vector<int> topo(vector<int> adj[], int V, vector<int>& indeg) 
{ 
    queue<int> q; 

    // Push every node to the queue 
    // which has no incoming edge 
    for (int i = 0; i < V; i++) { 
        if (indeg[i] == 0) 
            q.push(i); 
    } 
    vector<int> res; 
    while (!q.empty()) { 
        int u = q.front(); 
        q.pop(); 
        res.push_back(u); 

        // Since edge u is removed, update the indegrees 
        // of all the nodes which had an incoming edge from u 
        for (auto x : adj[u]) { 
            indeg[x]--; 
            if (indeg[x] == 0) 
                q.push(x); 
        } 
    } 
    return res; 
} 

// Function to generate the array 
// from the given sub-sequences 
vector<int> makearray(vector<vector<int> > v, int V) 
{ 

    // Create the graph from the input sub-sequences 
    vector<int> adj[V]; 
    for (int i = 0; i < v.size(); i++) { 
        for (int j = 0; j < v[i].size() - 1; j++) { 

            // Add edge between every two consecutive 
            // elements of the given sub-sequences 
            addEdge(adj, v[i][j], v[i][j + 1]); 
        } 
    } 

    // Get the indegrees for all the vertices 
    vector<int> indeg(V, 0); 
    getindeg(adj, V, indeg); 

    // Get the topological order of the created graph 
    vector<int> res = topo(adj, V, indeg); 
    return res; 
} 

// Driver code 
int main() 
{ 
    // Size of the required array 
    int n = 10; 

    // Given sub-sequences of the array 
    vector<vector<int> > subseqs{ { 9, 1, 2, 8, 3 }, 
                                  { 6, 1, 2 }, 
                                  { 9, 6, 3, 4 }, 
                                  { 5, 2, 7 }, 
                                  { 0, 9, 5, 4 } }; 

    // Get the resultant array as vector 
    vector<int> res = makearray(subseqs, n); 

    // Printing the array 
    for (auto x : res) { 
        cout << x << " "; 
    } 

    return 0; 
} 

```