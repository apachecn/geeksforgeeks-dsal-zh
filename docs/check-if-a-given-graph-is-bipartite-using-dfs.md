# 使用 DFS 检查给定的图是否是二分图

> 原文:[https://www . geeksforgeeks . org/check-如果给定的图是二分图-使用-dfs/](https://www.geeksforgeeks.org/check-if-a-given-graph-is-bipartite-using-dfs/)

给定一个连通图，检查该图是否为[二分图](https://www.geeksforgeeks.org/bipartite-graph/)。如果图着色可以使用两种颜色，使得集合中的顶点用相同的颜色着色，则二部图是可能的。请注意，可以使用两种颜色为偶数周期的周期图着色。例如，见下图。

![Bipartite2](img/fa0cedf028ebc150489065253b012dc3.png)

不可能用两种颜色给奇数周期的周期图着色。

![Bipartite3](img/a3ee6e7039d82a4ce6579be45994fd2f.png)

在之前的[帖子](https://www.geeksforgeeks.org/bipartite-graph/)中，已经讨论了使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的方法。在这篇文章中，已经实现了一种使用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的方法。

下面给出了检查图的二分性的算法。

*   使用*颜色[]* 数组，该数组为表示相反颜色的每个节点存储 0 或 1。
*   从任意节点调用函数 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
*   如果节点 u 以前没有被访问过，那么分配！将颜色[v]设置为颜色[u],并再次调用 DFS 来访问连接到 u 的节点。
*   如果在任何一点上，颜色[u]等于颜色[v]，那么这个节点就不是二分的。
*   修改 DFS 函数，使其在最后返回一个布尔值。

下面是上述方法的实现:

## C++

```
// C++ program to check if a connected
// graph is bipartite or not suing DFS
#include <bits/stdc++.h>
using namespace std;

// function to store the connected nodes
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// function to check whether a graph is bipartite or not
bool isBipartite(vector<int> adj[], int v,
                 vector<bool>& visited, vector<int>& color)
{

    for (int u : adj[v]) {

        // if vertex u is not explored before
        if (visited[u] == false) {

            // mark present vertic as visited
            visited[u] = true;

            // mark its color opposite to its parent
            color[u] = !color[v];

            // if the subtree rooted at vertex v is not bipartite
            if (!isBipartite(adj, u, visited, color))
                return false;
        }

        // if two adjacent are colored with same color then
        // the graph is not bipartite
        else if (color[u] == color[v])
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    // no of nodes
    int N = 6;

    // to maintain the adjacency list of graph
    vector<int> adj[N + 1];

    // to keep a check on whether
    // a node is discovered or not
    vector<bool> visited(N + 1);

    // to color the vertices
    // of graph with 2 color
    vector<int> color(N + 1);

    // adding edges to the graph
    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    addEdge(adj, 4, 5);
    addEdge(adj, 5, 6);
    addEdge(adj, 6, 1);

    // marking the source node as visited
    visited[1] = true;

    // marking the source node with a color
    color[1] = 0;

    // Function to check if the graph
    // is Bipartite or not
    if (isBipartite(adj, 1, visited, color)) {
        cout << "Graph is Bipartite";
    }
    else {
        cout << "Graph is not Bipartite";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a connected
// graph is bipartite or not suing DFS
import java.util.*;

class GFG{

// Function to store the connected nodes
static void addEdge(ArrayList<ArrayList<Integer>> adj,
                    int u, int v)
{
    adj.get(u).add(v);
    adj.get(v).add(u);
}

// Function to check whether a
// graph is bipartite or not
static boolean isBipartite(ArrayList<ArrayList<Integer>> adj,
                           int v, boolean visited[],
                           int color[])
{
    for(int u : adj.get(v))
    {

        // If vertex u is not explored before
        if (visited[u] == false)
        {

            // Mark present vertic as visited
            visited[u] = true;

            // Mark its color opposite to its parent
            color[u] = 1 - color[v];

            // If the subtree rooted at vertex
            // v is not bipartite
            if (!isBipartite(adj, u, visited, color))
                return false;
        }

        // If two adjacent are colored with
        // same color then the graph is
        // not bipartite
        else if (color[u] == color[v])
            return false;
    }
    return true;
}

// Driver Code
public static void main(String args[])
{

    // No of nodes
    int N = 6;

    // To maintain the adjacency list of graph
    ArrayList<
    ArrayList<Integer>> adj = new ArrayList<
                                  ArrayList<Integer>>(N + 1);

    // Initialize all the vertex
    for(int i = 0; i <= N; i++)
    {
        adj.add(new ArrayList<Integer>());
    }

    // To keep a check on whether
    // a node is discovered or not
    boolean visited[] = new boolean[N + 1];

    // To color the vertices
    // of graph with 2 color
    int color[] = new int[N + 1];

    // The value '-1' of colorArr[i] is
    // used to indicate that no color is
    // assigned to vertex 'i'. The value
    // 1 is used to indicate first color
    // is assigned and value 0 indicates 
    // second color is assigned.
    Arrays.fill(color, -1);

    // Adding edges to the graph
    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    addEdge(adj, 4, 5);
    addEdge(adj, 5, 6);
    addEdge(adj, 6, 1);

    // Marking the source node as visited
    visited[1] = true;

    // Marking the source node with a color
    color[1] = 0;

    // Function to check if the graph
    // is Bipartite or not
    if (isBipartite(adj, 1, visited, color))
    {
        System.out.println("Graph is Bipartite");
    }
    else
    {
        System.out.println("Graph is not Bipartite");
    }
}
}

// This code is contributed by adityapande88
```

## 蟒蛇 3

```
# Python3 program to check if a connected
# graph is bipartite or not suing DFS

# Function to store the connected nodes
def addEdge(adj, u, v):

    adj[u].append(v)
    adj[v].append(u)

# Function to check whether a graph is
# bipartite or not
def isBipartite(adj, v, visited, color):

    for u in adj[v]:

        # If vertex u is not explored before
        if (visited[u] == False):

            # Mark present vertic as visited
            visited[u] = True

            # Mark its color opposite to its parent
            color[u] = not color[v]

            # If the subtree rooted at vertex v
            # is not bipartite
            if (not isBipartite(adj, u,
                                visited, color)):
                return false

        # If two adjacent are colored with
        # same color then the graph is not
        # bipartite
        elif (color[u] == color[v]):
            return Talse

    return True

# Driver Code
if __name__=='__main__':

    # No of nodes
    N = 6

    # To maintain the adjacency list of graph
    adj = [[] for i in range(N + 1)]

    # To keep a check on whether
    # a node is discovered or not
    visited = [0 for i in range(N + 1)]

    # To color the vertices
    # of graph with 2 color
    color = [0 for i in range(N + 1)]

    # Adding edges to the graph
    addEdge(adj, 1, 2)
    addEdge(adj, 2, 3)
    addEdge(adj, 3, 4)
    addEdge(adj, 4, 5)
    addEdge(adj, 5, 6)
    addEdge(adj, 6, 1)

    # Marking the source node as visited
    visited[1] = True

    # Marking the source node with a color
    color[1] = 0

    # Function to check if the graph
    # is Bipartite or not
    if (isBipartite(adj, 1, visited, color)):
        print("Graph is Bipartite")
    else:
        print("Graph is not Bipartite")

# This code is contributed by rutvik_56
```

## C#

```
// C# program to check if a connected
// graph is bipartite or not suing DFS
using System;
using System.Collections.Generic;

class GFG{

// Function to store the connected nodes
static void addEdge(List<List<int>> adj,
                    int u, int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

// Function to check whether a
// graph is bipartite or not
static bool isBipartite(List<List<int>> adj,
                        int v, bool []visited,
                        int []color)
{
    foreach(int u in adj[v])
    {

        // If vertex u is not explored before
        if (visited[u] == false)
        {

            // Mark present vertic as visited
            visited[u] = true;

            // Mark its color opposite to its parent
            color[u] = 1 - color[v];

            // If the subtree rooted at vertex
            // v is not bipartite
            if (!isBipartite(adj, u, visited, color))
                return false;
        }

        // If two adjacent are colored with
        // same color then the graph is
        // not bipartite
        else if (color[u] == color[v])
            return false;
    }
    return true;
}

// Driver Code
public static void Main(String []args)
{

    // No of nodes
    int N = 6;

    // To maintain the adjacency list of graph
    List<List<int>> adj = new List<List<int>>(N + 1);

    // Initialize all the vertex
    for(int i = 0; i <= N; i++)
    {
        adj.Add(new List<int>());
    }

    // To keep a check on whether
    // a node is discovered or not
    bool []visited = new bool[N + 1];

    // To color the vertices
    // of graph with 2 color
    int []color = new int[N + 1];

    // The value '-1' of colorArr[i] is
    // used to indicate that no color is
    // assigned to vertex 'i'. The value
    // 1 is used to indicate first color
    // is assigned and value 0 indicates 
    // second color is assigned.
    for(int i = 0; i <= N; i++)  
        color[i] = -1;

    // Adding edges to the graph
    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    addEdge(adj, 4, 5);
    addEdge(adj, 5, 6);
    addEdge(adj, 6, 1);

    // Marking the source node as visited
    visited[1] = true;

    // Marking the source node with a color
    color[1] = 0;

    // Function to check if the graph
    // is Bipartite or not
    if (isBipartite(adj, 1, visited, color))
    {
        Console.WriteLine("Graph is Bipartite");
    }
    else
    {
        Console.WriteLine("Graph is not Bipartite");
    }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check if a connected
// graph is bipartite or not suing DFS

// function to store the connected nodes
function addEdge(adj, u, v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// function to check whether a graph is bipartite or not
function isBipartite(adj, v, visited, color)
{

    adj[v].forEach(u => {

        // if vertex u is not explored before
        if (visited[u] == false) {

            // mark present vertic as visited
            visited[u] = true;

            // mark its color opposite to its parent
            color[u] = !color[v];

            // if the subtree rooted at vertex v is not bipartite
            if (!isBipartite(adj, u, visited, color))
                return false;
        }

        // if two adjacent are colored with same color then
        // the graph is not bipartite
        else if (color[u] == color[v])
            return false;
    });
    return true;
}

// Driver Code
// no of nodes
var N = 6;
// to maintain the adjacency list of graph
var adj = Array.from(Array(N+1), ()=>Array());
// to keep a check on whether
// a node is discovered or not
var visited = Array(N+1);;
// to color the vertices
// of graph with 2 color
var color = Array(N+1);
// adding edges to the graph
addEdge(adj, 1, 2);
addEdge(adj, 2, 3);
addEdge(adj, 3, 4);
addEdge(adj, 4, 5);
addEdge(adj, 5, 6);
addEdge(adj, 6, 1);
// marking the source node as visited
visited[1] = true;
// marking the source node with a color
color[1] = 0;
// Function to check if the graph
// is Bipartite or not
if (isBipartite(adj, 1, visited, color)) {
    document.write( "Graph is Bipartite");
}
else {
    document.write( "Graph is not Bipartite");
}

</script>
```

**Output:** 

```
Graph is Bipartite
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)