# m 着色问题| 回溯 5

> 原文： [https://www.geeksforgeeks.org/m-coloring-problem-backtracking-5/](https://www.geeksforgeeks.org/m-coloring-problem-backtracking-5/)

给定一个无向图和一个数字 m，请确定该图是否最多可以用 m 种颜色着色，以使该图的两个相邻顶点都不用相同颜色着色。 在此，图形着色是指将颜色分配给所有顶点。
**输入输出格式**：，
***输入**：*

1.  二维数组 graph [V] [V]，其中 V 是图形中的顶点数，而 graph [V] [V]是图形的邻接矩阵表示。 如果存在从 i 到 j 的直接边，则值 graph [i] [j]为 1，否则 graph [i] [j]为 0。
2.  整数 m，它是可以使用的最大颜色数。

***输出**：*
数组 color [V]，其数字应为 1 到 m。 color [i]应该表示分配给第 i 个顶点的颜色。 如果图形不能用 m 种颜色上色，则代码也应返回 false。
**范例**：

```
Input:  
graph = {0, 1, 1, 1},
        {1, 0, 1, 0},
        {1, 1, 0, 1},
        {1, 0, 1, 0}
Output: 
Solution Exists: 
Following are the assigned colors
 1  2  3  2
Explanation: By coloring the vertices 
with following colors, adjacent 
vertices does not have same colors

Input: 
graph = {1, 1, 1, 1},
        {1, 1, 1, 1},
        {1, 1, 1, 1},
        {1, 1, 1, 1}
Output: Solution does not exist.
Explanation: No solution exits.

```

**以下是可以用 3 种不同颜色进行着色的图形示例。**

![](img/ff3960e2e77ef87837017b95370c5f77.png)

## [我们强烈建议您单击此处并进行实践，然后再继续解决方案。](https://practice.geeksforgeeks.org/problem-page.php?pid=635)

**<u>方法 1：</u>** 天真。
**天真方法**：生成所有可能的颜色配置。 由于每个节点都可以使用 m 种可用颜色中的任何一种进行着色，因此可能的颜色配置总数为 m ^ V。
生成颜色配置后，检查相邻的顶点是否具有相同的颜色。 如果满足条件，请打印组合并中断循环。
**算法**：

1.  创建一个使用当前索引，顶点数和输出颜色数组的递归函数。
2.  如果当前索引等于顶点数。 检查输出颜色配置是否安全，即检查相邻顶点是否没有相同颜色。 如果满足条件，请打印配置并中断。
3.  将颜色分配给一个顶点（1 到 m）。
4.  对于每种分配的颜色，以下一个索引和顶点数递归调用函数
5.  如果任何递归函数返回 true，则中断循环并返回 true。

## CPP14

```

#include <stdbool.h>
#include <stdio.h>

// Number of vertices in the graph
#define V 4

void printSolution(int color[]);

// check if the colored
// graph is safe or not
bool isSafe(bool graph[V][V], int color[])
{
    // check for every edge
    for (int i = 0; i < V; i++)
        for (int j = i + 1; j < V; j++)
            if (graph[i][j] && color[j] == color[i])
                return false;
    return true;
}

/* This function solves the m Coloring
   problem using recursion. It returns
  false if the m colours cannot be assigned,
  otherwise, return true and prints
  assignments of colours to all vertices.
  Please note that there may be more than
  one solutions, this function prints one
  of the feasible solutions.*/
bool graphColoring(bool graph[V][V], int m, int i,
                   int color[V])
{
    // if current index reached end
    if (i == V) {
        // if coloring is safe
        if (isSafe(graph, color)) {
            // Print the solution
            printSolution(color);
            return true;
        }
        return false;
    }

    // Assign each color from 1 to m
    for (int j = 1; j <= m; j++) {
        color[i] = j;

        // Recur of the rest vertices
        if (graphColoring(graph, m, i + 1, color))
            return true;

        color[i] = 0;
    }

    return false;
}

/* A utility function to print solution */
void printSolution(int color[])
{
    printf("Solution Exists:"
           " Following are the assigned colors \n");
    for (int i = 0; i < V; i++)
        printf(" %d ", color[i]);
    printf("\n");
}

// Driver program to test above function
int main()
{
    /* Create following graph and
       test whether it is 3 colorable
      (3)---(2)
       |   / |
       |  /  |
       | /   |
      (0)---(1)
    */
    bool graph[V][V] = {
        { 0, 1, 1, 1 },
        { 1, 0, 1, 0 },
        { 1, 1, 0, 1 },
        { 1, 0, 1, 0 },
    };
    int m = 3; // Number of colors

    // Initialize all color values as 0.
    // This initialization is needed
    // correct functioning of isSafe()
    int color[V];
    for (int i = 0; i < V; i++)
        color[i] = 0;

    if (!graphColoring(graph, m, 0, color))
        printf("Solution does not exist");

    return 0;
}

```

**Output:** 

```
Solution Exists: Following are the assigned colors 
 1  2  3  2

```

**复杂度分析**：

*   **时间复杂度**：O（m ^ V）。
    共有 O（m ^ V）种颜色组合。 因此，时间复杂度为 O（m ^ V）。
*   **空间复杂度**：O（V）。
    要存储输出数组，需要 O（V）空间。

**<u>方法 2</u> **：[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)。
**方法**：的想法是，从顶点 0 开始，将颜色逐一分配给不同的顶点。在分配颜色之前，请考虑是否已经为相邻的顶点分配了颜色，以检查安全性，即检查是否 相邻顶点的颜色相同或不同。 如果有任何不违反条件的颜色分配，请将颜色分配标记为解决方案的一部分。 如果无法进行颜色分配，则回溯并返回 false。
**算法**：

1.  创建一个使用图，当前索引，顶点数和输出颜色数组的递归函数。
2.  如果当前索引等于顶点数。 在输出数组中打印颜色配置。
3.  将颜色分配给一个顶点（1 到 m）。
4.  对于每种分配的颜色，请检查配置是否安全（即，检查相邻顶点是否具有相同的颜色）以下一个索引和顶点数递归调用该函数
5.  如果任何递归函数返回 true，则中断循环并返回 true。
6.  如果没有任何对策函数返回 true，则返回 false。

## C++

```cpp

#include <stdbool.h>
#include <stdio.h>

// Number of vertices in the graph
#define V 4

void printSolution(int color[]);

/* A utility function to check if 
   the current color assignment
   is safe for vertex v i.e. checks 
   whether the edge exists or not
   (i.e, graph[v][i]==1). If exist 
   then checks whether the color to 
   be filled in the new vertex(c is
   sent in the parameter) is already
   used by its adjacent 
   vertices(i-->adj vertices) or 
   not (i.e, color[i]==c) */
bool isSafe(
    int v, bool graph[V][V],
    int color[], int c)
{
    for (int i = 0; i < V; i++)
        if (
            graph[v][i] && c == color[i])
            return false;
    return true;
}

/* A recursive utility function 
to solve m coloring problem */
bool graphColoringUtil(
    bool graph[V][V], int m,
    int color[], int v)
{
    /* base case: If all vertices are 
       assigned a color then return true */
    if (v == V)
        return true;

    /* Consider this vertex v and 
       try different colors */
    for (int c = 1; c <= m; c++) {
        /* Check if assignment of color 
           c to v is fine*/
        if (isSafe(
                v, graph, color, c)) {
            color[v] = c;

            /* recur to assign colors to 
               rest of the vertices */
            if (
                graphColoringUtil(
                    graph, m, color, v + 1)
                == true)
                return true;

            /* If assigning color c doesn't
               lead to a solution then remove it */
            color[v] = 0;
        }
    }

    /* If no color can be assigned to 
       this vertex then return false */
    return false;
}

/* This function solves the m Coloring 
   problem using Backtracking. It mainly 
   uses graphColoringUtil() to solve the 
   problem. It returns false if the m 
   colors cannot be assigned, otherwise 
   return true and prints assignments of 
   colors to all vertices. Please note 
   that there may be more than one solutions,
   this function prints one of the
   feasible solutions.*/
bool graphColoring(
    bool graph[V][V], int m)
{
    // Initialize all color values as 0.
    // This initialization is needed
    // correct functioning of isSafe()
    int color[V];
    for (int i = 0; i < V; i++)
        color[i] = 0;

    // Call graphColoringUtil() for vertex 0
    if (
        graphColoringUtil(
            graph, m, color, 0)
        == false) {
        printf("Solution does not exist");
        return false;
    }

    // Print the solution
    printSolution(color);
    return true;
}

/* A utility function to print solution */
void printSolution(int color[])
{
    printf(
        "Solution Exists:"
        " Following are the assigned colors \n");
    for (int i = 0; i < V; i++)
        printf(" %d ", color[i]);
    printf("\n");
}

// driver program to test above function
int main()
{
    /* Create following graph and test 
       whether it is 3 colorable
      (3)---(2)
       |   / |
       |  /  |
       | /   |
      (0)---(1)
    */
    bool graph[V][V] = {
        { 0, 1, 1, 1 },
        { 1, 0, 1, 0 },
        { 1, 1, 0, 1 },
        { 1, 0, 1, 0 },
    };
    int m = 3; // Number of colors
    graphColoring(graph, m);
    return 0;
}

```

## Java

```java

/* Java program for solution of 
   M Coloring problem using backtracking */
public class mColoringProblem 
{
    final int V = 4;
    int color[];

    /* A utility function to check 
       if the current color assignment 
       is safe for vertex v */
    boolean isSafe(
        int v, int graph[][], int color[],
        int c)
    {
        for (int i = 0; i < V; i++)
            if (
                graph[v][i] == 1 && c == color[i])
                return false;
        return true;
    }

    /* A recursive utility function 
       to solve m coloring  problem */
    boolean graphColoringUtil(
        int graph[][], int m,
        int color[], int v)
    {
        /* base case: If all vertices are 
           assigned a color then return true */
        if (v == V)
            return true;

        /* Consider this vertex v and try 
           different colors */
        for (int c = 1; c <= m; c++) 
        {
            /* Check if assignment of color c to v
               is fine*/
            if (isSafe(v, graph, color, c))
            {
                color[v] = c;

                /* recur to assign colors to rest
                   of the vertices */
                if (
                    graphColoringUtil(
                        graph, m,
                        color, v + 1))
                    return true;

                /* If assigning color c doesn't lead
                   to a solution then remove it */
                color[v] = 0;
            }
        }

        /* If no color can be assigned to 
           this vertex then return false */
        return false;
    }

    /* This function solves the m Coloring problem using
       Backtracking. It mainly uses graphColoringUtil()
       to solve the problem. It returns false if the m
       colors cannot be assigned, otherwise return true
       and  prints assignments of colors to all vertices.
       Please note that there  may be more than one
       solutions, this function prints one of the
       feasible solutions.*/
    boolean graphColoring(int graph[][], int m)
    {
        // Initialize all color values as 0\. This
        // initialization is needed correct
        // functioning of isSafe()
        color = new int[V];
        for (int i = 0; i < V; i++)
            color[i] = 0;

        // Call graphColoringUtil() for vertex 0
        if (
            !graphColoringUtil(
                graph, m, color, 0)) 
        {
            System.out.println(
                "Solution does not exist");
            return false;
        }

        // Print the solution
        printSolution(color);
        return true;
    }

    /* A utility function to print solution */
    void printSolution(int color[])
    {
        System.out.println(
            "Solution Exists: Following"
            + " are the assigned colors");
        for (int i = 0; i < V; i++)
            System.out.print(" " + color[i] + " ");
        System.out.println();
    }

    // driver program to test above function
    public static void main(String args[])
    {
        mColoringProblem Coloring 
               = new mColoringProblem();
        /* Create following graph and 
           test whether it is
           3 colorable
          (3)---(2)
           |   / |
           |  /  |
           | /   |
          (0)---(1)
        */
        int graph[][] = {
            { 0, 1, 1, 1 },
            { 1, 0, 1, 0 },
            { 1, 1, 0, 1 },
            { 1, 0, 1, 0 },
        };
        int m = 3; // Number of colors
        Coloring.graphColoring(graph, m);
    }
}
// This code is contributed by Abhishek Shankhadhar

```

## Python

```py

# Python program for solution of M Coloring 
# problem using backtracking

class Graph():

    def __init__(self, vertices):
        self.V = vertices
        self.graph = [[0 for column in range(vertices)]\
                              for row in range(vertices)]

    # A utility function to check 
    # if the current color assignment
    # is safe for vertex v
    def isSafe(self, v, colour, c):
        for i in range(self.V):
            if self.graph[v][i] == 1 and colour[i] == c:
                return False
        return True

    # A recursive utility function to solve m
    # coloring  problem
    def graphColourUtil(self, m, colour, v):
        if v == self.V:
            return True

        for c in range(1, m + 1):
            if self.isSafe(v, colour, c) == True:
                colour[v] = c
                if self.graphColourUtil(m, colour, v + 1) == True:
                    return True
                colour[v] = 0

    def graphColouring(self, m):
        colour = [0] * self.V
        if self.graphColourUtil(m, colour, 0) == None:
            return False

        # Print the solution
        print "Solution exist and Following 
                  are the assigned colours:"
        for c in colour:
            print c,
        return True

# Driver Code
g = Graph(4)
g.graph = [[0, 1, 1, 1], [1, 0, 1, 0], [1, 1, 0, 1], [1, 0, 1, 0]]
m = 3
g.graphColouring(m)

# This code is contributed by Divyanshu Mehta

```

## C#

```cs

/* C# program for solution of M Coloring problem 
using backtracking */
using System;

class GFG {
    readonly int V = 4;
    int[] color;

    /* A utility function to check if the current 
    color assignment is safe for vertex v */
    bool isSafe(int v, int[, ] graph,
                int[] color, int c)
    {
        for (int i = 0; i < V; i++)
            if (graph[v, i] == 1 && c == color[i])
                return false;
        return true;
    }

    /* A recursive utility function to solve m 
    coloring problem */
    bool graphColoringUtil(int[, ] graph, int m,
                           int[] color, int v)
    {
        /* base case: If all vertices are assigned 
        a color then return true */
        if (v == V)
            return true;

        /* Consider this vertex v and try different 
        colors */
        for (int c = 1; c <= m; c++) {
            /* Check if assignment of color c to v 
            is fine*/
            if (isSafe(v, graph, color, c)) {
                color[v] = c;

                /* recur to assign colors to rest 
                of the vertices */
                if (graphColoringUtil(graph, m,
                                      color, v + 1))
                    return true;

                /* If assigning color c doesn't lead 
                to a solution then remove it */
                color[v] = 0;
            }
        }

        /* If no color can be assigned to this vertex 
        then return false */
        return false;
    }

    /* This function solves the m Coloring problem using 
    Backtracking. It mainly uses graphColoringUtil() 
    to solve the problem. It returns false if the m 
    colors cannot be assigned, otherwise return true 
    and prints assignments of colors to all vertices. 
    Please note that there may be more than one 
    solutions, this function prints one of the 
    feasible solutions.*/
    bool graphColoring(int[, ] graph, int m)
    {
        // Initialize all color values as 0\. This
        // initialization is needed correct functioning
        // of isSafe()
        color = new int[V];
        for (int i = 0; i < V; i++)
            color[i] = 0;

        // Call graphColoringUtil() for vertex 0
        if (!graphColoringUtil(graph, m, color, 0)) {
            Console.WriteLine("Solution does not exist");
            return false;
        }

        // Print the solution
        printSolution(color);
        return true;
    }

    /* A utility function to print solution */
    void printSolution(int[] color)
    {
        Console.WriteLine("Solution Exists: Following"
                          + " are the assigned colors");
        for (int i = 0; i < V; i++)
            Console.Write(" " + color[i] + " ");
        Console.WriteLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        GFG Coloring = new GFG();

        /* Create following graph and test whether it is 
        3 colorable 
        (3)---(2) 
        | / | 
        | / | 
        | / | 
        (0)---(1) 
        */
        int[, ] graph = { { 0, 1, 1, 1 },
                          { 1, 0, 1, 0 },
                          { 1, 1, 0, 1 },
                          { 1, 0, 1, 0 } };
        int m = 3; // Number of colors
        Coloring.graphColoring(graph, m);
    }
}

// This code is contributed by PrinciRaj1992

```

**Output:** 

```
Solution Exists: Following are the assigned colors 
 1  2  3  2

```

**复杂度分析**：

*   **时间复杂度**：O（m ^ V）。
    共有 O（m ^ V）种颜色组合。 因此，时间复杂度为 O（m ^ V）。 上限时间复杂度保持不变，但平均时间将减少。
*   **空间复杂度**：O（V）。
    要存储输出数组，需要 O（V）空间。

**<u>方法 3：</u>** 使用 BFS

这里的方法是首先用颜色 1 为每个节点从 1 到 n 着色。然后从未访问的起始节点开始行进 BFS，以一次性覆盖所有连接的组件。 在 BFS 遍历期间到达每个节点时，请执行以下操作：

*   检查给定节点的所有边缘。
*   对于通过边连接到节点的每个顶点：
    *   检查节点的颜色是否相同。 如果相同，则将另一个节点（不是当前节点）的颜色增加一个。
    *   检查它是否访问过或未访问过。 如果未访问，则将其标记为已访问并将其推入队列。
*   直到现在检查 maxColors 的条件。 如果超过 M，则返回 false

访问所有节点后，返回 true（因为在旅行时找不到违反条件）。

## C++

```cpp

// CPP program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

class node 
{

    // A node class which stores the color and the edges
    // connected to the node
public:
    int color = 1;
    set<int> edges;
};

int canPaint(vector<node>& nodes, int n, int m)
{

    // Create a visited array of n
    // nodes, initialized to zero
    vector<int> visited(n + 1, 0);

    // maxColors used till now are 1 as
    // all nodes are painted color 1
    int maxColors = 1;

    // Do a full BFS traversal from
    // all unvisited starting points
    for (int sv = 1; sv <= n; sv++) 
    {

        if (visited[sv])
            continue;

        // If the starting point is unvisited,
        // mark it visited and push it in queue
        visited[sv] = 1;
        queue<int> q;
        q.push(sv);

        // BFS Travel starts here
        while (!q.empty()) 
        {

            int top = q.front();
            q.pop();

            // Checking all adjacent nodes
            // to "top" edge in our queue
            for (auto it = nodes[top].edges.begin();
                 it != nodes[top].edges.end(); it++) 
            {

                // IMPORTANT: If the color of the
                // adjacent node is same, increase it by 1
                if (nodes[top].color == nodes[*it].color)
                    nodes[*it].color += 1;

                // If number of colors used shoots m, return
                // 0
                maxColors
                    = max(maxColors, max(nodes[top].color,
                                         nodes[*it].color));
                if (maxColors > m)
                    return 0;

                // If the adjacent node is not visited,
                // mark it visited and push it in queue
                if (!visited[*it]) {
                    visited[*it] = 1;
                    q.push(*it);
                }
            }
        }
    }

    return 1;
}

// Driver program to test above solution
int main()
{
    int t;
    cin >> t;

    // Run a loop for t test cases
    while (t--) 
    {

        // For each test case accept
        // the values of N, M and E
        int n, m, e;
        cin >> n >> m >> e;

        // Create a vector of n+1
        // nodes of type "node"
        // The zeroth position is just
        // dummy (1 to n to be used)
        vector<node> nodes(n + 1);

        // Add edges to each node as per given input
        for (int i = 0; i < e; i++) 
        {
            int s, d;
            cin >> s >> d;

            // Connect the undirected graph
            nodes[s].edges.insert(d);
            nodes[d].edges.insert(s);
        }

        // Display final answer
        cout << canPaint(nodes, n, m);
        cout << "\n";
    }
    return 0;
}

```

**参考**：，
[http://en.wikipedia.org/wiki/Graph_coloring](http://en.wikipedia.org/wiki/Graph_coloring)
如果发现不正确的内容，或者想分享有关的更多信息，请写评论 上面讨论的主题。

