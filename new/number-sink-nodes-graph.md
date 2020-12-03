# 图形

中的接收器节点数

> 原文： [https://www.geeksforgeeks.org/number-sink-nodes-graph/](https://www.geeksforgeeks.org/number-sink-nodes-graph/)

给定`n`个节点（编号从 1 到 n）和 **m 个**边的有向无环图。 任务是找到宿节点的数量。 宿节点是这样的节点，即没有边出现在该节点之外。

**示例**：

```
Input : n = 4, m = 2
        Edges[] = {{2, 3}, {4, 3}} 
Output : 2

Only node 1 and node 3 are sink nodes.

Input : n = 4, m = 2
        Edges[] = {{3, 2}, {3, 4}} 
Output : 3

```

这个想法是遍历所有边。 并为每个边标记从中出现边的源节点。 现在，对于每个节点，检查是否已标记。 并计算未标记的节点。

算法：

```

1\. Make any array A[] of size equal to the
    number of nodes and initialize to 1.
2\. Traverse all the edges one by one, say, 
   u -> v.
     (i) Mark A[u] as 1.
3\. Now traverse whole array A[] and count 
   number of unmarked nodes.
```

以下是此方法的实现：

## C++

```cpp

// C++ program to count number if sink nodes 
#include<bits/stdc++.h> 
using namespace std; 

// Return the number of Sink NOdes. 
int countSink(int n, int m, int edgeFrom[], 
                        int edgeTo[]) 
{ 
    // Array for marking the non-sink node. 
    int mark[n]; 
    memset(mark, 0, sizeof mark); 

    // Marking the non-sink node. 
    for (int i = 0; i < m; i++) 
        mark[edgeFrom[i]] = 1; 

    // Counting the sink nodes. 
    int count = 0; 
    for (int i = 1; i <= n ; i++) 
        if (!mark[i]) 
            count++; 

    return count; 
} 

// Driven Program 
int main() 
{ 
    int n = 4, m = 2; 
    int edgeFrom[] = { 2, 4 }; 
    int edgeTo[] = { 3, 3 }; 

    cout << countSink(n, m, edgeFrom, edgeTo) << endl; 

    return 0; 
} 

```