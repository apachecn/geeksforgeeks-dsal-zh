# 查询以查找包含给定边的树中的最短路径数

> 原文：[https://www.geeksforgeeks.org/queries-to-find-the-count-of-shortest-paths-in-a-tree-that-contains-a-given-edge/](https://www.geeksforgeeks.org/queries-to-find-the-count-of-shortest-paths-in-a-tree-that-contains-a-given-edge/)

给定一个[树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，其中 **N 个**顶点的编号从 **0** 到 **N – 1，M** 个边，以及 **Q** 个查询 形式为 **{U，V}，**，这样树中的 **U** 和 **V** 之间有直接的边。 每个查询的任务是从给定树（包含给定节点对之间的边）找到任何可能的无序顶点对之间的所有可能的[最短路径](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)。

**示例**：

> **输入**：N = 6，M [] = {{0，1}，{0，2}，{1，3}，{3，4}，{3，5}}，查询[ ] = {{1,3}，{0,2}}
> 0
> / \
> 1 2
> /
> 3
> / \
> 4 4 5
> **输出**：
> 9
> 5
> **说明**：
> 查询 1：边（1、3）位于路径中 {1、3），（1、3、4），（1、3、5），（0、3），（0、4），（0、5），（2、3），（2、4 ）和（2，5）。
> 查询 2：边（0，2）位于路径（2，0），（2，1），（2，3），（2，4）和（2，5）中。
> 
> **输入**：N = 6，M [] = {{0，1}，{0，2}，{2，3}，{1，4}，{1，5}}，查询[ ] = {{1,5}，{0,2}}
> 0
> / \
> 1 2
> / \ /
> 4 5 3
> **输出**：
> 5
> 8

**方法**：该问题可以根据以下观察结果解决：对于任何查询 **{U，V}，**，树中任何一对节点之间的最短路径将包含给定的边[ 如果节点之一位于 **U** 的子树中，而另一个节点位于其余树中，则 HTG4]（U，V）。 因此，所需的对数将是：

> 包含（U，V）作为边的最短路径计数= subtreeSize（U）*（N – subtreeSize（V））。

因此，请按照以下步骤解决问题：

*   从根节点开始在树上执行深度优先搜索遍历。

*   对于每个节点，将节点数存储在其子树（包括该节点）中。

*   遍历每个查询（U，V）并计算：

> min（subtreeSize（U），subtreeSize（V））*（N – min（subtreeSize（U），subtreeSize（V）））

下面是上述方法的实现：

## C++

```cpp

// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;

// Adjacency list to
// represent the tree
vector<int> tree[sz];

// Number of vertices
int n;

// Mark visited/ unvisited
// vertices
bool vis[sz];

// Stores the subtree size
// of the corresponding nodes
int subtreeSize[sz];

// Function to create an
// edge between two vertices
void addEdge(int a, int b)
{
    // Add a to b's list
    tree[a].push_back(b);

    // Add b to a's list
    tree[b].push_back(a);
}

// Function to perform DFS
void dfs(int x)
{
    // Mark the vertex
    // visited
    vis[x] = true;

    // Include the node in
    // the subtree
    subtreeSize[x] = 1;

    // Traverse all its children
    for (auto i : tree[x]) {
        if (!vis[i]) {
            dfs(i);
            subtreeSize[x]
                += subtreeSize[i];
        }
    }
}

// Function to print the
// required number of paths
void countPairs(int a, int b)
{
    int sub = min(subtreeSize[a],
                  subtreeSize[b]);

    cout << sub * (n - sub)
         << endl;
}

// Driver Code
int main()
{
    // Number of vertices
    n = 6;

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(3, 4);
    addEdge(3, 5);

    // Calling modified dfs function
    dfs(0);

    // Count pairs of vertices in the tree
    countPairs(1, 3);
    countPairs(0, 2);
    return 0;
}

```

## Java

```java

// Java implementation for 
// the above approach
import java.util.*;
class GFG{

static int sz = (int) 1e5;

// Adjacency list to
// represent the tree
static Vector<Integer> []tree = new Vector[sz];

// Number of vertices
static int n;

// Mark visited/ unvisited
// vertices
static boolean []vis = new boolean[sz];

// Stores the subtree size
// of the corresponding nodes
static int []subtreeSize = new int[sz];

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{
  // Add a to b's list
  tree[a].add(b);

  // Add b to a's list
  tree[b].add(a);
}

// Function to perform DFS
static void dfs(int x)
{
  // Mark the vertex
  // visited
  vis[x] = true;

  // Include the node in
  // the subtree
  subtreeSize[x] = 1;

  // Traverse all its children
  for (int i : tree[x]) 
  {
    if (!vis[i]) 
    {
      dfs(i);
      subtreeSize[x] += subtreeSize[i];
    }
  }
}

// Function to print the
// required number of paths
static void countPairs(int a, int b)
{
  int sub = Math.min(subtreeSize[a],
                     subtreeSize[b]);

  System.out.print(sub * (n - sub) + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Number of vertices
  n = 6;
  for (int i = 0; i < tree.length; i++)
    tree[i] = new Vector<Integer>();
  addEdge(0, 1);
  addEdge(0, 2);
  addEdge(1, 3);
  addEdge(3, 4);
  addEdge(3, 5);

  // Calling modified dfs function
  dfs(0);

  // Count pairs of vertices in the tree
  countPairs(1, 3);
  countPairs(0, 2);
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 implementation for 
# the above approach
sz = 100000

# Adjacency list to
# represent the tree
tree = [[] for i in range(sz)]

# Number of vertices
n = 0

# Mark visited/ unvisited
# vertices
vis = [False] * sz

# Stores the subtree size
# of the corresponding nodes
subtreeSize = [0 for i in range(sz)]

# Function to create an
# edge between two vertices
def addEdge(a, b):

    global tree

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Function to perform DFS
def dfs(x):

    # Mark the vertex
    # visited
    global vis
    global subtreeSize
    global tree
    vis[x] = True

    # Include the node in
    # the subtree
    subtreeSize[x] = 1

    # Traverse all its children
    for i in tree[x]:
        if (vis[i] == False):
            dfs(i)
            subtreeSize[x] += subtreeSize[i]

# Function to print the
# required number of paths
def countPairs(a, b):

    global subtreeSize
    sub = min(subtreeSize[a],
              subtreeSize[b])

    print(sub * (n - sub))

# Driver Code
if __name__ == '__main__':

    # Number of vertices
    n = 6

    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 3)
    addEdge(3, 4)
    addEdge(3, 5)

    # Calling modified dfs function
    dfs(0)

    # Count pairs of vertices in the tree
    countPairs(1, 3)
    countPairs(0, 2)

# This code is contributed by SURENDRA_GANGWAR

```

## C#

```cs

// C# implementation for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static int sz = (int) 1e5;

// Adjacency list to
// represent the tree
static List<int> []tree = 
            new List<int>[sz];

// Number of vertices
static int n;

// Mark visited/ unvisited
// vertices
static bool []vis = new bool[sz];

// Stores the subtree size
// of the corresponding nodes
static int []subtreeSize = new int[sz];

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{
  // Add a to b's list
  tree[a].Add(b);

  // Add b to a's list
  tree[b].Add(a);
}

// Function to perform DFS
static void dfs(int x)
{
  // Mark the vertex
  // visited
  vis[x] = true;

  // Include the node in
  // the subtree
  subtreeSize[x] = 1;

  // Traverse all its children
  foreach (int i in tree[x]) 
  {
    if (!vis[i]) 
    {
      dfs(i);
      subtreeSize[x] += subtreeSize[i];
    }
  }
}

// Function to print the
// required number of paths
static void countPairs(int a, int b)
{
  int sub = Math.Min(subtreeSize[a],
                     subtreeSize[b]);

  Console.Write(sub * (n - sub) + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Number of vertices
  n = 6;
  for (int i = 0; i < tree.Length; i++)
    tree[i] = new List<int>();
  addEdge(0, 1);
  addEdge(0, 2);
  addEdge(1, 3);
  addEdge(3, 4);
  addEdge(3, 5);

  // Calling modified dfs function
  dfs(0);

  // Count pairs of vertices in the tree
  countPairs(1, 3);
  countPairs(0, 2);
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
9
5

```

**时间复杂度**：O（N + M + Q）

**辅助空间**：`O(n)`



* * *

* * *



