# 使用给定的操作

最大限度地降低为无向图的所有顶点着色的成本

> 原文： [https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph-using-given-operation/](https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph-using-given-operation/)

给定两个整数`V`和`E`，它们表示无向图 **G（V，E）**的顶点和边的数量，边的列表 **EdgeList** 和代表每个节点着色成本的数组 **A []** ，任务是使用以下操作找到着色图形的最低成本：

> 对**节点**进行着色时，可以从其访问的所有节点都进行着色，而无需任何额外费用。

**示例**：

> **输入**：V = 6，E = 5，A [] = {12，25，8，11，10，7}，EdgeList = {{1，2}，{1，3}，{ 3，2}，{2，5}，{4，6}}
> **输出**：15
> **说明**：
> 为顶点 3 着色 在`8`的成本上，顶点{1、2、5}无需附加成本即可着色。
> 在以成本`7`为顶点 6 着色时，唯一剩余的顶点{4}也被着色。
> 因此，最低费用= 8 + 7 = 15。
> 
> **输入**：V = 7，E = 6，A [] = {3，5，8，6，9，11，10}，EdgeList = {{1，4}，{2，1} ，{2，7}，{3，4}，{3，5}，{5，6}}
> **输出**：5

**方法**：[

]请按照以下步骤解决问题：

*   从给定节点可到达的所有节点形成[连接组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)。

*   因此，对于每个连通组件，请使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，找到图的连接组件中的最小成本节点。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to find the minimum
// cost to color all vertices of an
// Undirected Graph
#include <bits/stdc++.h>
using namespace std;

#define MAX 10

vector<int> adj[MAX];

// Function to add edge in the
// given graph
void addEdge(int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
void dfs(int v, int cost[], bool vis[],
         int& min_cost_node)
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node
        = min(min_cost_node, cost[v - 1]);

    for (int i = 0; i < adj[v].size(); i++) {

        // Recur for all connected nodes
        if (vis[adj[v][i]] == false) {
            dfs(adj[v][i], cost, vis,
                min_cost_node);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
int minimumCost(int V, int cost[])
{

    // Marks if a vertex is
    // visited or not
    bool vis[V + 1];

    // Initialize all vertices as unvisited
    memset(vis, false, sizeof(vis));
    int min_cost = 0;

    // Perform DFS traversal
    for (int i = 1; i <= V; i++) {

        // If vertex is not visited
        if (!vis[i]) {
            int min_cost_node = INT_MAX;
            dfs(i, cost, vis, min_cost_node);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the final cost
    return min_cost;
}
// Driver Code
int main()
{
    int V = 6, E = 5;
    int cost[] = { 12, 25, 8, 11, 10, 7 };
    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    cout << min_cost << endl;

    return 0;
}

```

## Java

```java

// Java program to find the minimum
// cost to color all vertices of an
// Undirected Graph
import java.util.*;

class GFG{

static final int MAX = 10;

@SuppressWarnings("unchecked")
static Vector<Integer> []adj = new Vector[MAX];

static int min_cost_node;

// Function to add edge in the
// given graph
static void addEdge(int u, int v)
{
    adj[u].add(v);
    adj[v].add(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
static void dfs(int v, int cost[], boolean vis[])
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node = Math.min(min_cost_node,
                             cost[v - 1]);

    for(int i = 0; i < adj[v].size(); i++)
    {

        // Recur for all connected nodes
        if (vis[adj[v].get(i)] == false)
        {
            dfs(adj[v].get(i), cost, vis);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
static int minimumCost(int V, int cost[])
{

    // Marks if a vertex is
    // visited or not
    boolean []vis = new boolean[V + 1];

    // Initialize all vertices as unvisited
    Arrays.fill(vis, false);
    int min_cost = 0;

    // Perform DFS traversal
    for(int i = 1; i <= V; i++)
    {

        // If vertex is not visited
        if (!vis[i]) 
        {
            min_cost_node = Integer.MAX_VALUE;
            dfs(i, cost, vis);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the final cost
    return min_cost;
}

// Driver Code
public static void main(String[] args)
{
    int V = 6, E = 5;
    int cost[] = { 12, 25, 8, 11, 10, 7 };

    for(int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    System.out.print(min_cost + "\n");
}
}

// This code is contributed by 29AjayKumar

```

## Python

```py

# Python3 program to find the minimum
# cost to color all vertices of an
# Undirected Graph
import sys

MAX = 10

adj = [[] for i in range(MAX)]

# Function to add edge in the
# given graph
def addEdge(u, v):

    adj[u].append(v)
    adj[v].append(u)

# Function to perform DFS traversal and
# find the node with minimum cost
def dfs(v, cost, vis, min_cost_node):

    vis[v] = True

    # Update the minimum cost
    min_cost_node = min(min_cost_node, 
                        cost[v - 1])

    for i in range(len(adj[v])):

        # Recur for all connected nodes
        if (vis[adj[v][i]] == False):
            min_cost_node = dfs(adj[v][i], 
                                cost, vis, 
                                min_cost_node)

    return min_cost_node

# Function to calculate and return
# the minimum cost of coloring all
# vertices of the Undirected Graph
def minimumCost(V, cost):

    # Marks if a vertex is
    # visited or not
    vis = [False for i in range(V + 1)]

    min_cost = 0

    # Perform DFS traversal
    for i in range(1, V + 1):

        # If vertex is not visited
        if (not vis[i]):
            min_cost_node = sys.maxsize
            min_cost_node = dfs(i, cost, vis,
                                min_cost_node)

            # Update minimum cost
            min_cost += min_cost_node

    # Return the final cost
    return min_cost

# Driver Code
if __name__=="__main__":

    V = 6
    E = 5
    cost = [ 12, 25, 8, 11, 10, 7 ]

    addEdge(1, 2)
    addEdge(1, 3)
    addEdge(3, 2)
    addEdge(2, 5)
    addEdge(4, 6)

    min_cost = minimumCost(V, cost)

    print(min_cost)

# This code is contributed by rutvik_56

```

## C#

```cs

// C# program to find the minimum
// cost to color all vertices of an
// Undirected Graph
using System;
using System.Collections.Generic;

class GFG{

static readonly int MAX = 10;
static List<int> []adj = new List<int>[MAX];
static int min_cost_node;

// Function to add edge in the
// given graph
static void addEdge(int u, int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
static void dfs(int v, int []cost, bool []vis)
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node = Math.Min(min_cost_node,
                             cost[v - 1]);

    for(int i = 0; i < adj[v].Count; i++)
    {

        // Recur for all connected nodes
        if (vis[adj[v][i]] == false)
        {
            dfs(adj[v][i], cost, vis);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
static int minimumCost(int V, int []cost)
{

    // Marks if a vertex is
    // visited or not
    bool []vis = new bool[V + 1];

    int min_cost = 0;

    // Perform DFS traversal
    for(int i = 1; i <= V; i++)
    {

        // If vertex is not visited
        if (!vis[i]) 
        {
            min_cost_node = int.MaxValue;
            dfs(i, cost, vis);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the readonly cost
    return min_cost;
}

// Driver Code
public static void Main(String[] args)
{
    int V = 6;
    int []cost = { 12, 25, 8, 11, 10, 7 };

    for(int i = 0; i < adj.Length; i++)
        adj[i] = new List<int>();

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    Console.Write(min_cost + "\n");
}
}

// This code is contributed by Amit Katiyar 

```

**输出**：

```
15

```

***时间复杂度**：`O(V + E)`*

***辅助空间**：O（V）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。