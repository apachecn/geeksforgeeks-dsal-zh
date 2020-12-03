# 有向图和无向图中的三角形数

> 原文： [https://www.geeksforgeeks.org/number-of-triangles-in-directed-and-undirected-graphs/](https://www.geeksforgeeks.org/number-of-triangles-in-directed-and-undirected-graphs/)

给定一个图，计算其中的三角形数量。 该图可以是有向的或无向的。

例：

```
Input: digraph[V][V] = { {0, 0, 1, 0},
                        {1, 0, 0, 1},
                        {0, 1, 0, 0},
                        {0, 0, 1, 0}
                      };
Output: 2
Give adjacency matrix represents following 
directed graph.
![triangles](img/b34d8cd670f735e83849b6c97fd21af4.png)

```

我们已经讨论了基于图跟踪的[方法，该方法适用于无向图。 在本文中，我们讨论了一种新方法，该方法更简单，并且适用于有向图和无向图。](https://www.geeksforgeeks.org/number-of-triangles-in-a-undirected-graph/)

这个想法是使用三个嵌套循环来考虑每个三元组（i，j，k）并检查上述条件（从 i 到 j，从 j 到 k 到从 k 到 i 到 k 的边）

HTG1]无向图，可以将三元组（i，j，k）置换为六个组合（有关详细信息，请参见[先前的文章](https://www.geeksforgeeks.org/number-of-triangles-in-a-undirected-graph/)）。 因此，我们将总数除以 6 得到三角形的实际数量。

在**有向图**的情况下，排列数将为 3（随着节点的顺序变得相关）。 因此，在这种情况下，三角形的总数将通过将总数除以 3 得到。例如，考虑下面给出的有向图

以下是实现。

## C / C++

```

// C++ program to count triangles 
// in a graph. The program is for 
// adjacency matrix representation 
// of the graph. 
#include<bits/stdc++.h> 

// Number of vertices in the graph 
#define V 4 

using namespace std; 

// function to calculate the 
// number of triangles in a 
// simple directed/undirected  
// graph. isDirected is true if 
// the graph is directed, its 
// false otherwise 
int countTriangle(int graph[V][V],  
                  bool isDirected) 
{ 
    // Initialize result 
    int count_Triangle = 0; 

    // Consider every possible 
    // triplet of edges in graph 
    for (int i = 0; i < V; i++) 
    { 
        for (int j = 0; j < V; j++) 
        { 
            for (int k = 0; k < V; k++) 
            { 
               // check the triplet if 
               // it satisfies the condition 
               if (graph[i][j] && graph[j][k]  
                               && graph[k][i]) 
                  count_Triangle++; 
             } 
        } 
    } 

    // if graph is directed ,  
    // division is done by 3, 
    // else division by 6 is done 
    isDirected? count_Triangle /= 3 : 
                count_Triangle /= 6; 

    return count_Triangle; 
} 

//driver function to check the program 
int main() 
{ 
    // Create adjacency matrix 
    // of an undirected graph 
    int graph[][V] = { {0, 1, 1, 0}, 
                       {1, 0, 1, 1}, 
                       {1, 1, 0, 1}, 
                       {0, 1, 1, 0} 
                     }; 

    // Create adjacency matrix 
    // of a directed graph 
    int digraph[][V] = { {0, 0, 1, 0}, 
                        {1, 0, 0, 1}, 
                        {0, 1, 0, 0}, 
                        {0, 0, 1, 0} 
                       }; 

    cout << "The Number of triangles in undirected graph : "
         << countTriangle(graph, false); 
    cout << "\n\nThe Number of triangles in directed graph : "
         << countTriangle(digraph, true); 

    return 0; 
} 

```