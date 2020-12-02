# 源节点中树中每个节点的级别（使用 BFS）

> 原文： [https://www.geeksforgeeks.org/level-node-tree-source-node-using-bfs/](https://www.geeksforgeeks.org/level-node-tree-source-node-using-bfs/)

给定具有 v 个顶点的树，请从源节点中找到树中每个节点的级别。

**示例**：

```
Input :   

Output :  Node      Level
           0          0
           1          1
           2          1
           3          2
           4          2
           5          2
           6          2
           7          3

Explanation : 

Input:

Output :  Node      Level
           0          0
           1          1
           2          1
           3          2
           4          2
Explanation:

```

**方法**：
[BFS（广度优先搜索）](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)是一种图遍历技术，其中先访问节点及其邻居，然后再访问邻居。 简而言之，它从源头水平遍历。 首先，它遍历 1 级节点（源节点的直接邻居），然后遍历 2 级节点（源节点的邻居），依此类推。 BFS 可用于确定给定源节点中每个节点的级别。

**算法**：

1.  创建树，一个队列以存储节点并将根节点或起始节点插入队列。 创建一个额外的数组*级别*，其大小为 v（顶点数），并创建一个访问数组。
2.  在队列大小大于 0 时运行循环。
3.  将当前节点标记为已访问。
4.  从队列中弹出一个节点，并插入其子节点（如果存在），并将插入的节点的大小更新为 *level [child] = level [node] + 1* 。
5.  打印所有节点及其级别。

**实施**：

## C++

```cpp

// CPP Program to determine level of each node 
// and print level 
#include <bits/stdc++.h> 
using namespace std; 

// function to determine level of each node starting 
// from x using BFS 
void printLevels(vector<int> graph[], int V, int x) 
{ 
    // array to store level of each node 
    int level[V]; 
    bool marked[V]; 

    // create a queue 
    queue<int> que; 

    // enqueue element x 
    que.push(x); 

    // initialize level of source node to 0 
    level[x] = 0; 

    // marked it as visited 
    marked[x] = true; 

    // do until queue is empty 
    while (!que.empty()) { 

        // get the first element of queue 
        x = que.front(); 

        // dequeue element 
        que.pop(); 

        // traverse neighbors of node x 
        for (int i = 0; i < graph[x].size(); i++) { 
            // b is neighbor of node x 
            int b = graph[x][i]; 

            // if b is not marked already 
            if (!marked[b]) { 

                // enqueue b in queue 
                que.push(b); 

                // level of b is level of x + 1 
                level[b] = level[x] + 1; 

                // mark b 
                marked[b] = true; 
            } 
        } 
    } 

    // display all nodes and their levels 
    cout << "Nodes"
         << "    "
         << "Level" << endl; 
    for (int i = 0; i < V; i++) 
        cout << " " << i << "   -->   " << level[i] << endl; 
} 

// Driver Code 
int main() 
{ 
    // adjacency graph for tree 
    int V = 8; 
    vector<int> graph[V]; 

    graph[0].push_back(1); 
    graph[0].push_back(2); 
    graph[1].push_back(3); 
    graph[1].push_back(4); 
    graph[1].push_back(5); 
    graph[2].push_back(5); 
    graph[2].push_back(6); 
    graph[6].push_back(7); 

    // call levels function with source as 0 
    printLevels(graph, V, 0); 

    return 0; 
} 

```