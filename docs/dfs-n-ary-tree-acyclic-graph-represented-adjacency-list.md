# 表示为邻接表

的 n 元树（无环图）的 DFS

> 原文： [https://www.geeksforgeeks.org/dfs-n-ary-tree-acyclic-graph-represented-adjacency-list/](https://www.geeksforgeeks.org/dfs-n-ary-tree-acyclic-graph-represented-adjacency-list/)

给出了一个由 n 个节点组成的树，我们需要打印其 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。

**示例**：

```
Input : Edges of graph
        1 2
        1 3
        2 4
        3 5
Output : 1 2 4 3 5

```

一个简单的解决方案是实现标准 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。

我们可以修改我们的方法，以避免为访问的节点增加空间。 代替使用访问数组，我们可以跟踪父级。 我们遍历除父节点外的所有相邻节点。

下面是实现：

## C++

```cpp

/* CPP code to perform DFS of given tree : */
#include <bits/stdc++.h> 
using namespace std; 

// DFS on tree 
void dfs(vector<int> list[], int node, int arrival) 
{ 
    // Printing traversed node 
    cout << node << '\n'; 

    // Traversing adjacent edges 
    for (int i = 0; i < list[node].size(); i++) { 

        // Not traversing the parent node 
        if (list[node][i] != arrival) 
            dfs(list, list[node][i], node); 
    } 
} 

int main() 
{ 
    // Number of nodes 
    int nodes = 5; 

    // Adjacency list 
    vector<int> list[10000]; 

    // Designing the tree 
    list[1].push_back(2); 
    list[2].push_back(1); 

    list[1].push_back(3); 
    list[3].push_back(1); 

    list[2].push_back(4); 
    list[4].push_back(2); 

    list[3].push_back(5); 
    list[5].push_back(3); 

    // Function call 
    dfs(list, 1, 0); 

    return 0; 
} 

```