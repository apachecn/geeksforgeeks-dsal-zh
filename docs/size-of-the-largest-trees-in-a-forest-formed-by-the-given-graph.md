# 由给定图形形成的森林中最大树木的大小

> 原文:[https://www . geesforgeks . org/给定图形形成的森林中最大的树的大小/](https://www.geeksforgeeks.org/size-of-the-largest-trees-in-a-forest-formed-by-the-given-graph/)

给定一个具有 **N** 节点和 **M** 边的**无向无环图**，任务是找出该图形成的森林中最大的树的大小。

> 森林是不相交的树的集合。换句话说，我们也可以说森林是一个不连通的非循环图的集合。

**示例:**

> **输入:** N = 5，边[][] = {{0，1}，{0，2}，{3，4}}
> **输出:** 3
> **说明:**
> 有 2 棵树，每棵树大小分别为 3 和 2。
> 
> ```
>    0
>  /   \
> 1     2
> ```
> 
> 和
> 
> ```
> 3
>  \
>   4
> ```
> 
> 因此最大的树的大小是 3。
> 
> **输入:** N = 5，边[][] = {{0，1}，{0，2}，{3，4}，{0，4}，{3，5}}
> **输出:** 6

**方法:**想法是首先[统计每个森林的可达节点数量](https://www.geeksforgeeks.org/find-all-reachable-nodes-from-every-node-present-in-a-given-set/)。因此:

*   在每个节点上应用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，获取该节点形成的树的大小，并检查是否从一个源访问了每个连接的节点。
*   如果当前树的大小大于答案，则将答案更新为当前树的大小。
*   如果还没有访问某些节点集，再次执行 DFS 遍历。
*   最后，访问所有节点时所有答案的最大值就是最终答案。

下面是上述方法的实现:

## C++

```
// C++ program to find the size
// of the largest tree in the forest

#include <bits/stdc++.h>
using namespace std;

// A utility function to add
// an edge in an undirected graph.
void addEdge(vector<int> adj[],
             int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// A utility function to perform DFS of a
// graph recursively from a given vertex u
// and returns the size of the tree formed by u
int DFSUtil(int u, vector<int> adj[],
            vector<bool>& visited)
{
    visited[u] = true;
    int sz = 1;

    // Iterating through all the nodes
    for (int i = 0; i < adj[u].size(); i++)
        if (visited[adj[u][i]] == false)

            // Perform DFS if the node is
            // not yet visited
            sz += DFSUtil(
                adj[u][i], adj, visited);
    return sz;
}

// Function to return the  size of the
// largest tree in the forest given as
// the adjacency list
int largestTree(vector<int> adj[], int V)
{
    vector<bool> visited(V, false);
    int answer = 0;

    // Iterating through all the vertices
    for (int u = 0; u < V; u++) {
        if (visited[u] == false) {

            // Find the answer
            answer
                = max(answer,
                      DFSUtil(u, adj, visited));
        }
    }
    return answer;
}

// Driver code
int main()
{
    int V = 5;
    vector<int> adj[V];
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 2);
    addEdge(adj, 3, 4);
    cout << largestTree(adj, V);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the size
// of the largest tree in the forest
import java.util.*;
class GFG{

// A utility function to add
// an edge in an undirected graph.
static void addEdge(Vector<Integer> adj[],
                    int u, int v)
{
  adj[u].add(v);
  adj[v].add(u);
}

// A utility function to perform DFS of a
// graph recursively from a given vertex u
// and returns the size of the tree formed by u
static int DFSUtil(int u, Vector<Integer> adj[],
                   Vector<Boolean> visited)
{
  visited.add(u, true);
  int sz = 1;

  // Iterating through all the nodes
  for (int i = 0; i < adj[u].size(); i++)
    if (visited.get(adj[u].get(i)) == false)

      // Perform DFS if the node is
      // not yet visited
      sz += DFSUtil(adj[u].get(i),
                    adj, visited);
  return sz;
}

// Function to return the  size of the
// largest tree in the forest given as
// the adjacency list
static int largestTree(Vector<Integer> adj[],
                       int V)
{
  Vector<Boolean> visited = new Vector<>();
  for(int i = 0; i < V; i++)
  {
    visited.add(false);
  }
  int answer = 0;

  // Iterating through all the vertices
  for (int u = 0; u < V; u++)
  {
    if (visited.get(u) == false)
    {
      // Find the answer
      answer = Math.max(answer,
               DFSUtil(u, adj, visited));
    }
  }
  return answer;
}

// Driver code
public static void main(String[] args)
{
  int V = 5;
  Vector<Integer> adj[] = new Vector[V];
  for (int i = 0; i < adj.length; i++)
    adj[i] = new Vector<Integer>();
  addEdge(adj, 0, 1);
  addEdge(adj, 0, 2);
  addEdge(adj, 3, 4);
  System.out.print(largestTree(adj, V));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the size
# of the largest tree in the forest

# A utility function to add
# an edge in an undirected graph.
def addEdge(adj, u, v):

    adj[u].append(v)
    adj[v].append(u)

# A utility function to perform DFS of a
# graph recursively from a given vertex u
# and returns the size of the tree formed by u
def DFSUtil(u, adj, visited):

    visited[u] = True
    sz = 1

    # Iterating through all the nodes
    for i in range(0, len(adj[u])):
        if (visited[adj[u][i]] == False):

            # Perform DFS if the node is
            # not yet visited
            sz += DFSUtil(adj[u][i], adj, visited)

    return sz

# Function to return the  size of the
# largest tree in the forest given as
# the adjacency list
def largestTree(adj, V):

    visited = [False for i in range(V)]

    answer = 0

    # Iterating through all the vertices
    for u in range(V):
        if (visited[u] == False):

            # Find the answer
            answer = max(answer,DFSUtil(
                u, adj, visited))

    return answer

# Driver code
if __name__=="__main__":

    V = 5

    adj = [[] for i in range(V)]

    addEdge(adj, 0, 1)
    addEdge(adj, 0, 2)
    addEdge(adj, 3, 4)

    print(largestTree(adj, V))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the size
// of the largest tree in the forest
using System;
using System.Collections.Generic;
class GFG{

// A utility function to add
// an edge in an undirected graph.
static void addEdge(List<int> []adj,
                    int u, int v)
{
  adj[u].Add(v);
  adj[v].Add(u);
}

// A utility function to perform DFS of a
// graph recursively from a given vertex u
// and returns the size of the tree formed by u
static int DFSUtil(int u, List<int> []adj,
                   List<Boolean> visited)
{
  visited.Insert(u, true);
  int sz = 1;

  // Iterating through all the nodes
  for (int i = 0; i < adj[u].Count; i++)
    if (visited[adj[u][i]] == false)

      // Perform DFS if the node is
      // not yet visited
      sz += DFSUtil(adj[u][i],
                    adj, visited);
  return sz;
}

// Function to return the  size of the
// largest tree in the forest given as
// the adjacency list
static int largestTree(List<int> []adj,
                       int V)
{
  List<Boolean> visited = new List<Boolean>();
  for(int i = 0; i < V; i++)
  {
    visited.Add(false);
  }
  int answer = 0;

  // Iterating through all the vertices
  for (int u = 0; u < V; u++)
  {
    if (visited[u] == false)
    {
      // Find the answer
      answer = Math.Max(answer,
               DFSUtil(u, adj, visited));
    }
  }
  return answer;
}

// Driver code
public static void Main(String[] args)
{
  int V = 5;
  List<int> []adj = new List<int>[V];

  for (int i = 0; i < adj.Length; i++)
    adj[i] = new List<int>();

  addEdge(adj, 0, 1);
  addEdge(adj, 0, 2);
  addEdge(adj, 3, 4);
  Console.Write(largestTree(adj, V));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find the size
    // of the largest tree in the forest

    // A utility function to add
    // an edge in an undirected graph.
    function addEdge(adj, u, v)
    {
        adj[u].push(v);
        adj[v].push(u);
    }

    // A utility function to perform DFS of a
    // graph recursively from a given vertex u
    // and returns the size of the tree formed by u
    function DFSUtil(u, adj, visited)
    {
        visited[u] = true;
        let sz = 1;

        // Iterating through all the nodes
        for(let i = 0; i < adj[u].length; i++)
        {
            if (visited[adj[u][i]] == false)
            {
                // Perform DFS if the node is
                // not yet visited
                sz += DFSUtil(adj[u][i], adj, visited);
            }
        }

        return sz;
     }

    // Function to return the  size of the
    // largest tree in the forest given as
    // the adjacency list
    function largestTree(adj, V)
    {
        let visited = new Array(V);
        visited.fill(false);

        let answer = 0;

        // Iterating through all the vertices
        for(let u = 0; u < V; u++)
        {
            if (visited[u] == false)
            {
                // Find the answer
                answer = Math.max(answer,DFSUtil(u, adj, visited));
            }
        }

        return answer;
    }

    let V = 5;

    let adj = [];
    for(let i = 0; i < V; i++)
    {
        adj.push([]);
    }

    addEdge(adj, 0, 1);
    addEdge(adj, 0, 2);
    addEdge(adj, 3, 4);

    document.write(largestTree(adj, V));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(V + E)* ，其中 V 为顶点数，E 为边数。