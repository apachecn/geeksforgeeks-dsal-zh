# Floyd Warshall 算法| DP-16

> 原文： [https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)

[Floyd Warshall 算法](http://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)用于解决全对最短路径问题。 问题是在给定的边缘加权有向图中找到每对顶点之间的最短距离。

**示例**：

```
Input:
       graph[][] = { {0,   5,  INF, 10},
                    {INF,  0,  3,  INF},
                    {INF, INF, 0,   1},
                    {INF, INF, INF, 0} }
which represents the following graph
             10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3       
Note that the value of graph[i][j] is 0 if i is equal to j 
And graph[i][j] is INF (infinite) if there is no edge from vertex i to j.

Output:
Shortest distance matrix
      0      5      8      9
    INF      0      3      4
    INF    INF      0      1
    INF    INF    INF      0 

```

**Floyd Warshall 算法**
第一步，我们初始化与输入图矩阵相同的解矩阵。 然后，我们通过将所有顶点视为中间顶点来更新解矩阵。 这个想法是一个接一个地拾取所有顶点并更新所有最短路径，其中包括将所拾取的顶点作为最短路径中的中间顶点。 当我们选择顶点数 k 作为中间顶点时，我们已经将顶点{0，1，2，.. k-1}视为中间顶点。 对于源顶点和目标顶点的每对（i，j），都有两种可能的情况。
**1）** k 在从 i 到 j 的最短路径中不是中间顶点。 我们将 dist [i] [j]的值保持不变。
**2）** k 是从 i 到 j 的最短路径中的中间顶点。 如果 dist [i] [j] > dist [i] [k] + dist [k ] [j]

下图显示了所有对最短路径问题中的上述最佳子结构属性。

[![](img/957485506abad8275ceb037ee2a55849.png "Floyd Warshell")](https://media.geeksforgeeks.org/wp-content/uploads/dpFloyd-Warshall-.jpg)

以下是 Floyd Warshall 算法的实现。

## C ++

```

// C++ Program for Floyd Warshall Algorithm  
#include <bits/stdc++.h> 
using namespace std; 

// Number of vertices in the graph  
#define V 4  

/* Define Infinite as a large enough 
value.This value will be used for  
vertices not connected to each other */
#define INF 99999  

// A function to print the solution matrix  
void printSolution(int dist[][V]);  

// Solves the all-pairs shortest path  
// problem using Floyd Warshall algorithm  
void floydWarshall (int graph[][V])  
{  
    /* dist[][] will be the output matrix  
    that will finally have the shortest  
    distances between every pair of vertices */
    int dist[V][V], i, j, k;  

    /* Initialize the solution matrix same  
    as input graph matrix. Or we can say  
    the initial values of shortest distances 
    are based on shortest paths considering  
    no intermediate vertex. */
    for (i = 0; i < V; i++)  
        for (j = 0; j < V; j++)  
            dist[i][j] = graph[i][j];  

    /* Add all vertices one by one to  
    the set of intermediate vertices.  
    ---> Before start of an iteration,  
    we have shortest distances between all  
    pairs of vertices such that the  
    shortest distances consider only the  
    vertices in set {0, 1, 2, .. k-1} as 
    intermediate vertices.  
    ----> After the end of an iteration,  
    vertex no. k is added to the set of  
    intermediate vertices and the set becomes {0, 1, 2, .. k} */
    for (k = 0; k < V; k++)  
    {  
        // Pick all vertices as source one by one  
        for (i = 0; i < V; i++)  
        {  
            // Pick all vertices as destination for the  
            // above picked source  
            for (j = 0; j < V; j++)  
            {  
                // If vertex k is on the shortest path from  
                // i to j, then update the value of dist[i][j]  
                if (dist[i][k] + dist[k][j] < dist[i][j])  
                    dist[i][j] = dist[i][k] + dist[k][j];  
            }  
        }  
    }  

    // Print the shortest distance matrix  
    printSolution(dist);  
}  

/* A utility function to print solution */
void printSolution(int dist[][V])  
{  
    cout<<"The following matrix shows the shortest distances"
            " between every pair of vertices \n";  
    for (int i = 0; i < V; i++)  
    {  
        for (int j = 0; j < V; j++)  
        {  
            if (dist[i][j] == INF)  
                cout<<"INF"<<"     ";  
            else
                cout<<dist[i][j]<<"     ";  
        }  
        cout<<endl;  
    }  
}  

// Driver code  
int main()  
{  
    /* Let us create the following weighted graph  
            10  
    (0)------->(3)  
        |     /|\  
    5 |     |  
        |     | 1  
    \|/     |  
    (1)------->(2)  
            3     */
    int graph[V][V] = { {0, 5, INF, 10},  
                        {INF, 0, 3, INF},  
                        {INF, INF, 0, 1},  
                        {INF, INF, INF, 0}  
                    };  

    // Print the solution  
    floydWarshall(graph);  
    return 0;  
}  

// This code is contributed by rathbhupendra 

```