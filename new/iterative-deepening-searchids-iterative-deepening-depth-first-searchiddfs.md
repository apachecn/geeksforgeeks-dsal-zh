# 迭代加深搜索（IDS）或迭代加深深度优先搜索（IDDFS）

> 原文： [https://www.geeksforgeeks.org/iterative-deepening-searchids-iterative-deepening-depth-first-searchiddfs/](https://www.geeksforgeeks.org/iterative-deepening-searchids-iterative-deepening-depth-first-searchiddfs/)

遍历图形有两种常用方法： [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 和 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。 考虑到一个巨大的高度和宽度的树（或图），由于以下原因，BFS 和 DFS 都不太有效。

1.  **DFS** 首先遍历经过根的一个相邻节点，然后遍历下一个相邻节点。 这种方法的问题是，如果有一个节点靠近根，但在 DFS 探索的前几个子树中没有，那么 DFS 很晚到达该节点。 同样，DFS 可能找不到到节点的最短路径（就边缘数而言）。

[![iddfs3](img/d6de95744e5fb4eafba90e772f537210.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/iddfs3.png)

3.  **BFS** 逐级移动，但是需要更多空间。 DFS 所需的空间为 O（d），其中 d 为树的深度，而 BFS 所需的空间为 O（n），其中 n 为树中的节点数（为什么？请注意，树的最后一层可以具有约 n / 2 个节点和倒数第二个 n / 4 个节点，在 BFS 中，我们需要将每个级别逐个排在队列中。

**IDDFS** 结合了深度优先搜索的空间效率和广度优先搜索的快速搜索（针对更靠近根的节点）。

**IDDFS 如何工作？**
IDDFS 从初始值开始为不同深度调用 DFS。 在每个呼叫中​​，都限制 DFS 超出给定深度。 因此，基本上，我们以 BFS 方式进行 DFS。

**算法：**

```
// Returns true if target is reachable from
// src within max_depth
bool IDDFS(src, target, max_depth)
    for limit from 0 to max_depth
       if DLS(src, target, limit) == true
           return true
    return false   

bool DLS(src, target, limit)
    if (src == target)
        return true;

    // If reached the maximum depth, 
    // stop recursing.
    if (limit <= 0) return **false**;   

    **foreach** adjacent i of src
        **if** DLS(i, target, limit?1)             
            **return** **true**

    **return** **false**=>
```

需要注意的重要一点是，我们多次访问顶级节点。 访问最后一个（或最大深度）级别一次，访问第二个最后一个级别两次，依此类推。 它看起来似乎很昂贵，但事实证明并不是那么昂贵，因为在一棵树中，大多数节点都位于底层。 因此，是否多次访问高层并不重要。

以下是上述算法
的实现

## C / C ++

```

// C++ program to search if a target node is reachable from 
// a source with given max depth. 
#include<bits/stdc++.h> 
using namespace std; 

// Graph class represents a directed graph using adjacency 
// list representation. 
class Graph 
{ 
    int V;    // No. of vertices 

    // Pointer to an array containing 
    // adjacency lists 
    list<int> *adj; 

    // A function used by IDDFS 
    bool DLS(int v, int target, int limit); 

public: 
    Graph(int V);   // Constructor 
    void addEdge(int v, int w); 

    // IDDFS traversal of the vertices reachable from v 
    bool IDDFS(int v, int target, int max_depth); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 

// A function to perform a Depth-Limited search 
// from given source 'src' 
bool Graph::DLS(int src, int target, int limit) 
{ 
    if (src == target) 
        return true; 

    // If reached the maximum depth, stop recursing. 
    if (limit <= 0) 
        return false; 

    // Recur for all the vertices adjacent to source vertex 
    for (auto i = adj[src].begin(); i != adj[src].end(); ++i) 
       if (DLS(*i, target, limit-1) == true) 
          return true; 

     return false; 
} 

// IDDFS to search if target is reachable from v. 
// It uses recursive DFSUtil(). 
bool Graph::IDDFS(int src, int target, int max_depth) 
{ 
    // Repeatedly depth-limit search till the 
    // maximum depth. 
    for (int i = 0; i <= max_depth; i++) 
       if (DLS(src, target, i) == true) 
          return true; 

    return false; 
} 

// Driver code 
int main() 
{ 
    // Let us create a Directed graph with 7 nodes 
    Graph g(7); 
    g.addEdge(0, 1); 
    g.addEdge(0, 2); 
    g.addEdge(1, 3); 
    g.addEdge(1, 4); 
    g.addEdge(2, 5); 
    g.addEdge(2, 6); 

    int target = 6, maxDepth = 3, src = 0; 
    if (g.IDDFS(src, target, maxDepth) == true) 
        cout << "Target is reachable from source "
                "within max depth"; 
    else
        cout << "Target is NOT reachable from source "
                "within max depth"; 
    return 0; 
} 

```