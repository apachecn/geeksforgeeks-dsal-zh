# 克鲁斯卡尔算法(邻接矩阵的简单实现)

> 原文:[https://www . geeksforgeeks . org/kruskals-algorithm-simple-implement-for-邻接矩阵/](https://www.geeksforgeeks.org/kruskals-algorithm-simple-implementation-for-adjacency-matrix/)

以下是使用[克鲁斯卡尔算法](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)
查找 MST 的步骤

> **1。**按权重非递减顺序对所有边进行排序。
> T3】2。挑最小的边。检查它是否与到目前为止形成的生成树形成一个循环。如果没有形成循环，包括这条边。否则，丢弃它。
> **3。**重复步骤#2，直到生成树中有(V-1)条边。

在[之前的帖子](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)中，我们已经讨论了 Kruskal 算法的一个实现。在这篇文章中，讨论了邻接矩阵的一个更简单的实现。

## C++

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java implementation for Kruskal's
// algorithm
import java.util.*;

class GFG
{

static int V = 5;
static int[] parent = new int[V];
static int INF = Integer.MAX_VALUE;

// Find set of vertex i
static int find(int i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

// Does union of i and j. It returns
// false if i and j are already in same
// set.
static void union1(int i, int j)
{
    int a = find(i);
    int b = find(j);
    parent[a] = b;
}

// Finds MST using Kruskal's algorithm
static void kruskalMST(int cost[][])
{
    int mincost = 0; // Cost of min MST.

    // Initialize sets of disjoint sets.
    for (int i = 0; i < V; i++)
        parent[i] = i;

    // Include minimum weight edges one by one
    int edge_count = 0;
    while (edge_count < V - 1)
    {
        int min = INF, a = -1, b = -1;
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {
                if (find(i) != find(j) && cost[i][j] < min)
                {
                    min = cost[i][j];
                    a = i;
                    b = j;
                }
            }
        }

        union1(a, b);
        System.out.printf("Edge %d:(%d, %d) cost:%d \n",
            edge_count++, a, b, min);
        mincost += min;
    }
    System.out.printf("\n Minimum cost= %d \n", mincost);
}

// Driver code
public static void main(String[] args)
{
/* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         */
    int cost[][] = {
        { INF, 2, INF, 6, INF },
        { 2, INF, 3, 8, 5 },
        { INF, 3, INF, INF, 7 },
        { 6, 8, INF, INF, 9 },
        { INF, 5, 7, 9, INF },
    };

    // Print the solution
    kruskalMST(cost);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation for Kruskal's
# algorithm

# Find set of vertex i
def find(i):
    while parent[i] != i:
        i = parent[i]
    return i

# Does union of i and j. It returns
# false if i and j are already in same
# set.
def union(i, j):
    a = find(i)
    b = find(j)
    parent[a] = b

# Finds MST using Kruskal's algorithm
def kruskalMST(cost):
    mincost = 0 # Cost of min MST

    # Initialize sets of disjoint sets
    for i in range(V):
        parent[i] = i

    # Include minimum weight edges one by one
    edge_count = 0
    while edge_count < V - 1:
        min = INF
        a = -1
        b = -1
        for i in range(V):
            for j in range(V):
                if find(i) != find(j) and cost[i][j] < min:
                    min = cost[i][j]
                    a = i
                    b = j
        union(a, b)
        print('Edge {}:({}, {}) cost:{}'.format(edge_count, a, b, min))
        edge_count += 1
        mincost += min

    print("Minimum cost= {}".format(mincost))

# Driver code
# Let us create the following graph
#         2 3
#     (0)--(1)--(2)
#     | / \ |
#     6| 8/ \5 |7
#     | /     \ |
#     (3)-------(4)
#         9

V = 5
parent = [i for i in range(V)]
INF = float('inf')
cost = [[INF, 2, INF, 6, INF],
        [2, INF, 3, 8, 5],
        [INF, 3, INF, INF, 7],
        [6, 8, INF, INF, 9],
        [INF, 5, 7, 9, INF]]

# Print the solution
kruskalMST(cost)

# This code is contributed by ng24_7
```

## C#

```
// Simple C# implementation for Kruskal's
// algorithm
using System;    

class GFG
{

static int V = 5;
static int[] parent = new int[V];
static int INF = int.MaxValue;

// Find set of vertex i
static int find(int i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

// Does union of i and j. It returns
// false if i and j are already in same
// set.
static void union1(int i, int j)
{
    int a = find(i);
    int b = find(j);
    parent[a] = b;
}

// Finds MST using Kruskal's algorithm
static void kruskalMST(int [,]cost)
{
    int mincost = 0; // Cost of min MST.

    // Initialize sets of disjoint sets.
    for (int i = 0; i < V; i++)
        parent[i] = i;

    // Include minimum weight edges one by one
    int edge_count = 0;
    while (edge_count < V - 1)
    {
        int min = INF, a = -1, b = -1;
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {
                if (find(i) != find(j) && cost[i, j] < min)
                {
                    min = cost[i, j];
                    a = i;
                    b = j;
                }
            }
        }

        union1(a, b);
        Console.Write("Edge {0}:({1}, {2}) cost:{3} \n",
            edge_count++, a, b, min);
        mincost += min;
    }
    Console.Write("\n Minimum cost= {0} \n", mincost);
}

// Driver code
public static void Main(String[] args)
{
/* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         */
    int [,]cost = {
        { INF, 2, INF, 6, INF },
        { 2, INF, 3, 8, 5 },
        { INF, 3, INF, INF, 7 },
        { 6, 8, INF, INF, 9 },
        { INF, 5, 7, 9, INF },
    };

    // Print the solution
    kruskalMST(cost);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Simple Javascript implementation for Kruskal's
// algorithm

var V = 5;
var parent = Array(V).fill(0);
var INF = 1000000000;

// Find set of vertex i
function find(i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

// Does union of i and j. It returns
// false if i and j are already in same
// set.
function union1(i, j)
{
    var a = find(i);
    var b = find(j);
    parent[a] = b;
}

// Finds MST using Kruskal's algorithm
function kruskalMST(cost)
{
    var mincost = 0; // Cost of min MST.

    // Initialize sets of disjoint sets.
    for (var i = 0; i < V; i++)
        parent[i] = i;

    // Include minimum weight edges one by one
    var edge_count = 0;
    while (edge_count < V - 1)
    {
        var min = INF, a = -1, b = -1;
        for (var i = 0; i < V; i++)
        {
            for (var j = 0; j < V; j++)
            {
                if (find(i) != find(j) && cost[i][j] < min)
                {
                    min = cost[i][j];
                    a = i;
                    b = j;
                }
            }
        }

        union1(a, b);
        document.write(`Edge ${edge_count++}:(${a},
        ${b}) cost:${min} <br>`);
        mincost += min;
    }
    document.write(`<br> Minimum cost= ${mincost} <br>`);
}

// Driver code

/* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         */
var cost = [
    [INF, 2, INF, 6, INF],
    [2, INF, 3, 8, 5],
    [INF, 3, INF, INF, 7],
    [6, 8, INF, INF, 9],
    [INF, 5, 7, 9, INF]];
// Print the solution
kruskalMST(cost);

</script>
```

**Output:** 

```
Edge 0:(0, 1) cost:2 
Edge 1:(1, 2) cost:3 
Edge 2:(1, 4) cost:5 
Edge 3:(0, 3) cost:6 

 Minimum cost= 16
```

请注意，上述解决方案效率不高。其思想是为邻接矩阵表示提供一个简单的实现。请参见下面的高效实现。
[克鲁斯卡尔最小生成树算法|贪婪算法-2](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)
[克鲁斯卡尔最小生成树使用 C++中的 STL](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/)