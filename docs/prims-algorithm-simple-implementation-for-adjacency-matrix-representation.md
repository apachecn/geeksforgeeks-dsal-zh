# Prim 算法(邻接矩阵表示的简单实现)

> 原文:[https://www . geesforgeks . org/prims-算法-简单-实现-针对邻接矩阵-表示/](https://www.geeksforgeeks.org/prims-algorithm-simple-implementation-for-adjacency-matrix-representation/)

我们讨论了图的邻接矩阵表示的 [Prim 算法及其实现。
如前一篇文章所述，在](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/) [Prim 的算法](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)中，维护了两个集合，一个集合包含已经包含在 MST 中的顶点列表，另一个集合包含尚未包含的顶点。在每次迭代中，我们考虑连接两个集合的边中的最小权重边。
上一篇文章中讨论的实现使用两个数组来寻找连接两个集合的最小权重边。这里我们用一个 inMST[V]。如果顶点 I 包含在 MST 中，MST[i]的值将为真。在每一遍中，我们只考虑那些边，使得边的一个顶点包含在 MST 中，而另一个顶点不包含在 MST 中。在我们拾取一条边之后，我们将两个顶点都标记为包含在 MST 中。

## C++

```
// A simple C++ implementation to find minimum
// spanning tree for adjacency representation.
#include <bits/stdc++.h>
using namespace std;
#define V 5

// Returns true if edge u-v is a valid edge to be
// include in MST. An edge is valid if one end is
// already included in MST and other is not in MST.
bool isValidEdge(int u, int v, vector<bool> inMST)
{
   if (u == v)
       return false;
   if (inMST[u] == false && inMST[v] == false)
        return false;
   else if (inMST[u] == true && inMST[v] == true)
        return false;
   return true;
}

void primMST(int cost[][V])
{ 
    vector<bool> inMST(V, false);

    // Include first vertex in MST
    inMST[0] = true;

    // Keep adding edges while number of included
    // edges does not become V-1.
    int edge_count = 0, mincost = 0;
    while (edge_count < V - 1) {

        // Find minimum weight valid edge. 
        int min = INT_MAX, a = -1, b = -1;
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {              
                if (cost[i][j] < min) {
                    if (isValidEdge(i, j, inMST)) {
                        min = cost[i][j];
                        a = i;
                        b = j;
                    }
                }
            }
        }
        if (a != -1 && b != -1) {
            printf("Edge %d:(%d, %d) cost: %d \n",
                         edge_count++, a, b, min);
            mincost = mincost + min;
            inMST[b] = inMST[a] = true;
        }
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
    primMST(cost);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java implementation to find minimum
// spanning tree for adjacency representation.
import java.util.*;

class GFG
{

static int V = 5;
static int INT_MAX = Integer.MAX_VALUE;

// Returns true if edge u-v is a valid edge to be
// include in MST. An edge is valid if one end is
// already included in MST and other is not in MST.
static boolean isValidEdge(int u, int v,
                           boolean[] inMST)
{
    if (u == v)
        return false;
    if (inMST[u] == false && inMST[v] == false)
        return false;
    else if (inMST[u] == true && inMST[v] == true)
        return false;
    return true;
}

static void primMST(int cost[][])
{
    boolean []inMST = new boolean[V];

    // Include first vertex in MST
    inMST[0] = true;

    // Keep adding edges while number of included
    // edges does not become V-1.
    int edge_count = 0, mincost = 0;
    while (edge_count < V - 1)
    {

        // Find minimum weight valid edge.
        int min = INT_MAX, a = -1, b = -1;
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {            
                if (cost[i][j] < min)
                {
                    if (isValidEdge(i, j, inMST))
                    {
                        min = cost[i][j];
                        a = i;
                        b = j;
                    }
                }
            }
        }

        if (a != -1 && b != -1)
        {
            System.out.printf("Edge %d:(%d, %d) cost: %d \n",
                                    edge_count++, a, b, min);
            mincost = mincost + min;
            inMST[b] = inMST[a] = true;
        }
    }
    System.out.printf("\n Minimum cost = %d \n", mincost);
}

// Driver Code
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
    int cost[][] = {{ INT_MAX, 2, INT_MAX, 6, INT_MAX },
                    { 2, INT_MAX, 3, 8, 5 },
                    { INT_MAX, 3, INT_MAX, INT_MAX, 7 },
                    { 6, 8, INT_MAX, INT_MAX, 9 },
                    { INT_MAX, 5, 7, 9, INT_MAX }};

    // Print the solution
    primMST(cost);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find minimum
# spanning tree for adjacency representation.
from sys import maxsize
INT_MAX = maxsize
V = 5

# Returns true if edge u-v is a valid edge to be
# include in MST. An edge is valid if one end is
# already included in MST and other is not in MST.
def isValidEdge(u, v, inMST):
    if u == v:
        return False
    if inMST[u] == False and inMST[v] == False:
        return False
    elif inMST[u] == True and inMST[v] == True:
        return False
    return True

def primMST(cost):
    inMST = [False] * V

    # Include first vertex in MST
    inMST[0] = True

    # Keep adding edges while number of included
    # edges does not become V-1.
    edge_count = 0
    mincost = 0
    while edge_count < V - 1:

        # Find minimum weight valid edge.
        minn = INT_MAX
        a = -1
        b = -1
        for i in range(V):
            for j in range(V):
                if cost[i][j] < minn:
                    if isValidEdge(i, j, inMST):
                        minn = cost[i][j]
                        a = i
                        b = j

        if a != -1 and b != -1:
            print("Edge %d: (%d, %d) cost: %d" %
                 (edge_count, a, b, minn))
            edge_count += 1
            mincost += minn
            inMST[b] = inMST[a] = True

    print("Minimum cost = %d" % mincost)

# Driver Code
if __name__ == "__main__":
    ''' Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         '''

    cost = [[INT_MAX, 2, INT_MAX, 6, INT_MAX],
            [2, INT_MAX, 3, 8, 5],
            [INT_MAX, 3, INT_MAX, INT_MAX, 7],
            [6, 8, INT_MAX, INT_MAX, 9],
            [INT_MAX, 5, 7, 9, INT_MAX]]

    # Print the solution
    primMST(cost)

# This code is contributed by
# sanjeev2552
```

## C#

```
// A simple C# implementation to find minimum
// spanning tree for adjacency representation.
using System;

class GFG
{

static int V = 5;
static int INT_MAX = int.MaxValue;

// Returns true if edge u-v is a valid edge to be
// include in MST. An edge is valid if one end is
// already included in MST and other is not in MST.
static bool isValidEdge(int u, int v,
                        bool[] inMST)
{
    if (u == v)
        return false;
    if (inMST[u] == false && inMST[v] == false)
        return false;
    else if (inMST[u] == true &&
             inMST[v] == true)
        return false;
    return true;
}

static void primMST(int [,]cost)
{
    bool []inMST = new bool[V];

    // Include first vertex in MST
    inMST[0] = true;

    // Keep adding edges while number of
    // included edges does not become V-1.
    int edge_count = 0, mincost = 0;
    while (edge_count < V - 1)
    {

        // Find minimum weight valid edge.
        int min = INT_MAX, a = -1, b = -1;
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {        
                if (cost[i, j] < min)
                {
                    if (isValidEdge(i, j, inMST))
                    {
                        min = cost[i, j];
                        a = i;
                        b = j;
                    }
                }
            }
        }

        if (a != -1 && b != -1)
        {
            Console.Write("Edge {0}:({1}, {2}) cost: {3} \n",
                                    edge_count++, a, b, min);
            mincost = mincost + min;
            inMST[b] = inMST[a] = true;
        }
    }
    Console.Write("\n Minimum cost = {0} \n", mincost);
}

// Driver Code
public static void Main(String[] args)
{
    /* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | / \ |
    (3)-------(4)
            9     */
    int [,]cost = {{ INT_MAX, 2, INT_MAX, 6, INT_MAX },
                   { 2, INT_MAX, 3, 8, 5 },
                   { INT_MAX, 3, INT_MAX, INT_MAX, 7 },
                   { 6, 8, INT_MAX, INT_MAX, 9 },
                   { INT_MAX, 5, 7, 9, INT_MAX }};

    // Print the solution
    primMST(cost);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation to find minimum
// spanning tree for adjacency representation.

let V = 5;
let let_MAX = Number.MAX_VALUE;

// Returns true if edge u-v is a valid edge to be
// include in MST. An edge is valid if one end is
// already included in MST and other is not in MST.
function isValidEdge(u, v, inMST)
{
    if (u == v)
        return false;
    if (inMST[u] == false && inMST[v] == false)
        return false;
    else if (inMST[u] == true && inMST[v] == true)
        return false;
    return true;
}

function primMST(cost)
{
    let inMST = Array(V).fill(false);

    // Include first vertex in MST
    inMST[0] = true;

    // Keep adding edges while number of included
    // edges does not become V-1.
    let edge_count = 0, mincost = 0;
    while (edge_count < V - 1)
    {

        // Find minimum weight valid edge.
        let min = let_MAX, a = -1, b = -1;
        for (let i = 0; i < V; i++)
        {
            for (let j = 0; j < V; j++)
            {            
                if (cost[i][j] < min)
                {
                    if (isValidEdge(i, j, inMST))
                    {
                        min = cost[i][j];
                        a = i;
                        b = j;
                    }
                }
            }
        }

        if (a != -1 && b != -1)
        {
            document.write("Edge " +
            edge_count++ + ": (" +  a +"," + b +
            ") " + "cost: " + min + "<br/>");
            mincost = mincost + min;
            inMST[b] = inMST[a] = true;
        }
    }
     document.write("<br>");
     document.write("  ");
     document.write("Minimum cost = " + mincost);
}

// driver code

      /* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         */
    let cost = [[ let_MAX, 2, let_MAX, 6, let_MAX ],
                    [ 2, let_MAX, 3, 8, 5 ],
                    [ let_MAX, 3, let_MAX, let_MAX, 7 ],
                    [ 6, 8, let_MAX, let_MAX, 9 ],
                    [ let_MAX, 5, 7, 9, let_MAX ]];

    // Print the solution
    primMST(cost);

</script>
```

**Output:** 

```
Edge 0:(0, 1) cost: 2 
Edge 1:(1, 2) cost: 3 
Edge 2:(1, 4) cost: 5 
Edge 3:(0, 3) cost: 6 

 Minimum cost= 16
```

**时间复杂度:** O(V <sup>3</sup> )
注意[以前使用邻接矩阵](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)的方法的时间复杂度是 O(V <sup>2</sup> )，而[邻接表表示实现](https://www.geeksforgeeks.org/prims-mst-for-adjacency-list-representation-greedy-algo-6/)的时间复杂度是 O((E+V)LogV)。
**辅助空间:** O(E + V)