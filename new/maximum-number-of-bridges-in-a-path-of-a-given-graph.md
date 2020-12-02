# 给定图

的路径中的最大桥数

> 原文： [https://www.geeksforgeeks.org/maximum-number-of-bridges-in-a-path-of-a-given-graph/](https://www.geeksforgeeks.org/maximum-number-of-bridges-in-a-path-of-a-given-graph/)

给定[无向图](https://www.geeksforgeeks.org/graph-and-its-representations/)，任务是计算给定图的任意两个顶点之间的[桥](https://www.geeksforgeeks.org/bridge-in-a-graph/)的最大数量。
**范例**：

```
Input: 
Graph
1 ------- 2 ------- 3 -------- 4
          |         |
          |         |
          5 ------- 6
Output: 2 
Explanation: 
There are 2 bridges, (1 - 2)
and (3 - 4), in the path from 1 to 4.

Input: 
Graph:
1 ------- 2 ------- 3 ------- 4
Output: 3 
Explanation: 
There are 3 bridges, (1 - 2), (2 - 3)
and (3 - 4) in the path from 1 to 4.

```

**方法**：[
]请按照以下步骤解决问题：

*   [找到图中的所有桥](https://www.geeksforgeeks.org/bridge-in-a-graph/)并将它们存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
*   删除所有的桥将图形缩小为较小的分量。
*   这些小组件没有任何桥接，它们是[弱连接组件](https://www.geeksforgeeks.org/convert-undirected-graph-directed-graph-minimize-disconnected-component/)，其中没有桥接。
*   生成由以桥为边的桥连接的节点组成的树。
*   现在，任何节点之间路径中的最大桥等于该树的直径。
*   因此，找到该树的[直径](https://www.geeksforgeeks.org/diameter-tree-using-dfs/)并将其打印为答案。

以下是上述方法的实现

## C++

```cpp

// C++ program to find the
// maximum number of bridges
// in any path of the given graph

#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 5;

// Stores the nodes
// and their connections
vector<vector<int> > v(N);

// Store the tree with
// Bridges as the edges
vector<vector<int> > g(N);

// Stores the visited nodes
vector<bool> vis(N, 0);

// for finding bridges
vector<int> in(N), low(N);

// for Disjoint Set Union
vector<int> parent(N), rnk(N);
// for storing actaul bridges
vector<pair<int, int> > bridges;

// Stores the number of
// nodes and edges
int n, m;
// For finding bridges
int timer = 0;

int find_set(int a)
{
    // Function to find root of
    // the component in which
    // A lies
    if (parent[a] == a)
        return a;

    // Doing path compression
    return parent[a]
           = find_set(parent[a]);
}

void union_set(int a, int b)
{
    // Function to do union
    // between a and b
    int x = find_set(a), y = find_set(b);

    // If both are already in the
    // same component
    if (x == y)
        return;

    // If both have same rank,
    // then increase anyone's rank
    if (rnk[x] == rnk[y])
        rnk[x]++;

    if (rnk[y] > rnk[x])
        swap(x, y);

    parent[y] = x;
}

// Function to find bridges
void dfsBridges(int a, int par)
{
    vis[a] = 1;
    // Initialize in time and
    // low value
    in[a] = low[a] = timer++;

    for (int i v[a]) {

        if (i == par)
            continue;

        if (vis[i])

            // Update the low value
            // of the parent
            low[a] = min(low[a], in[i]);
        else {

            // Perform DFS on its child
            // updating low if the child
            // has connection with any
            // ancestor
            dfsBridges(i, a);

            low[a] = min(low[a], low[i]);

            if (in[a] < low[i])

                // Bridge found
                bridges.push_back(make_pair(i, a));

            // Otherwise
            else

                // Find union between parent
                // and child as they
                // are in same component
                union_set(i, a);
        }
    }
}

// Function to find diameter of the
// tree for storing max two depth child
int dfsDiameter(int a, int par, int& diameter)
{
    int x = 0, y = 0;
    for (int i g[a]) {
        if (i == par)
            continue;

        int mx = dfsDiameter(i, a, diameter);

        // Finding max two depth
        // from its children
        if (mx > x) {
            y = x;
            x = mx;
        }
        else if (mx > y)
            y = mx;
    }

    // Update diameter with the
    // sum of max two depths
    diameter = max(diameter, x + y);

    // Return the maximum depth
    return x + 1;
}

// Function to find maximum
// bridges bwtween
// any two nodes
int findMaxBridges()
{

    for (int i = 0; i <= n; i++) {
        parent[i] = i;
        rnk[i] = 1;
    }

    // DFS to find bridges
    dfsBridges(1, 0);

    // If no bridges are found
    if (bridges.empty())
        return 0;

    int head = -1;

    // Iterate over all bridges
    for (auto& i bridges) {

        // Find the endpoints
        int a = find_set(i.first);
        int b = find_set(i.second);

        // Generate the tree with
        // bridges as the edges
        g[a].push_back(b);
        g[b].push_back(a);

        // Update the head
        head = a;
    }

    int diameter = 0;
    dfsDiameter(head, 0, diameter);

    // Return the diameter
    return diameter;
}

// Driver Code
int main()
{
    /*

    Graph =>

        1 ---- 2 ---- 3 ---- 4
               |      | 
               5 ---- 6 
    */

    n = 6, m = 6;

    v[1].push_back(2);
    v[2].push_back(1);
    v[2].push_back(3);
    v[3].push_back(2);
    v[2].push_back(5);
    v[5].push_back(2);
    v[5].push_back(6);
    v[6].push_back(5);
    v[6].push_back(3);
    v[3].push_back(6);
    v[3].push_back(4);
    v[4].push_back(4);

    int ans = findMaxBridges();

    cout << ans << endl;

    return 0;
}

```

## Java

```java

// Java program to find the
// maximum number of bridges
// in any path of the given graph
import java.util.*;
class GFG{

static int N = (int)1e5 + 5;

// Stores the nodes
// and their connections
static Vector<Integer> []v = 
       new Vector[N];

// Store the tree with
// Bridges as the edges
static Vector<Integer> []g = 
       new Vector[N];

// Stores the visited nodes
static boolean []vis = 
       new boolean[N];

// For finding bridges
static int []in = new int[N];
static int []low = new int[N];

// for Disjoint Set Union
static int []parent = new int[N];
static int []rnk = new int[N];

// For storing actaul bridges
static Vector<pair> bridges = 
       new Vector<>();

// Stores the number of
// nodes and edges
static int n, m;

// For finding bridges
static int timer = 0;
static int diameter;

static class pair
{ 
  int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} 

static void swap(int x, 
                 int y) 
{
  int temp = x;
  x = y;
  y = temp;
}

static int find_set(int a)
{
  // Function to find root of
  // the component in which
  // A lies
  if (parent[a] == a)
    return a;

  // Doing path compression
  return parent[a] = 
         find_set(parent[a]);
}

static void union_set(int a, int b)
{
  // Function to do union
  // between a and b
  int x = find_set(a), 
      y = find_set(b);

  // If both are already 
  // in the same component
  if (x == y)
    return;

  // If both have same rank,
  // then increase anyone's rank
  if (rnk[x] == rnk[y])
    rnk[x]++;

  if (rnk[y] > rnk[x])
    swap(x, y);

  parent[y] = x;
}

// Function to find bridges
static void dfsBridges(int a, 
                       int par)
{
  vis[a] = true;

  // Initialize in time and
  // low value
  in[a] = low[a] = timer++;

  for (int i : v[a]) 
  {
    if (i == par)
      continue;

    if (vis[i])

      // Update the low value
      // of the parent
      low[a] = Math.min(low[a], 
                        in[i]);
    else
    {
      // Perform DFS on its child
      // updating low if the child
      // has connection with any
      // ancestor
      dfsBridges(i, a);

      low[a] = Math.min(low[a], 
                        low[i]);

      if (in[a] < low[i])

        // Bridge found
        bridges.add(new pair(i, a));

      // Otherwise
      else

        // Find union between parent
        // and child as they
        // are in same component
        union_set(i, a);
    }
  }
}

// Function to find diameter 
// of the tree for storing 
// max two depth child
static int dfsDiameter(int a, 
                       int par)
{
  int x = 0, y = 0;
  for (int i : g[a]) 
  {
    if (i == par)
      continue;

    int mx = dfsDiameter(i, a);

    // Finding max two depth
    // from its children
    if (mx > x) 
    {
      y = x;
      x = mx;
    }
    else if (mx > y)
      y = mx;
  }

  // Update diameter with the
  // sum of max two depths
  diameter = Math.max(diameter, 
                      x + y);

  // Return the maximum depth
  return x + 1;
}

// Function to find maximum
// bridges bwtween
// any two nodes
static int findMaxBridges()
{
  for (int i = 0; i <= n; i++) 
  {
    parent[i] = i;
    rnk[i] = 1;
  }

  // DFS to find bridges
  dfsBridges(1, 0);

  // If no bridges are found
  if (bridges.isEmpty())
    return 0;

  int head = -1;

  // Iterate over all bridges
  for (pair i : bridges) 
  {
    // Find the endpoints
    int a = find_set(i.first);
    int b = find_set(i.second);

    // Generate the tree with
    // bridges as the edges
    g[a].add(b);
    g[b].add(a);

    // Update the head
    head = a;
  }

  diameter = 0;
  dfsDiameter(head, 0);

  // Return the diameter
  return diameter;
}

// Driver Code
public static void main(String[] args)
{
  /*

    Graph =>

        1 ---- 2 ---- 3 ---- 4
               |      | 
               5 ---- 6 
    */

  n = 6;
  m = 6;

  for (int i = 0; i < v.length; i++)
    v[i] = new Vector<Integer>();

  for (int i = 0; i < g.length; i++)
    g[i] = new Vector<Integer>();

  v[1].add(2);
  v[2].add(1);
  v[2].add(3);
  v[3].add(2);
  v[2].add(5);
  v[5].add(2);
  v[5].add(6);
  v[6].add(5);
  v[6].add(3);
  v[3].add(6);
  v[3].add(4);
  v[4].add(4);

  int ans = findMaxBridges();
  System.out.print(ans + "\n");
}
}

// This code is contributed by Princi Singh

```

## C#

```cs

// C# program to find the
// maximum number of bridges
// in any path of the given graph
using System;
using System.Collections.Generic;
class GFG{

static int N = (int)1e5 + 5;

// Stores the nodes
// and their connections
static List<int> []v = 
       new List<int>[N];

// Store the tree with
// Bridges as the edges
static List<int> []g = 
       new List<int>[N];

// Stores the visited nodes
static bool []vis = 
       new bool[N];

// For finding bridges
static int []init = new int[N];
static int []low = new int[N];

// for Disjoint Set Union
static int []parent = new int[N];
static int []rnk = new int[N];

// For storing actaul bridges
static List<pair> bridges = 
       new List<pair>();

// Stores the number of
// nodes and edges
static int n, m;

// For finding bridges
static int timer = 0;
static int diameter;

class pair
{ 
  public int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} 

static void swap(int x, 
                 int y) 
{
  int temp = x;
  x = y;
  y = temp;
}

static int find_set(int a)
{
  // Function to find root of
  // the component in which
  // A lies
  if (parent[a] == a)
    return a;

  // Doing path compression
  return parent[a] = 
         find_set(parent[a]);
}

static void union_set(int a, 
                      int b)
{
  // Function to do union
  // between a and b
  int x = find_set(a), 
      y = find_set(b);

  // If both are already 
  // in the same component
  if (x == y)
    return;

  // If both have same rank,
  // then increase anyone's rank
  if (rnk[x] == rnk[y])
    rnk[x]++;

  if (rnk[y] > rnk[x])
    swap(x, y);

  parent[y] = x;
}

// Function to find bridges
static void dfsBridges(int a, 
                       int par)
{
  vis[a] = true;

  // Initialize in time and
  // low value
  init[a] = low[a] = timer++;

  foreach (int i in v[a]) 
  {
    if (i == par)
      continue;

    if (vis[i])

      // Update the low value
      // of the parent
      low[a] = Math.Min(low[a], 
                        init[i]);
    else
    {
      // Perform DFS on its child
      // updating low if the child
      // has connection with any
      // ancestor
      dfsBridges(i, a);

      low[a] = Math.Min(low[a], 
                        low[i]);

      if (init[a] < low[i])

        // Bridge found
        bridges.Add(new pair(i, a));

      // Otherwise
      else

        // Find union between parent
        // and child as they
        // are in same component
        union_set(i, a);
    }
  }
}

// Function to find diameter 
// of the tree for storing 
// max two depth child
static int dfsDiameter(int a, 
                       int par)
{
  int x = 0, y = 0;
  foreach (int i in g[a]) 
  {
    if (i == par)
      continue;

    int mx = dfsDiameter(i, a);

    // Finding max two depth
    // from its children
    if (mx > x) 
    {
      y = x;
      x = mx;
    }
    else if (mx > y)
      y = mx;
  }

  // Update diameter with the
  // sum of max two depths
  diameter = Math.Max(diameter, 
                      x + y);

  // Return the 
  // maximum depth
  return x + 1;
}

// Function to find maximum
// bridges bwtween
// any two nodes
static int findMaxBridges()
{
  for (int i = 0; i <= n; i++) 
  {
    parent[i] = i;
    rnk[i] = 1;
  }

  // DFS to find bridges
  dfsBridges(1, 0);

  // If no bridges are found
  if (bridges.Count == 0)
    return 0;

  int head = -1;

  // Iterate over all bridges
  foreach (pair i in bridges) 
  {
    // Find the endpoints
    int a = find_set(i.first);
    int b = find_set(i.second);

    // Generate the tree with
    // bridges as the edges
    g[a].Add(b);
    g[b].Add(a);

    // Update the head
    head = a;
  }

  diameter = 0;
  dfsDiameter(head, 0);

  // Return the diameter
  return diameter;
}

// Driver Code
public static void Main(String[] args)
{
  /*

    Graph =>

        1 ---- 2 ---- 3 ---- 4
               |      | 
               5 ---- 6 
    */

  n = 6;
  m = 6;

  for (int i = 0; i < v.Length; i++)
    v[i] = new List<int>();

  for (int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  v[1].Add(2);
  v[2].Add(1);
  v[2].Add(3);
  v[3].Add(2);
  v[2].Add(5);
  v[5].Add(2);
  v[5].Add(6);
  v[6].Add(5);
  v[6].Add(3);
  v[3].Add(6);
  v[3].Add(4);
  v[4].Add(4);

  int ans = findMaxBridges();
  Console.Write(ans + "\n");
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
2

```

**时间复杂度**：O（N + M）
**辅助空间**：O（N + M）

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。