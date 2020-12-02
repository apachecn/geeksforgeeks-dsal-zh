# 计数断开连接图中的单节点隔离子图

> 原文： [https://www.geeksforgeeks.org/count-single-node-isolated-sub-graphs-disconnected-graph/](https://www.geeksforgeeks.org/count-single-node-isolated-sub-graphs-disconnected-graph/)

给出了具有 N 个顶点和 K 个边的不连续图。 任务是找到单例子图的计数。 单例图是只有一个顶点的图。

**示例**：

```
Input : 
Vertices : 6
Edges :    1 2
           1 3
           5 6
Output : 1
Explanation :  The Graph has 3 components : {1-2-3}, {5-6}, {4}
Out of these, the only component forming singleton graph is {4}.

```

对于以邻接表表示形式给出的图，这个想法很简单。 我们遍历列表并找到列表中没有元素的索引（代表节点），即没有连接的组件。

下面是表示形式：

## C++

```cpp

// CPP code to count the singleton sub-graphs 
// in a disconnected graph 
#include <bits/stdc++.h> 
using namespace std; 

// Function to compute the count 
int compute(vector<int> graph[], int N) 
{ 
    // Storing intermediate result 
    int count = 0; 

    // Traversing the Nodes 
    for (int i = 1; i <= N; i++) 

        // Singleton component 
        if (graph[i].size() == 0) 
            count++;     

    // Returning the result 
    return count; 
} 

// Driver 
int main() 
{ 
    // Number of nodes 
    int N = 6; 

    // Adjacency list for edges 1..6 
    vector<int> graph[7]; 

    // Representing edges 
    graph[1].push_back(2); 
    graph[2].push_back(1); 

    graph[2].push_back(3); 
    graph[3].push_back(2); 

    graph[5].push_back(6); 
    graph[6].push_back(5); 

    cout << compute(graph, N); 
} 

```