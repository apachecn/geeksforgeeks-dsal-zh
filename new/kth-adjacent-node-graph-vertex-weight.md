# 图中第 k 个最重的相邻节点，其中每个顶点都有权重

> 原文： [https://www.geeksforgeeks.org/kth-adjacent-node-graph-vertex-weight/](https://www.geeksforgeeks.org/kth-adjacent-node-graph-vertex-weight/)

给定正数`k`和`N`个节点的无向​​图，从 0 到 N-1 编号，每个节点都具有与之相关的权重。 请注意，这与正常加权图不同，在正常加权图中，每个边都有权重。

对于每个节点，如果按照降序对直接连接到其上的节点（按照它们的权重）进行排序，那么位于`k`位置的节点数将是多少。 为每个节点打印第 k 个节点号（非权重），如果不存在，则打印-1。

**示例**：

```
Input : N = 3, k = 2, wt[] = { 2, 4, 3 }.
edge 1: 0 2
edge 2: 0 1
edge 3: 1 2

Output : 2 0 0
Graph:
         0 (weight 2)
        / \
       /   \
      1-----2
(weight 4)  (weight 3)
For node 0, sorted (decreasing order) nodes
according to their weights are node 1(weight 4),
node 2(weight 3). The node at 2nd position for
node 0 is node 2.
For node 1, sorted (decreasing order) nodes 
according to their weight are node 2(weight 3), 
node 0(weight 2). The node at 2nd position for 
node 1 is node 0.
For node 2, sorted (decreasing order) nodes 
according to their weight are node 1(weight 4),
node 0(weight 2). The node at 2nd position for
node 2 is node 0.

```

这个想法是根据相邻节点的权重对每个节点的邻接表进行排序。
首先，为所有节点创建邻接列表。 现在，对于每个节点，所有直接与其连接的节点都存储在一个列表中。 在邻接列表中，存储节点及其权重。

现在，对于每个节点，以相反的顺序对直接连接到它的所有节点的权重进行排序，然后打印每个节点列表中第 k 位的节点号。

以下是此方法的实现：

## C ++

```

// C++ program to find Kth node weight after s 
// orting of nodes directly connected to a node. 
#include<bits/stdc++.h> 
using namespace std; 

// Print Kth node number for each node after sorting 
// connected node according to their weight. 
void printkthnode(vector< pair<int, int> > adj[], 
                        int wt[], int n, int k) 
{ 
    // Sort Adjacency List of all node on the basis 
    // of its weight. 
    for (int i = 0; i < n; i++) 
      sort(adj[i].begin(), adj[i].end()); 

    // Printing Kth node for each node. 
    for (int i = 0; i < n; i++) 
    { 
        if (adj[i].size() >= k) 
          cout << adj[i][adj[i].size() - k].second; 
        else
          cout << "-1"; 
    } 
} 

// Driven Program 
int main() 
{ 
    int n = 3, k = 2; 
    int wt[] = { 2, 4, 3 }; 

    // Making adjacency list, storing the nodes 
    // along with their weight. 
    vector< pair<int, int> > adj[n+1]; 

    adj[0].push_back(make_pair(wt[2], 2)); 
    adj[2].push_back(make_pair(wt[0], 0)); 

    adj[0].push_back(make_pair(wt[1], 1)); 
    adj[1].push_back(make_pair(wt[0], 0)); 

    adj[1].push_back(make_pair(wt[2], 2)); 
    adj[2].push_back(make_pair(wt[1], 1)); 

    printkthnode(adj, wt, n, k); 
    return 0; 
} 

```