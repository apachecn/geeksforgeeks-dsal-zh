# 树中所有成对最短路径的和

> 原文:[https://www . geesforgeks . org/全对最短路径树总和/](https://www.geeksforgeeks.org/sum-of-all-pair-shortest-paths-in-a-tree/)

给定一个加权无向图 **T** ，该图由值为**【0，N–1】**的节点和类型为{ **u** 、 **v** 、 **w** 的数组**边[]【3】**组成，该数组表示顶点 **u** 和 **v** 之间具有权重 **w** 的边。任务是找到给定树中所有成对最短路径的总和[。](https://www.geeksforgeeks.org/johnsons-algorithm/)

**示例:**

> **输入:** N = 3，边[][] = {{0，2，15}，{1，0，90}}
> **输出:** 210
> **解释:**
> 节点 0 和 1 之间的路径权重之和= 90
> 节点 0 和 2 之间的路径权重之和= 15
> 节点 1 和 2 之间的路径权重之和= 105
> 因此，总和= 90 + 15 + 105
> 
> **输入:** N = 4，边[][] = {{0，1，1}，{1，2，2}，{2，3， 3}}
> **输出:** 20
> **说明:**
> 节点 0 和 1 之间路径权重之和= 1
> 节点 0 和 2 之间路径权重之和= 3
> 节点 0 和 3 之间路径权重之和= 6
> 节点 1 和 2 之间路径权重之和= 2
> 节点 1 和 3 之间路径权重之和= 5
> 路径权重之和 节点 2 和 3 之间= 3
> 因此，总和= 1 + 3 + 6 + 2 + 5 + 3 = 20。

**天真方法:**最简单的方法是[使用弗洛伊德·沃肖尔算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)找到每对顶点之间的最短路径。在预计算每对节点之间最短路径的成本后，打印所有最短路径的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;
#define INF 99999

// Function that performs the Floyd
// Warshall to find all shortest paths
int floyd_warshall(int* graph, int V)
{

    int dist[V][V], i, j, k;

    // Initialize the distance matrix
    for (i = 0; i < V; i++) {
        for (j = 0; j < V; j++) {
            dist[i][j] = *((graph + i * V) + j);
        }
    }

    for (k = 0; k < V; k++) {

        // Pick all vertices as
        // source one by one
        for (i = 0; i < V; i++) {

            // Pick all vertices as
            // destination for the
            // above picked source
            for (j = 0; j < V; j++) {

                // If vertex k is on the
                // shortest path from i to
                // j then update dist[i][j]
                if (dist[i][k]
                        + dist[k][j]
                    < dist[i][j]) {
                    dist[i][j]
                        = dist[i][k]
                          + dist[k][j];
                }
            }
        }
    }

    // Sum the upper diagonal of the
    // shortest distance matrix
    int sum = 0;

    // Traverse the given dist[][]
    for (i = 0; i < V; i++) {

        for (j = i + 1; j < V; j++) {

            // Add the distance
            sum += dist[i][j];
        }
    }

    // Return the final sum
    return sum;
}

// Function to generate the tree
int sumOfshortestPath(int N, int E,
                      int edges[][3])
{
    int g[N][N];
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            g[i][j] = INF;
        }
    }

    // Add edges
    for (int i = 0; i < E; i++) {

        // Get source and destination
        // with weight
        int u = edges[i][0];
        int v = edges[i][1];
        int w = edges[i][2];

        // Add the edges
        g[u][v] = w;
        g[v][u] = w;
    }

    // Perform Floyd Warshal Algorithm
    return floyd_warshall((int*)g, N);
}

// Driver code
int main()
{
    // Number of Vertices
    int N = 4;

    // Number of Edges
    int E = 3;

    // Given Edges with weight
    int Edges[][3]
        = { { 0, 1, 1 }, { 1, 2, 2 },
            { 2, 3, 3 } };

    // Function Call
    cout << sumOfshortestPath(N, E, Edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

static final int INF = 99999;

// Function that performs the Floyd
// Warshall to find all shortest paths
static int floyd_warshall(int[][] graph,
                          int V)
{
  int [][]dist = new int[V][V];
  int i, j, k;

  // Initialize the distance matrix
  for (i = 0; i < V; i++)
  {
    for (j = 0; j < V; j++)
    {
      dist[i][j] = graph[i][j];
    }
  }

  for (k = 0; k < V; k++)
  {
    // Pick all vertices as
    // source one by one
    for (i = 0; i < V; i++)
    {
      // Pick all vertices as
      // destination for the
      // above picked source
      for (j = 0; j < V; j++)
      {
        // If vertex k is on the
        // shortest path from i to
        // j then update dist[i][j]
        if (dist[i][k] + dist[k][j] <
            dist[i][j])
        {
          dist[i][j] = dist[i][k] +
                       dist[k][j];
        }
      }
    }
  }

  // Sum the upper diagonal of the
  // shortest distance matrix
  int sum = 0;

  // Traverse the given dist[][]
  for (i = 0; i < V; i++)
  {
    for (j = i + 1; j < V; j++)
    {
      // Add the distance
      sum += dist[i][j];
    }
  }

  // Return the final sum
  return sum;
}

// Function to generate the tree
static int sumOfshortestPath(int N, int E,
                             int edges[][])
{
  int [][]g = new int[N][N];
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < N; j++)
    {
      g[i][j] = INF;
    }
  }

  // Add edges
  for (int i = 0; i < E; i++)
  {
    // Get source and destination
    // with weight
    int u = edges[i][0];
    int v = edges[i][1];
    int w = edges[i][2];

    // Add the edges
    g[u][v] = w;
    g[v][u] = w;
  }

  // Perform Floyd Warshal Algorithm
  return floyd_warshall(g, N);
}

// Driver code
public static void main(String[] args)
{
  // Number of Vertices
  int N = 4;

  // Number of Edges
  int E = 3;

  // Given Edges with weight
  int Edges[][] = {{0, 1, 1}, {1, 2, 2},
                   {2, 3, 3}};

  // Function Call
  System.out.print(
         sumOfshortestPath(N, E, Edges));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
INF = 99999

# Function that performs the Floyd
# Warshall to find all shortest paths
def floyd_warshall(graph, V):

    dist = [[0 for i in range(V)]
               for i in range(V)]

    # Initialize the distance matrix
    for i in range(V):
        for j in range(V):
            dist[i][j] = graph[i][j]

    for k in range(V):

        # Pick all vertices as
        # source one by one
        for i in range(V):

            # Pick all vertices as
            # destination for the
            # above picked source
            for j in range(V):

                # If vertex k is on the
                # shortest path from i to
                # j then update dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j]):
                    dist[i][j] = dist[i][k] + dist[k][j]

    # Sum the upper diagonal of the
    # shortest distance matrix
    sum = 0

    # Traverse the given dist[][]
    for i in range(V):
        for j in range(i + 1, V):

            # Add the distance
            sum += dist[i][j]

    # Return the final sum
    return sum

# Function to generate the tree
def sumOfshortestPath(N, E,edges):

    g = [[INF for i in range(N)]
              for i in range(N)]

    # Add edges
    for i in range(E):

        # Get source and destination
        # with weight
        u = edges[i][0]
        v = edges[i][1]
        w = edges[i][2]

        # Add the edges
        g[u][v] = w
        g[v][u] = w

    # Perform Floyd Warshal Algorithm
    return floyd_warshall(g, N)

# Driver code
if __name__ == '__main__':

    # Number of Vertices
    N = 4

    # Number of Edges
    E = 3

    # Given Edges with weight
    Edges = [ [ 0, 1, 1 ],
              [ 1, 2, 2 ],
              [ 2, 3, 3 ] ]

    # Function Call
    print(sumOfshortestPath(N, E, Edges))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static readonly int INF = 99999;

// Function that performs the Floyd
// Warshall to find all shortest paths
static int floyd_warshall(int[,] graph,
                          int V)
{
  int [,]dist = new int[V, V];
  int i, j, k;

  // Initialize the distance matrix
  for (i = 0; i < V; i++)
  {
    for (j = 0; j < V; j++)
    {
      dist[i, j] = graph[i, j];
    }
  }

  for (k = 0; k < V; k++)
  {
    // Pick all vertices as
    // source one by one
    for (i = 0; i < V; i++)
    {
      // Pick all vertices as
      // destination for the
      // above picked source
      for (j = 0; j < V; j++)
      {
        // If vertex k is on the
        // shortest path from i to
        // j then update dist[i,j]
        if (dist[i, k] + dist[k, j] <
            dist[i, j])
        {
          dist[i, j] = dist[i, k] +
                       dist[k, j];
        }
      }
    }
  }

  // Sum the upper diagonal of the
  // shortest distance matrix
  int sum = 0;

  // Traverse the given dist[,]
  for (i = 0; i < V; i++)
  {
    for (j = i + 1; j < V; j++)
    {
      // Add the distance
      sum += dist[i, j];
    }
  }

  // Return the readonly sum
  return sum;
}

// Function to generate the tree
static int sumOfshortestPath(int N, int E,
                             int [,]edges)
{
  int [,]g = new int[N, N];

  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < N; j++)
    {
      g[i, j] = INF;
    }
  }

  // Add edges
  for (int i = 0; i < E; i++)
  {
    // Get source and destination
    // with weight
    int u = edges[i, 0];
    int v = edges[i, 1];
    int w = edges[i, 2];

    // Add the edges
    g[u, v] = w;
    g[v, u] = w;
  }

  // Perform Floyd Warshal Algorithm
  return floyd_warshall(g, N);
}

// Driver code
public static void Main(String[] args)
{
  // Number of Vertices
  int N = 4;

  // Number of Edges
  int E = 3;

  // Given Edges with weight
  int [,]Edges = {{0, 1, 1},
                  {1, 2, 2},
                  {2, 3, 3}};

  // Function Call
  Console.Write(sumOfshortestPath(N,
                                  E, Edges));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for
// the above approach
let INF = 99999;

// Function that performs the Floyd
// Warshall to find all shortest paths
function floyd_warshall(graph,V)
{
    let dist = new Array(V);
    for(let i = 0; i < V; i++)
    {
        dist[i] = new Array(V);
    }
  let i, j, k;

  // Initialize the distance matrix
  for (i = 0; i < V; i++)
  {
    for (j = 0; j < V; j++)
    {
      dist[i][j] = graph[i][j];
    }
  }

  for (k = 0; k < V; k++)
  {

    // Pick all vertices as
    // source one by one
    for (i = 0; i < V; i++)
    {

      // Pick all vertices as
      // destination for the
      // above picked source
      for (j = 0; j < V; j++)
      {

        // If vertex k is on the
        // shortest path from i to
        // j then update dist[i][j]
        if (dist[i][k] + dist[k][j] <
            dist[i][j])
        {
          dist[i][j] = dist[i][k] +
                       dist[k][j];
        }
      }
    }
  }

  // Sum the upper diagonal of the
  // shortest distance matrix
  let sum = 0;

  // Traverse the given dist[][]
  for (i = 0; i < V; i++)
  {
    for (j = i + 1; j < V; j++)
    {
      // Add the distance
      sum += dist[i][j];
    }
  }

  // Return the final sum
  return sum;
}

// Function to generate the tree
function sumOfshortestPath(N,E,edges)
{
    let g = new Array(N);
  for (let i = 0; i < N; i++)
  {
      g[i] = new Array(N);
    for (let j = 0; j < N; j++)
    {
      g[i][j] = INF;
    }
  }

  // Add edges
  for (let i = 0; i < E; i++)
  {

    // Get source and destination
    // with weight
    let u = edges[i][0];
    let v = edges[i][1];
    let w = edges[i][2];

    // Add the edges
    g[u][v] = w;
    g[v][u] = w;
  }

  // Perform Floyd Warshal Algorithm
  return floyd_warshall(g, N);
}

// Driver code
// Number of Vertices
let N = 4;

// Number of Edges
let E = 3;

// Given Edges with weight
let Edges = [[0, 1, 1], [1, 2, 2],
[2, 3, 3]];

// Function Call
document.write(
sumOfshortestPath(N, E, Edges));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
20
```

***时间复杂度:** O(N <sup>3</sup> ，其中 N 为顶点数。*
***辅助空间:** O(N)*

**高效方法:**想法是使用[DFS 算法](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，使用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个顶点，从这个顶点访问每隔一个顶点的成本可以在线性时间内找到。按照以下步骤解决问题:

1.  遍历节点 **0** 到**N–1**。
2.  对于每个节点 **i** ，使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 找到访问每隔一个顶点的成本总和，其中源将是节点 **i** ，让我们用 **S <sub>i</sub>** 来表示这个总和。
3.  现在，计算**S = S<sub>0</sub>+S<sub>1</sub>+…+S<sub>N-1</sub>**。并将 **S** 除以 **2** ，因为每条路径都要计算两次。
4.  完成上述步骤后，打印得到的总和 **S** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function that performs the DFS
// traversal to find cost to reach
// from vertex v to other vertexes
void dfs(int v, int p,
         vector<pair<int, int>> t[],
         int h, int ans[])
{

    // Traverse the Adjacency list
    // of u
    for(pair<int, int> u : t[v])
    {
        if (u.first == p)
            continue;

        // Recursive Call
        dfs(u.first, v, t, h + u.second, ans);
    }

    // Update ans[v]
    ans[v] = h;
}

// Function to find the sum of
// weights of all paths
int solve(int n, int edges[][3])
{

    // Stores the Adjacency List
    vector<pair<int, int>> t[n];

    // Store the edges
    for(int i = 0; i < n - 1; i++)
    {
        t[edges[i][0]].push_back({edges[i][1],
                                  edges[i][2]});

        t[edges[i][1]].push_back({edges[i][0],
                                  edges[i][2]});
    }

    // sum is the answer
    int sum = 0;

    // Calculate sum for each vertex
    for(int i = 0; i < n; i++)
    {
        int ans[n];

        // Perform the DFS Traversal
        dfs(i, -1, t, 0, ans);

        // Sum of distance
        for(int j = 0; j < n; j++)
            sum += ans[j];
    }

    // Return the final sum
    return sum / 2;
}

// Driver Code
int main()
{

    // No of vertices
    int N = 4;

    // Given Edges
    int edges[][3] = { { 0, 1, 1 },
                       { 1, 2, 2 },
                       { 2, 3, 3 } };

    // Function Call
    cout << solve(N, edges) << endl;

    return 0;
}

// This code is contributed by pratham76
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.awt.*;
import java.io.*;
import java.util.*;

@SuppressWarnings("unchecked")
class GFG {

    // Function that performs the DFS
    // traversal to find cost to reach
    // from vertex v to other vertexes
    static void dfs(int v, int p,
                    ArrayList<Point> t[],
                    int h, int ans[])
    {

        // Traverse the Adjacency list
        // of u
        for (Point u : t[v]) {
            if (u.x == p)
                continue;

            // Recursive Call
            dfs(u.x, v, t, h + u.y, ans);
        }

        // Update ans[v]
        ans[v] = h;
    }

    // Function to find the sum of
    // weights of all paths
    static int solve(int n, int edges[][])
    {

        // Stores the Adjacency List
        ArrayList<Point> t[]
            = new ArrayList[n];

        for (int i = 0; i < n; i++)
            t[i] = new ArrayList<>();

        // Store the edges
        for (int i = 0; i < n - 1; i++) {

            t[edges[i][0]].add(
                new Point(edges[i][1],
                          edges[i][2]));

            t[edges[i][1]].add(
                new Point(edges[i][0],
                          edges[i][2]));
        }

        // sum is the answer
        int sum = 0;

        // Calculate sum for each vertex
        for (int i = 0; i < n; i++) {

            int ans[] = new int[n];

            // Perform the DFS Traversal
            dfs(i, -1, t, 0, ans);

            // Sum of distance
            for (int j = 0; j < n; j++)
                sum += ans[j];
        }

        // Return the final sum
        return sum / 2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // No of vertices
        int N = 4;

        // Given Edges
        int edges[][]
            = new int[][] { { 0, 1, 1 },
                            { 1, 2, 2 },
                            { 2, 3, 3 } };

        // Function Call
        System.out.println(solve(N, edges));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that performs the DFS
# traversal to find cost to reach
# from vertex v to other vertexes
def dfs(v, p, t, h, ans):

    # Traverse the Adjacency list
    # of u
    for u in t[v]:
        if (u[0] == p):
            continue

        # Recursive Call
        dfs(u[0], v, t, h + u[1], ans)

    # Update ans[v]
    ans[v] = h

# Function to find the sum of
# weights of all paths
def solve(n, edges):

    # Stores the Adjacency List
    t = [[] for i in range(n)]

    # Store the edges
    for i in range(n - 1):
        t[edges[i][0]].append([edges[i][1],
                               edges[i][2]])
        t[edges[i][1]].append([edges[i][0],
                               edges[i][2]])

    # sum is the answer
    sum = 0

    # Calculate sum for each vertex
    for i in range(n):
        ans = [0 for i in range(n)]

        # Perform the DFS Traversal
        dfs(i, -1, t, 0, ans)

        # Sum of distance
        for j in range(n):
            sum += ans[j]

    # Return the final sum
    return sum // 2

# Driver Code
if __name__ == "__main__":

    # No of vertices
    N = 4

    # Given Edges
    edges = [ [ 0, 1, 1 ],
              [ 1, 2, 2 ],
              [ 2, 3, 3 ] ]

    # Function Call
    print(solve(N, edges))

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that performs the DFS
// traversal to find cost to reach
// from vertex v to other vertexes
static void dfs(int v, int p,
                List<Tuple<int, int>> []t,
                int h, int []ans)
{

    // Traverse the Adjacency list
    // of u
    foreach(Tuple<int, int> u in t[v])
    {
        if (u.Item1 == p)
            continue;

        // Recursive call
        dfs(u.Item1, v, t,
        h + u.Item2, ans);
    }

    // Update ans[v]
    ans[v] = h;
}

// Function to find the sum of
// weights of all paths
static int solve(int n, int [,]edges)
{

    // Stores the Adjacency List
    List<Tuple<int,
               int>> []t = new List<Tuple<int,
                                          int>>[n];

    for(int i = 0; i < n; i++)
        t[i] = new List<Tuple<int, int>>();

    // Store the edges
    for(int i = 0; i < n - 1; i++)
    {
        t[edges[i, 0]].Add(
            new Tuple<int, int>(edges[i, 1],
                                edges[i, 2]));

        t[edges[i, 1]].Add(
            new Tuple<int, int>(edges[i, 0],
                                edges[i, 2]));
    }

    // sum is the answer
    int sum = 0;

    // Calculate sum for each vertex
    for(int i = 0; i < n; i++)
    {
        int []ans = new int[n];

        // Perform the DFS Traversal
        dfs(i, -1, t, 0, ans);

        // Sum of distance
        for(int j = 0; j < n; j++)
            sum += ans[j];
    }

    // Return the readonly sum
    return sum / 2;
}

// Driver Code
public static void Main(String[] args)
{

    // No of vertices
    int N = 4;

    // Given Edges
    int [,]edges = new int[,] { { 0, 1, 1 },
                                { 1, 2, 2 },
                                { 2, 3, 3 } };

    // Function call
    Console.WriteLine(solve(N, edges));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that performs the DFS
// traversal to find cost to reach
// from vertex v to other vertexes
function dfs(v, p, t, h, ans)
{

    // Traverse the Adjacency list
    // of u
    for(let u = 0; u < t[v].length; u++)
    {
        if (t[v][u][0] == p)
            continue;

        // Recursive Call
        dfs(t[v][u][0], v, t,
        h + t[v][u][1], ans);
    }

    // Update ans[v]
    ans[v] = h;
}

// Function to find the sum of
// weights of all paths
function solve(n, edges)
{

    // Stores the Adjacency List
    let t = new Array(n);

    for(let i = 0; i < n; i++)
        t[i] = [];

    // Store the edges
    for(let i = 0; i < n - 1; i++)
    {

        t[edges[i][0]].push([edges[i][1],
                             edges[i][2]]);

        t[edges[i][1]].push([edges[i][0],
                             edges[i][2]]);
    }

    // Sum is the answer
    let sum = 0;

    // Calculate sum for each vertex
    for(let i = 0; i < n; i++)
    {
        let ans = new Array(n);

        // Perform the DFS Traversal
        dfs(i, -1, t, 0, ans);

        // Sum of distance
        for(let j = 0; j < n; j++)
            sum += ans[j];
    }

    // Return the final sum
    return sum / 2;
}

// Driver Code
let N = 4;
let edges = [ [ 0, 1, 1 ],
              [ 1, 2, 2 ],
              [ 2, 3, 3 ] ];

document.write(solve(N, edges));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
20
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为顶点数。*
***辅助空间:** O(N)*