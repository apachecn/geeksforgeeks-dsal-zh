# 哈密顿周期| 回溯 6

> 原文： [https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/](https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/)

[无向图中的汉密尔顿路径](http://en.wikipedia.org/wiki/Hamiltonian_path)是只访问每个顶点一次的路径。 哈密​​顿循环（或哈密顿回路）是哈密顿路径，因此从哈密顿路径的最后一个顶点到第一个顶点有一条边（在图中）。 确定给定图是否包含哈密顿循环。 如果包含，则打印路径。 以下是所需功能的输入和输出。

*输入：*

2D 数组图形[V] [V]，其中 V 是图形中的顶点数，而 graph [V] [V]是图形的邻接矩阵表示。 如果存在从 i 到 j 的直接边，则值 graph [i] [j]为 1，否则 graph [i] [j]为 0。

*输出：*

应该包含哈密顿路径的数组路径[V]。 path [i]应该表示哈密顿路径中的第 i 个顶点。 如果图中没有汉密尔顿循环，则代码也应返回 false。

例如，下图中的哈密顿循环为{0，1，2，4，4，3，0}。

```
(0)--(1)--(2)
 |   / \   |
 |  /   \  | 
 | /     \ |
(3)-------(4)

```

而且下图不包含任何哈密顿循环。

```
(0)--(1)--(2)
 |   / \   |
 |  /   \  | 
 | /     \ |
(3)      (4) 

```

**天真的算法**

生成所有可能的顶点配置，并打印满足给定约束的配置。 会有 n！ （n 个阶乘）配置。

```
while there are untried conflagrations
{
   generate the next configuration
   if ( there are edges between two consecutive vertices of this
      configuration and there is an edge from the last vertex to 
      the first ).
   {
      print this configuration;
      break;
   }
}

```

**回溯算法**

创建一个空路径数组并将顶点 0 添加到其中。 从顶点开始添加其他顶点。1.添加顶点之前，检查它是否与先前添加的顶点相邻并且尚未添加。 如果找到这样的顶点，则将其添加为解决方案的一部分。 如果找不到顶点，则返回 false。

**回溯解决方案的实现**

以下是回溯解决方案的实现。

## C++

```cpp

/* C++ program for solution of Hamiltonian  
Cycle problem using backtracking */
#include <bits/stdc++.h> 
using namespace std; 

// Number of vertices in the graph  
#define V 5  

void printSolution(int path[]);  

/* A utility function to check if  
the vertex v can be added at index 'pos'  
in the Hamiltonian Cycle constructed  
so far (stored in 'path[]') */
bool isSafe(int v, bool graph[V][V],  
            int path[], int pos)  
{  
    /* Check if this vertex is an adjacent  
    vertex of the previously added vertex. */
    if (graph [path[pos - 1]][ v ] == 0)  
        return false;  

    /* Check if the vertex has already been included.  
    This step can be optimized by creating 
    an array of size V */
    for (int i = 0; i < pos; i++)  
        if (path[i] == v)  
            return false;  

    return true;  
}  

/* A recursive utility function  
to solve hamiltonian cycle problem */
bool hamCycleUtil(bool graph[V][V],  
                  int path[], int pos)  
{  
    /* base case: If all vertices are  
    included in Hamiltonian Cycle */
    if (pos == V)  
    {  
        // And if there is an edge from the  
        // last included vertex to the first vertex  
        if (graph[path[pos - 1]][path[0]] == 1)  
            return true;  
        else
            return false;  
    }  

    // Try different vertices as a next candidate  
    // in Hamiltonian Cycle. We don't try for 0 as  
    // we included 0 as starting point in hamCycle()  
    for (int v = 1; v < V; v++)  
    {  
        /* Check if this vertex can be added  
        // to Hamiltonian Cycle */
        if (isSafe(v, graph, path, pos))  
        {  
            path[pos] = v;  

            /* recur to construct rest of the path */
            if (hamCycleUtil (graph, path, pos + 1) == true)  
                return true;  

            /* If adding vertex v doesn't lead to a solution,  
            then remove it */
            path[pos] = -1;  
        }  
    }  

    /* If no vertex can be added to  
    Hamiltonian Cycle constructed so far,  
    then return false */
    return false;  
}  

/* This function solves the Hamiltonian Cycle problem  
using Backtracking. It mainly uses hamCycleUtil() to  
solve the problem. It returns false if there is no  
Hamiltonian Cycle possible, otherwise return true  
and prints the path. Please note that there may be  
more than one solutions, this function prints one  
of the feasible solutions. */
bool hamCycle(bool graph[V][V])  
{  
    int *path = new int[V];  
    for (int i = 0; i < V; i++)  
        path[i] = -1;  

    /* Let us put vertex 0 as the first vertex in the path. 
    If there is a Hamiltonian Cycle, then the path can be  
    started from any point of the cycle as the graph is undirected */
    path[0] = 0;  
    if (hamCycleUtil(graph, path, 1) == false )  
    {  
        cout << "\nSolution does not exist";  
        return false;  
    }  

    printSolution(path);  
    return true;  
}  

/* A utility function to print solution */
void printSolution(int path[])  
{  
    cout << "Solution Exists:"
            " Following is one Hamiltonian Cycle \n";  
    for (int i = 0; i < V; i++)  
        cout << path[i] << " ";  

    // Let us print the first vertex again 
    // to show the complete cycle  
    cout << path[0] << " ";  
    cout << endl; 
}  

// Driver Code  
int main()  
{  
    /* Let us create the following graph  
        (0)--(1)--(2)  
        | / \ |  
        | / \ |  
        | / \ |  
        (3)-------(4) */
    bool graph1[V][V] = {{0, 1, 0, 1, 0},  
                        {1, 0, 1, 1, 1},  
                        {0, 1, 0, 0, 1},  
                        {1, 1, 0, 0, 1},  
                        {0, 1, 1, 1, 0}};  

    // Print the solution  
    hamCycle(graph1);  

    /* Let us create the following graph  
    (0)--(1)--(2)  
    | / \ |  
    | / \ |  
    | / \ |  
    (3) (4) */
    bool graph2[V][V] = {{0, 1, 0, 1, 0},  
                         {1, 0, 1, 1, 1},  
                         {0, 1, 0, 0, 1},  
                         {1, 1, 0, 0, 0},  
                         {0, 1, 1, 0, 0}};  

    // Print the solution  
    hamCycle(graph2);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```