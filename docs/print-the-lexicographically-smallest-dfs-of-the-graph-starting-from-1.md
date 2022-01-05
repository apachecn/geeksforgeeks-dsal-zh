# 从 1

开始打印图的字典最小 DFS

> 原文:[https://www . geeksforgeeks . org/print-the-the-字典最小-DFS-of-graph-from-1/](https://www.geeksforgeeks.org/print-the-lexicographically-smallest-dfs-of-the-graph-starting-from-1/)

给定一个有 **N 个顶点**和 **M 条边**的连通图。任务是打印从 1 开始的字典最小的图的 DFS 遍历。**注意**顶点编号从 **1** 到 **N** 。
**举例:**

> **输入:** N = 5，M = 5，边[] = {{1，4}，{3，4}，{5，4}，{3，2}，{1，5}}
> **输出:**1 4 3 2 5
> T6】输入: N = 5，M = 8，边[] = {{1，4}，{3，4}，{5，4}，{3，2}，{1，5}，{1，2}，{1，1 }

**方法:**不做普通的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，首先我们要对每个顶点的边进行排序，这样在每一轮中只有最小的边被首先拾取。排序后，只需执行一个正常的 DFS，它将给出字典最小的 DFS 遍历。
以下是上述方法的实施:

## C++

```
// C++ program to find the lexicographically
// smallest traversal of a graph
#include <bits/stdc++.h>
using namespace std;

// Utility function to add an
// edge to the graph
void insertEdges(int u, int v, vector<int>* adj)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform DFS traversal
void dfs(vector<int>* adj, int src, int n,
         bool* visited)
{
    // Print current vertex
    cout << src << " ";

    // Mark it as visited
    visited[src] = true;

    // Iterate over all the edges connected
    // to this vertex
    for (int i = 0; i < adj[src].size(); i++) {
        // If this vertex is not visited,
        /// call dfs from this node
        if (!visited[adj[src][i]])
            dfs(adj, adj[src][i], n, visited);
    }
}

// Function to print the lexicographically
// smallest DFS
void printLexoSmall(vector<int>* adj, int n)
{
    // A boolean array to keep track of
    // nodes visited
    bool visited[n + 1] = { 0 };

    // Sort the edges of each vertex in
    // ascending order
    for (int i = 0; i < n; i++)
        sort(adj[i].begin(), adj[i].end());

    // Call DFS
    for (int i = 1; i < n; i++) {
        if (!visited[i])
            dfs(adj, i, n, visited);
    }
}

// Driver code
int main()
{
    int n = 5, m = 5;
    vector<int> adj[n + 1];

    insertEdges(1, 4, adj);
    insertEdges(3, 4, adj);
    insertEdges(5, 4, adj);
    insertEdges(3, 2, adj);
    insertEdges(1, 5, adj);
    insertEdges(1, 2, adj);
    insertEdges(3, 5, adj);
    insertEdges(1, 3, adj);

    printLexoSmall(adj, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the lexicographically
// smallest traversal of a graph
import java.util.*;

class GFG
{

    static boolean visited[];
    static Vector<Vector<Integer>> adj = new Vector<Vector<Integer>>();

// Utility function to add an
// edge to the graph
static void insertEdges(int u, int v)
{
    adj.get(u).add(v);
    adj.get(v).add(u);
}

// Function to perform DFS traversal
static void dfs( int src, int n)
{
    // Print current vertex
    System.out.print( src + " ");

    // Mark it as visited
    visited[src] = true;

    // Iterate over all the edges connected
    // to this vertex
    for (int i = 0; i < adj.get(src).size(); i++)
    {
        // If this vertex is not visited,
        /// call dfs from this node
        if (!visited[adj.get(src).get(i)])
            dfs( adj.get(src).get(i), n);
    }
}

// Function to print the lexicographically
// smallest DFS
static void printLexoSmall( int n)
{
    // A boolean array to keep track of
    // nodes visited
    visited= new boolean[n + 1];

    // Sort the edges of each vertex in
    // ascending order
    for (int i = 0; i < n; i++)
        Collections.sort(adj.get(i));

    // Call DFS
    for (int i = 1; i < n; i++)
    {
        if (!visited[i])
            dfs( i, n);
    }
}

// Driver code
public static void main(String args[])
{
    int n = 5, m = 5;

    for(int i = 0; i < n + 1; i++)
    adj.add(new Vector<Integer>());

    insertEdges(1, 4);
    insertEdges(3, 4);
    insertEdges(5, 4);
    insertEdges(3, 2);
    insertEdges(1, 5);
    insertEdges(1, 2);
    insertEdges(3, 5);
    insertEdges(1, 3);

    printLexoSmall( n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the lexicographically
# smallest traversal of a graph

# Utility function to add an edge
# to the graph
def insertEdges(u, v, adj):

    adj[u].append(v)
    adj[v].append(u)

# Function to perform DFS traversal
def dfs(adj, src, n, visited):

    # Print current vertex
    print(src, end = " ")

    # Mark it as visited
    visited[src] = True

    # Iterate over all the edges
    # connected to this vertex
    for i in range(0, len(adj[src])):

        # If this vertex is not visited,
        # call dfs from this node
        if not visited[adj[src][i]]:
            dfs(adj, adj[src][i], n, visited)

# Function to print the lexicographically
# smallest DFS
def printLexoSmall(adj, n):

    # A boolean array to keep track
    # of nodes visited
    visited = [0] * (n + 1)

    # Sort the edges of each vertex 
    # in ascending order
    for i in range(0, n):
        adj[i].sort()

    # Call DFS
    for i in range(1, n):
        if not visited[i]:
            dfs(adj, i, n, visited)

# Driver code
if __name__ == "__main__":

    n, m = 5, 5
    adj = [[] for i in range(n + 1)]

    insertEdges(1, 4, adj)
    insertEdges(3, 4, adj)
    insertEdges(5, 4, adj)
    insertEdges(3, 2, adj)
    insertEdges(1, 5, adj)
    insertEdges(1, 2, adj)
    insertEdges(3, 5, adj)
    insertEdges(1, 3, adj)

    printLexoSmall(adj, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the lexicographically
// smallest traversal of a graph
using System;
using System.Collections.Generic;

class GFG
{

    public static bool[] visited;
    public static List<List<int>> adj = new List<List<int>>();

// Utility function to add an
// edge to the graph
public static void insertEdges(int u, int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

// Function to perform DFS traversal
public static void dfs(int src, int n)
{
    // Print current vertex
    Console.Write(src + " ");

    // Mark it as visited
    visited[src] = true;

    // Iterate over all the edges connected
    // to this vertex
    for (int i = 0; i < adj[src].Count; i++)
    {
        // If this vertex is not visited,
        /// call dfs from this node
        if (!visited[adj[src][i]])
        {
            dfs(adj[src][i], n);
        }
    }
}

// Function to print the lexicographically
// smallest DFS
public static void printLexoSmall(int n)
{
    // A boolean array to keep track of
    // nodes visited
    visited = new bool[n + 1];

    // Sort the edges of each vertex in
    // ascending order
    for (int i = 0; i < n; i++)
    {
        adj[i].Sort();
    }

    // Call DFS
    for (int i = 1; i < n; i++)
    {
        if (!visited[i])
        {
            dfs(i, n);
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int n = 5, m = 5;

    for (int i = 0; i < n + 1; i++)
    {
        adj.Add(new List<int>());
    }

    insertEdges(1, 4);
    insertEdges(3, 4);
    insertEdges(5, 4);
    insertEdges(3, 2);
    insertEdges(1, 5);
    insertEdges(1, 2);
    insertEdges(3, 5);
    insertEdges(1, 3);

    printLexoSmall(n);
}
}

// This code is contributed by shrikanth13
```

## java 描述语言

```
<script>
// Javascript program to find the lexicographically
// smallest traversal of a graph

let visited;
let adj =[] ;

// Utility function to add an
// edge to the graph
function insertEdges(u,v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function to perform DFS traversal
function dfs(src,n)
{
    // Print current vertex
    document.write( src + " ");

    // Mark it as visited
    visited[src] = true;

    // Iterate over all the edges connected
    // to this vertex
    for (let i = 0; i < adj[src].length; i++)
    {
        // If this vertex is not visited,
        /// call dfs from this node
        if (!visited[adj[src][i]])
            dfs( adj[src][i], n);
    }
}

// Function to print the lexicographically
// smallest DFS
function printLexoSmall(n)
{
    // A boolean array to keep track of
    // nodes visited
    visited= new Array(n + 1);

    // Sort the edges of each vertex in
    // ascending order
    for (let i = 0; i < n; i++)
        adj[i].sort(function(a,b){return a-b;});

    // Call DFS
    for (let i = 1; i < n; i++)
    {
        if (!visited[i])
            dfs( i, n);
    }
}

// Driver code
let n = 5, m = 5;

for(let i = 0; i < n + 1; i++)
    adj.push([]);

insertEdges(1, 4);
insertEdges(3, 4);
insertEdges(5, 4);
insertEdges(3, 2);
insertEdges(1, 5);
insertEdges(1, 2);
insertEdges(3, 5);
insertEdges(1, 3);

printLexoSmall( n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1 2 3 4 5
```