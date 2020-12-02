# Kruskal 算法（邻接矩阵的简单实现）

> 原文： [https://www.geeksforgeeks.org/kruskals-algorithm-simple-implementation-for-adjacency-matrix/](https://www.geeksforgeeks.org/kruskals-algorithm-simple-implementation-for-adjacency-matrix/)

以下是使用 [Kruskal 算法](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)查找 MST 的步骤

> **1\.** 对所有边缘按其权重的非降序排序。
> **2\.** 选取最小的边缘。 检查它是否与形成的生成树形成一个循环。 如果未形成循环，则包括该边。 否则，将其丢弃。
> **3\.** 重复步骤 2，直到生成树中有（V-1）个边。

我们在[先前的文章](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)中讨论了 Kruskal 算法的一种实现。 在这篇文章中，讨论了邻接矩阵的一种更简单的实现。

## C ++

```

// Simple C++ implementation for Kruskal's 
// algorithm 
#include <bits/stdc++.h> 
using namespace std; 

#define V 5 
int parent[V]; 

// Find set of vertex i 
int find(int i) 
{ 
    while (parent[i] != i) 
        i = parent[i]; 
    return i; 
} 

// Does union of i and j. It returns 
// false if i and j are already in same 
// set. 
void union1(int i, int j) 
{ 
    int a = find(i); 
    int b = find(j); 
    parent[a] = b; 
} 

// Finds MST using Kruskal's algorithm 
void kruskalMST(int cost[][V]) 
{ 
    int mincost = 0; // Cost of min MST. 

    // Initialize sets of disjoint sets. 
    for (int i = 0; i < V; i++) 
        parent[i] = i; 

    // Include minimum weight edges one by one 
    int edge_count = 0; 
    while (edge_count < V - 1) { 
        int min = INT_MAX, a = -1, b = -1; 
        for (int i = 0; i < V; i++) { 
            for (int j = 0; j < V; j++) { 
                if (find(i) != find(j) && cost[i][j] < min) { 
                    min = cost[i][j]; 
                    a = i; 
                    b = j; 
                } 
            } 
        } 

        union1(a, b); 
        printf("Edge %d:(%d, %d) cost:%d \n", 
               edge_count++, a, b, min); 
        mincost += min; 
    } 
    printf("\n Minimum cost= %d \n", mincost); 
} 

// driver program to test above function 
int main() 
{ 
    /* Let us create the following graph 
          2    3 
      (0)--(1)--(2) 
       |   / \   | 
      6| 8/   \5 |7 
       | /     \ | 
      (3)-------(4) 
            9          */
    int cost[][V] = { 
        { INT_MAX, 2, INT_MAX, 6, INT_MAX }, 
        { 2, INT_MAX, 3, 8, 5 }, 
        { INT_MAX, 3, INT_MAX, INT_MAX, 7 }, 
        { 6, 8, INT_MAX, INT_MAX, 9 }, 
        { INT_MAX, 5, 7, 9, INT_MAX }, 
    }; 

    // Print the solution 
    kruskalMST(cost); 

    return 0; 
} 

```