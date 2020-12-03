# 打印距离 K

内的所有邻居节点

> 原文： [https://www.geeksforgeeks.org/print-all-neigbour-nodes-within-distance-k/](https://www.geeksforgeeks.org/print-all-neigbour-nodes-within-distance-k/)

给定一个`N`个节点，`E`边，一个节点`X`和距离`K`的图形。 任务是打印距`X`距离`K`的所有节点。

> **输入**：
> ![](img/65b88bb626e719c2731da58538a65152.png)
> 
> **输出**：4 5 2 7 3
> 
> 节点 4 的距离 2 之内的 Neigbour 节点为：4 5 2 7 3

**方法**：
打印距离`K`或小于`K`的所有节点。 我们可以通过应用 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 变体来做到这一点，该变体从必须打印距离的 K 节点直到距离 K。

```
dfs(K, node, -1, tree) 

```

-1 表示节点父代。
此递归函数基本上会打印节点，然后调用 **dfs（K-1，节点的邻居，节点，树）**。
基本条件为 K > 0。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print 
// the nearest K neighbour 
// nodes (including itself) 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of an edge 
struct arr { 
    int from, to; 
}; 

// Recursive function to print 
// the neighbor nodes of a node 
// until K distance 
void dfs(int k, int node, 
         int parent, 
         const vector<vector<int> >& tree) 
{ 

    // Base condition 
    if (k < 0) 
        return; 

    // Print the node 
    cout << node << ' '; 

    // Traverse the connected 
    // nodes/adjacency list 
    for (int i : tree[node]) { 

        if (i != parent) { 

            // node i becomes the parent 
            // of its child node 
            dfs(k - 1, i, node, tree); 
        } 
    } 
} 

// Function to print nodes under 
// distance k 
void print_under_dis_K(struct arr graph[], 
                       int node, int k, 
                       int v, int e) 
{ 

    // To make graph with 
    // the given edges 
    vector<vector<int> > tree(v + 1, 
                              vector<int>()); 

    for (int i = 0; i < e; i++) { 
        int from = graph[i].from; 
        int to = graph[i].to; 

        tree[from].push_back(to); 
        tree[to].push_back(from); 
    } 

    dfs(k, node, -1, tree); 
} 

// Driver Code 
int main() 
{ 

    // Number of vertex and edges 
    int v = 7, e = 6; 

    // Given edges 
    struct arr graph[v + 1] = { 
        { 2, 1 }, 
        { 2, 5 }, 
        { 5, 4 }, 
        { 5, 7 }, 
        { 4, 3 }, 
        { 7, 6 } 
    }; 

    // k is the required distance 
    // upto which are neighbor 
    // nodes should get printed 
    int node = 4, k = 2; 

    // function calling 
    print_under_dis_K(graph, node, k, v, e); 

    return 0; 
} 

```