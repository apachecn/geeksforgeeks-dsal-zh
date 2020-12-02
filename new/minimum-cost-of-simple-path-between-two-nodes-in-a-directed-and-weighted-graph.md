# 有向图和加权图

中两个节点之间的简单路径的最低成本

> 原文： [https://www.geeksforgeeks.org/minimum-cost-of-simple-path-between-two-nodes-in-a-directed-and-weighted-graph/](https://www.geeksforgeeks.org/minimum-cost-of-simple-path-between-two-nodes-in-a-directed-and-weighted-graph/)

给定**有向图**，其中可能包含循环，其中**每个边的权重**，任务是找到从给定源顶点到顶点的任何简单路径的最小代价 给定目标顶点“ t”。 简单路径是从一个顶点到另一个顶点的路径，这样就不会多次访问一个顶点。 如果没有简单的路径，则返回 INF（infinite）。

该图以[邻接矩阵表示形式](https://www.geeksforgeeks.org/graph-and-its-representations/)给出，其中图[i] [j]的值指示从顶点 i 到顶点 j 的边的权重，值 INF（infinite）指示从 i 到 j 的边没有权重 。

**示例：**

```
Input : V = 5, E = 6
        s = 0, t = 2
    graph[][] =      0   1   2   3   4  
                 0  INF -1  INF  1  INF
                 1  INF INF -2  INF INF
                 2  -3  INF INF INF INF
                 3  INF INF -1  INF INF
                 4  INF INF INF  2  INF

Output : -3 
Explanation : 
The minimum cost simple path between 0 and 2 is given by:
0 -----> 1 ------> 2 whose cost is (-1) + (-2) = (-3). 

Input : V = 5, E = 6
        s = 0, t = 4
    graph[][] =      0   1   2   3   4  
                 0  INF -7  INF -2  INF
                 1  INF INF -11 INF INF
                 2  INF INF INF INF INF
                 3  INF INF INF  3  -4
                 4  INF INF INF INF INF

Output : -6
Explanation : 
The minimum cost simple path between 0 and 2 is given by:
0 -----> 3 ------> 4 whose cost is (-2) + (-4) = (-6). 

```

**方法：**
解决上述问题的主要思路是，使用**深度优先搜索**的修改版本遍历从 s 到 t 的所有简单路径，并找到最小成本路径 其中。 关于 DFS 的一个重要发现是，它一次遍历一条路径，因此我们可以通过在离开节点之前将节点标记为未访问来使用 DFS 独立遍历单独的路径。
一个简单的解决方案是从 s 开始，转到所有相邻的顶点，然后对其他相邻的顶点进行递归操作，直到到达目的地。 即使图形中存在负权重周期或自身边缘，该算法也将起作用。

下面是上述方法的实现：

## C ++

```

// C++ code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph
#include <bits/stdc++.h>
using namespace std;

// Define number of vertices in
// the graph and infinite value
#define V 5
#define INF INT_MAX

// Function to do DFS through the nodes
int minimumCostSimplePath(int u, int destination,
                    bool visited[], int graph[][V])
{

    // check if we find the destination
    // then further cost will be 0
    if (u == destination)
        return 0;

    // marking the current node as visited
    visited[u] = 1;

    int ans = INF;

    // traverse through all
    // the adjacent nodes
    for (int i = 0; i < V; i++) {
        if (graph[u][i] != INF && !visited[i]) {

            // cost of the further path
            int curr = minimumCostSimplePath(i,
                        destination, visited, graph);

            // check if we have reached the destination
            if (curr < INF) {

                // Taking the minimum cost path
                ans = min(ans, graph[u][i] + curr);
            }
        }
    }

    // unmarking the current node
    // to make it available for other
    // simple paths
    visited[u] = 0;

    // returning the minimum cost
    return ans;
}

// driver code
int main()
{

    // initialising the graph
    int graph[V][V];
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            graph[i][j] = INF;
        }
    }

    // marking all nodes as unvisited
    bool visited[V] = { 0 };

    // initialising the edges;
    graph[0][1] = -1;
    graph[0][3] = 1;
    graph[1][2] = -2;
    graph[2][0] = -3;
    graph[3][2] = -1;
    graph[4][3] = 2;

    // source and destination
    int s = 0, t = 2;

    // marking the source as visited
    visited[s] = 1;

    cout << minimumCostSimplePath(s, t, 
                            visited, graph);

    return 0;
}

```

## 爪哇

```

// Java code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph
import java.util.*;
import java.lang.*;

class GFG{

// Define number of vertices in
// the graph and infinite value
static int V = 5;
static int INF = Integer.MAX_VALUE;

// Function to do DFS through the nodes
static int minimumCostSimplePath(int u, int destination,
                                 boolean visited[], 
                                 int graph[][])
{

    // Check if we find the destination
    // then further cost will be 0
    if (u == destination)
        return 0;

    // Marking the current node as visited
    visited[u] = true;

    int ans = INF;

    // Traverse through all
    // the adjacent nodes
    for(int i = 0; i < V; i++) 
    {
        if (graph[u][i] != INF && !visited[i])
        {

            // Cost of the further path
            int curr = minimumCostSimplePath(i,
                        destination, visited, graph);

            // Check if we have reached the
            // destination
            if (curr < INF)
            {

                // Taking the minimum cost path
                ans = Math.min(ans, graph[u][i] + curr);
            }
        }
    }

    // Unmarking the current node
    // to make it available for other
    // simple paths
    visited[u] = false;

    // Returning the minimum cost
    return ans;
}   

// Driver code
public static void main(String[] args)
{

    // Initialising the graph
    int graph[][] = new int[V][V];
    for(int i = 0; i < V; i++)
    {
        for(int j = 0; j < V; j++) 
        {
            graph[i][j] = INF;
        }
    }

    // Marking all nodes as unvisited
    boolean visited[] = new boolean[V];

    // Initialising the edges;
    graph[0][1] = -1;
    graph[0][3] = 1;
    graph[1][2] = -2;
    graph[2][0] = -3;
    graph[3][2] = -1;
    graph[4][3] = 2;

    // Source and destination
    int s = 0, t = 2;

    // Marking the source as visited
    visited[s] = true;

    System.out.println(minimumCostSimplePath(s, t, 
                            visited, graph));
}
}

// This code is contributed by offbeat

```

## Python3

```

# Python3 code for printing Minimum Cost
# Simple Path between two given nodes
# in a directed and weighted graph
import sys

V = 5
INF = sys.maxsize

# Function to do DFS through the nodes
def minimumCostSimplePath(u, destination, 
                          visited, graph):

    # Check if we find the destination
    # then further cost will be 0
    if (u == destination):
        return 0

    # Marking the current node as visited
    visited[u] = 1

    ans = INF

    # Traverse through all
    # the adjacent nodes
    for i in range(V):
        if (graph[u][i] != INF and not visited[i]):

            # Cost of the further path
            curr = minimumCostSimplePath(i, destination, 
                                         visited, graph)

            # Check if we have reached the destination
            if (curr < INF):

                # Taking the minimum cost path
                ans = min(ans, graph[u][i] + curr)

    # Unmarking the current node
    # to make it available for other
    # simple paths
    visited[u] = 0

    # Returning the minimum cost
    return ans

# Driver code
if __name__=="__main__":

    # Initialising the graph
    graph = [[INF for j in range(V)]
                  for i in range(V)]

    # Marking all nodes as unvisited
    visited = [0 for i in range(V)]

    # Initialising the edges
    graph[0][1] = -1
    graph[0][3] = 1
    graph[1][2] = -2
    graph[2][0] = -3
    graph[3][2] = -1
    graph[4][3] = 2

    # Source and destination
    s = 0
    t = 2

    # Marking the source as visited
    visited[s] = 1

    print(minimumCostSimplePath(s, t, visited, graph))

# This code is contributed by rutvik_56

```

**Output:** 

```
-3

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。