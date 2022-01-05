# 用 DFS 方法计算无环图中两个顶点之间的节点数

> 原文:[https://www . geeksforgeeks . org/通过 dfs 方法计算非循环图中两个顶点之间的节点数/](https://www.geeksforgeeks.org/calculate-number-of-nodes-between-two-vertices-in-an-acyclic-graph-by-dfs-method/)

给定一个由 **V** 顶点和 **E** 边、一个源顶点 **src** 和一个目的顶点 **dest** 组成的连通非循环图，任务是计算图中给定源顶点和目的顶点之间的顶点数。

**示例**:

> **输入:** V = 8，E = 7，src = 7，dest = 8，edges[][] ={{1 4}，{4，5}，{4，2}，{2，6}，{6，3}，{2，7}，{3，8}}
> 输出:3
> T6】解释:T8】7 和 8 之间的路径是 7->2->6->3->3
> 所以，7 到 8 之间的节点数是 3。
> 
> [![](img/f4160071d20eb16a4c9057b36676f7fc.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200908100034/acyclicGraph.jpg)
> 
> **输入:** V = 8，E = 7，src = 5，dest = 2，edges[][] ={{1 4}，{4，5}，{4，2}，{2，6}，{6，3}，{2，7}，{3，8 } }
> T3】输出:1
> T6】解释:T8】5 和 2 之间的路径是 5 - > 4 - > 2。
> 所以，5 到 2 之间的节点数是 1。

**方法:**这个问题也可以使用[这篇](https://www.geeksforgeeks.org/number-nodes-two-vertices-acyclic-graph-disjoint-union-method/)文章中所述的[不相交联合](https://www.geeksforgeeks.org/union-find/)方法来解决。解决这个问题的另一种方法是使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)方法来解决。按照以下步骤解决此问题:

*   初始化一个访问过的数组 **vis[]** 来标记哪些节点已经被访问过。将所有节点标记为 0，即未访问。
*   执行一个 DFS，找出**和 ***dest 之间路径中存在的节点数。*****
*   *****src*** 和 ***dest*** 之间的节点数等于它们与 2 之间的路径长度差，即***(path srctdest–2***)。**
*   **由于图是无环且连通的，因此在**和 ***dest 之间总会有一条单一的路径。*******

****下面是上述算法的实现。****

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of nodes
// in the path from source to destination
int dfs(int src, int dest, int* vis,
        vector<int>* adj)
{

    // Mark the node visited
    vis[src] = 1;

    // If dest is reached
    if (src == dest) {
        return 1;
    }

    // Traverse all adjacent nodes
    for (int u : adj[src]) {

        // If not already visited
        if (!vis[u]) {

            int temp = dfs(u, dest, vis, adj);

            // If there is path, then
            // include the current node
            if (temp != 0) {

                return temp + 1;
            }
        }
    }

    // Return 0 if there is no path
    // between src and dest through
    // the current node
    return 0;
}

// Function to return the
// count of nodes between two
// given vertices of the acyclic Graph
int countNodes(int V, int E, int src, int dest,
               int edges[][2])
{
    // Initialize an adjacency list
    vector<int> adj[V + 1];

    // Populate the edges in the list
    for (int i = 0; i < E; i++) {
        adj[edges[i][0]].push_back(edges[i][1]);
        adj[edges[i][1]].push_back(edges[i][0]);
    }

    // Mark all the nodes as not visited
    int vis[V + 1] = { 0 };

    // Count nodes in the path from src to dest
    int count = dfs(src, dest, vis, adj);

    // Return the nodes between src and dest
    return count - 2;
}

// Driver Code
int main()
{
    // Given number of vertices and edges
    int V = 8, E = 7;

    // Given source and destination vertices
    int src = 5, dest = 2;

    // Given edges
    int edges[][2]
        = { { 1, 4 }, { 4, 5 },
            { 4, 2 }, { 2, 6 },
            { 6, 3 }, { 2, 7 },
            { 3, 8 } };

    cout << countNodes(V, E, src, dest, edges);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.Vector;
class GFG{

// Function to return the count of nodes
// in the path from source to destination
static int dfs(int src, int dest, int []vis,
               Vector<Integer> []adj)
{
  // Mark the node visited
  vis[src] = 1;

  // If dest is reached
  if (src == dest)
  {
    return 1;
  }

  // Traverse all adjacent nodes
  for (int u : adj[src])
  {
    // If not already visited
    if (vis[u] == 0)
    {
      int temp = dfs(u, dest,
                     vis, adj);

      // If there is path, then
      // include the current node
      if (temp != 0)
      {
        return temp + 1;
      }
    }
  }

  // Return 0 if there is no path
  // between src and dest through
  // the current node
  return 0;
}

// Function to return the
// count of nodes between two
// given vertices of the acyclic Graph
static int countNodes(int V, int E,
                      int src, int dest,
                      int edges[][])
{
  // Initialize an adjacency list
  Vector<Integer> []adj = new Vector[V + 1];
  for (int i = 0; i < adj.length; i++)
    adj[i] = new Vector<Integer>();

  // Populate the edges in the list
  for (int i = 0; i < E; i++)
  {
    adj[edges[i][0]].add(edges[i][1]);
    adj[edges[i][1]].add(edges[i][0]);
  }

  // Mark all the nodes as
  // not visited
  int vis[] = new int[V + 1];

  // Count nodes in the path
  // from src to dest
  int count = dfs(src, dest,
                  vis, adj);

  // Return the nodes
  // between src and dest
  return count - 2;
}

// Driver Code
public static void main(String[] args)
{
  // Given number of vertices and edges
  int V = 8, E = 7;

  // Given source and destination vertices
  int src = 5, dest = 2;

  // Given edges
  int edges[][] = {{1, 4}, {4, 5},
                   {4, 2}, {2, 6},
                   {6, 3}, {2, 7},
                   {3, 8}};

  System.out.print(countNodes(V, E,
                              src, dest,
                              edges));
}
}

// This code is contributed by shikhasingrajput**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to return the count of nodes
# in the path from source to destination
def dfs(src, dest, vis, adj):

    # Mark the node visited
    vis[src] = 1

    # If dest is reached
    if (src == dest):
        return 1

    # Traverse all adjacent nodes
    for u in adj[src]:

        # If not already visited
        if not vis[u]:
            temp = dfs(u, dest, vis, adj)

            # If there is path, then
            # include the current node
            if (temp != 0):
                return temp + 1

    # Return 0 if there is no path
    # between src and dest through
    # the current node
    return 0

# Function to return the
# count of nodes between two
# given vertices of the acyclic Graph
def countNodes(V, E, src, dest, edges):

    # Initialize an adjacency list
    adj = [[] for i in range(V + 1)]

    # Populate the edges in the list
    for i in range(E):
        adj[edges[i][0]].append(edges[i][1])
        adj[edges[i][1]].append(edges[i][0])

    # Mark all the nodes as not visited
    vis = [0] * (V + 1)

    # Count nodes in the path from src to dest
    count = dfs(src, dest, vis, adj)

    # Return the nodes between src and dest
    return count - 2

# Driver Code
if __name__ == '__main__':

    # Given number of vertices and edges
    V = 8
    E = 7

    # Given source and destination vertices
    src = 5
    dest = 2

    # Given edges
    edges = [ [ 1, 4 ], [ 4, 5 ],
              [ 4, 2 ], [ 2, 6 ],
              [ 6, 3 ], [ 2, 7 ],
              [ 3, 8 ] ]

    print(countNodes(V, E, src, dest, edges))

# This code is contributed by mohit kumar 29   **
```

## ****C#****

```
**// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the count of nodes
// in the path from source to destination
static int dfs(int src, int dest,
               int []vis, List<int> []adj)
{
  // Mark the node visited
  vis[src] = 1;

  // If dest is reached
  if (src == dest)
  {
    return 1;
  }

  // Traverse all adjacent nodes
  foreach (int u in adj[src])
  {
    // If not already visited
    if (vis[u] == 0)
    {
      int temp = dfs(u, dest,
                     vis, adj);

      // If there is path, then
      // include the current node
      if (temp != 0)
      {
        return temp + 1;
      }
    }
  }

  // Return 0 if there is no path
  // between src and dest through
  // the current node
  return 0;
}

// Function to return the
// count of nodes between two
// given vertices of the acyclic Graph
static int countNodes(int V, int E,
                      int src, int dest,
                      int [,]edges)
{
  // Initialize an adjacency list
  List<int> []adj = new List<int>[V + 1];

  for (int i = 0; i < adj.Length; i++)
    adj[i] = new List<int>();

  // Populate the edges in the list
  for (int i = 0; i < E; i++)
  {
    adj[edges[i, 0]].Add(edges[i, 1]);
    adj[edges[i, 1]].Add(edges[i, 0]);
  }

  // Mark all the nodes as
  // not visited
  int []vis = new int[V + 1];

  // Count nodes in the path
  // from src to dest
  int count = dfs(src, dest,
                  vis, adj);

  // Return the nodes
  // between src and dest
  return count - 2;
}

// Driver Code
public static void Main(String[] args)
{
  // Given number of vertices and edges
  int V = 8, E = 7;

  // Given source and destination vertices
  int src = 5, dest = 2;

  // Given edges
  int [,]edges = {{1, 4}, {4, 5},
                  {4, 2}, {2, 6},
                  {6, 3}, {2, 7},
                  {3, 8}};

  Console.Write(countNodes(V, E, src,
                           dest, edges));
}
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>
// Javascript program for the above approach

// Function to return the count of nodes
// in the path from source to destination
function dfs(src,dest,vis,adj)
{
  // Mark the node visited
  vis[src] = 1;

  // If dest is reached
  if (src == dest)
  {
    return 1;
  }

  // Traverse all adjacent nodes
  for (let u=0;u< adj[src].length;u++)
  {
    // If not already visited
    if (vis[adj[src][u]] == 0)
    {
      let temp = dfs(adj[src][u], dest,
                     vis, adj);

      // If there is path, then
      // include the current node
      if (temp != 0)
      {
        return temp + 1;
      }
    }
  }

  // Return 0 if there is no path
  // between src and dest through
  // the current node
  return 0;
}

// Function to return the
// count of nodes between two
// given vertices of the acyclic Graph
function countNodes(V,E,src,dest,edges)
{
    // Initialize an adjacency list
  let adj = new Array(V + 1);
  for (let i = 0; i < adj.length; i++)
    adj[i] = [];

  // Populate the edges in the list
  for (let i = 0; i < E; i++)
  {
    adj[edges[i][0]].push(edges[i][1]);
    adj[edges[i][1]].push(edges[i][0]);
  }

  // Mark all the nodes as
  // not visited
  let vis = new Array(V + 1);
  for(let i=0;i<vis.length;i++)
  {
      vis[i]=0;
  }
  // Count nodes in the path
  // from src to dest
  let count = dfs(src, dest,
                  vis, adj);

  // Return the nodes
  // between src and dest
  return count - 2;
}

// Driver Code
// Given number of vertices and edges
let V = 8, E = 7;

// Given source and destination vertices
let src = 5, dest = 2;

// Given edges
let edges = [[1, 4], [4, 5],
[4, 2], [2, 6],
[6, 3], [2, 7],
[3, 8]];

document.write(countNodes(V, E,
                            src, dest,
                            edges));

// This code is contributed by unknown2108
</script>**
```

******Output:** 

```
1
```**** 

*******时间复杂度:** O(V+E)*
***辅助空间:** O(V)*****