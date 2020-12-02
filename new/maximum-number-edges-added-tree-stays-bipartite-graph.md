# 要添加到树上以使其保持二分图的最大边数

> 原文： [https://www.geeksforgeeks.org/maximum-number-edges-added-tree-stays-bipartite-graph/](https://www.geeksforgeeks.org/maximum-number-edges-added-tree-stays-bipartite-graph/)

一棵树始终是[二分图](https://www.geeksforgeeks.org/bipartite-graph/)，因为我们总是可以分成两个具有交替级别的不相交集。 换句话说，我们总是用两种颜色对其进行着色，以使备用色阶具有相同的颜色。 任务是计算最大编号。 可以添加到树中的边的数量，以便保留为二部图。

**示例：**

```
Input : Tree edges as vertex pairs 
        1 2
        1 3
Output : 0
Explanation :
The only edge we can add is from node 2 to 3.
But edge 2, 3 will result in odd cycle, hence 
violation of Bipartite Graph property.

Input : Tree edges as vertex pairs 
        1 2
        1 3
        2 4
        3 5
Output : 2
Explanation : On colouring the graph, {1, 4, 5} 
and {2, 3} form two different sets. Since, 1 is 
connected from both 2 and 3, we are left with 
edges 4 and 5\. Since, 4 is already connected to
2 and 5 to 3, only options remain {4, 3} and 
{5, 2}.

```

1）对图形进行简单的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) （或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) ）遍历，并用两种颜色对其进行着色。
2）在着色的同时，还要跟踪用两种颜色着色的节点数。 设两个计数为 count_color <sub>0</sub> 和 count_color <sub>1</sub> 。
3）现在我们知道二元图可以具有的最大边数是 count_color <sub>0</sub> x count_color <sub>1</sub> 。
4）我们还知道具有 n 个节点的树具有 n-1 个边。
5）因此，我们的答案是 count_color <sub>0</sub> x count_color <sub>1</sub> –（n-1）。

下面是实现：

## C ++

```

// CPP code to print maximum edges such that 
// Tree remains a Bipartite graph 
#include <bits/stdc++.h> 
using namespace std; 

// To store counts of nodes with two colors 
long long count_color[2]; 

void dfs(vector<int> adj[], int node, int parent, int color) 
{ 
    // Increment count of nodes with current 
    // color 
    count_color[color]++; 

    // Traversing adjacent nodes 
    for (int i = 0; i < adj[node].size(); i++) { 

        // Not recurring for the parent node 
        if (adj[node][i] != parent) 
            dfs(adj, adj[node][i], node, !color); 
    } 
} 

// Finds maximum number of edges that can be added 
// without violating Bipartite property. 
int findMaxEdges(vector<int> adj[], int n) 
{ 
    // Do a DFS to count number of nodes 
    // of each color 
    dfs(adj, 1, 0, 0); 

    return count_color[0] * count_color[1] - (n - 1); 
} 

// Driver code 
int main() 
{ 
    int n = 5; 
    vector<int> adj[n + 1]; 
    adj[1].push_back(2); 
    adj[1].push_back(3); 
    adj[2].push_back(4); 
    adj[3].push_back(5); 
    cout << findMaxEdges(adj, n); 
    return 0; 
} 

```