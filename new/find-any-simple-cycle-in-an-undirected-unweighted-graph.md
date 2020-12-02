# 在无向非加权图

中查找任何简单周期

> 原文： [https://www.geeksforgeeks.org/find-any-simple-cycle-in-an-undirected-unweighted-graph/](https://www.geeksforgeeks.org/find-any-simple-cycle-in-an-undirected-unweighted-graph/)

给定一个无向且无权连接的[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，在该图中找到一个简单的循环（如果存在）。

**简单循环**：

> 简单循环是图形中没有重复顶点的循环（起始和结束顶点除外）。
> 
> 基本上，如果一个周期不能分解为两个或多个周期，则这是一个简单的周期。
> 为更好地理解，请参考下图：
> 
> ![](img/c4fc69541412b75755fc43c24db496a4.png)
> 
> 上图中的图形说明了循环 1-> 2-> 3-> 4-> 1 不是一个简单的循环
> ，因为它可以分为 2 个简单的循环 1-> 3-> 4-> 1 和 1-> 2-> 3-> 1。

**示例**：

> **输入**：edge [] = {（（1，2），（2，3），（2，4），（3，4）}
> 
> ![](img/4529a6a10649529e13046bd11439f66f.png)
> 
> **输出**：2 = > 3 = > 4 = > 2
> **说明**：
> 该图只有一个长度为 3 的循环，即 简单的周期。
> 
> **输入**：edge [] = {（1、2），（2、3），（3、4），（1、4），（1、3）}
> 
> ![](img/ce5db82ffb78facb03afd0ac5131f99c.png)
> 
> **输出**：1 = > 3 = > 4 = > 1

**方法**：的想法是[检查图形是否包含循环](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)。 只需使用 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 即可完成。
现在，如果图形包含一个循环，我们可以从 DFS 本身获取该循环的**最终顶点**（例如 a 和 b）。 现在，如果我们从 a 到 b 运行 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) （忽略 a 和 b 之间的直接边），我们将能够获得从 a 到 b 的最短路径，这将为我们提供 **最短周期，其中包含**点`a`和`b`。 使用父数组可以轻松跟踪路径。 **这个最短的周期将是一个简单的周期**。

#### **最短周期将是一个简单周期的证明**：

我们可以用矛盾来证明这一点。 假设这个周期内还有另一个简单的周期。 这意味着内部简单循环的长度较短，因此可以说从 a 到 b 的路径更短。 但是我们发现使用 BFS 从 a 到 b 的最短路径。 因此，不再存在更短的路径，并且找到的路径最短。 因此，在我们发现的周期之内，不可能存在内部周期。
因此，该循环是**简单循环**。

下面是上述方法的实现：

## C ++

```

// C++ implementation to find the
// simple cycle in the given path

#include <bits/stdc++.h>
using namespace std;
#define MAXN 1005

// Declaration of the Graph
vector<vector<int> > adj(MAXN);

// Declaration of visited array
vector<bool> vis(MAXN);
int a, b;

// Function to add edges
// connecting 'a' and 'b'
// to the graph
void addedge(int a, int b)
{
    adj[a].push_back(b);
    adj[b].push_back(a);
}

// Function to detect if the
// graph contains a cycle or not
bool detect_cycle(int node, int par)
{
    // Marking the current node visited
    vis[node] = 1;
    // Traversing to the childs
    // of the current node
    // Simple DFS approach
    for (auto child : adj[node]) {
        if (vis[child] == 0) {
            if (detect_cycle(child, node))
                return true;
        }

        // Checking for a back-edge
        else if (child != par) {
            // A cycle is detected
            // Marking the end-vertices
            // of the cycle
            a = child;
            b = node;
            return true;
        }
    }
    return false;
}

vector<int> simple_cycle;

// Function to get the simple cycle from the
// end-vertices of the cycle we found from DFS
void find_simple_cycle(int a, int b)
{
    // Parent array to get the path
    vector<int> par(MAXN, -1);

    // Queue for BFS
    queue<int> q;
    q.push(a);
    bool ok = true;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        vis[node] = 1;
        for (auto child : adj[node]) {
            if (node == a && child == b)
                // Ignoring the direct edge
                // between a and b
                continue;

            if (vis[child] == 0) {
                // Updating the parent array
                par[child] = node;

                if (child == b) {
                    // If b is reached,
                    // we've found the
                    // shortest path from
                    // a to b already
                    ok = false;
                    break;
                }
                q.push(child);
                vis[child] = 1;
            }
        }
        // If required task is done
        if (ok == false)
            break;
    }

    // Cycle starting from a
    simple_cycle.push_back(a);
    int x = b;

    // Until we reach a again
    while (x != a) {
        simple_cycle.push_back(x);
        x = par[x];
    }
}

// Driver Code
int main()
{

    // Creating the graph
    addedge(1, 2);
    addedge(2, 3);
    addedge(3, 4);
    addedge(4, 1);
    addedge(1, 3);

    if (detect_cycle(1, -1) == true) {
        // If cycle is present

        // Resetting the visited array
        // for simple cycle finding
        vis = vector<bool>(MAXN, false);
        find_simple_cycle(a, b);

        // Printing the simple cycle
        cout << "A simple cycle: ";
        for (auto& node : simple_cycle) {
            cout << node << " => ";
        }
        cout << a;
        cout << "\n";
    }
    else {
        cout << "The Graph doesn't "
             << "contain a cycle.\n";
    }

    return 0;
}

```

## 爪哇

```

// Java implementation to 
// find the simple cycle 
// in the given path
import java.util.*;
class GFG{

  static final int MAXN = 1005;

// Declaration of the 
// Graph
static Vector<Integer> []adj =
              new Vector[MAXN];

// Declaration of visited 
// array
static boolean []vis = 
       new boolean[MAXN];
static int a, b;

// Function to add edges
// connecting 'a' and 'b'
// to the graph
static void addedge(int a, 
                    int b)
{
  adj[a].add(b);
  adj[b].add(a);
}

// Function to detect if the
// graph contains a cycle or not
static boolean detect_cycle(int node, 
                            int par)
{
  // Marking the current 
  // node visited
  vis[node] = true;

  // Traversing to the childs
  // of the current node
  // Simple DFS approach
  for (int child : adj[node]) 
  {
    if (vis[child] == false) 
    {
      if (detect_cycle(child, 
                       node))
        return true;
    }

    // Checking for a back-edge
    else if (child != par) 
    {
      // A cycle is detected
      // Marking the end-vertices
      // of the cycle
      a = child;
      b = node;
      return true;
    }
  }
  return false;
}

static Vector<Integer> simple_cycle =
              new Vector<>();

// Function to get the simple 
// cycle from the end-vertices 
//of the cycle we found from DFS
static void find_simple_cycle(int a, 
                              int b)
{
  // Parent array to get the path
  int []par = new int[MAXN];

  // Queue for BFS
  Queue<Integer> q = 
        new LinkedList<>();
  q.add(a);
  boolean ok = true;

  while (!q.isEmpty()) 
  {
    int node = q.peek();
    q.remove();
    vis[node] = true;

    for (int child : adj[node]) 
    {
      if (node == a && 
          child == b)
        // Ignoring the direct edge
        // between a and b
        continue;

      if (vis[child] == false) 
      {
        // Updating the parent 
        // array
        par[child] = node;

        if (child == b) 
        {
          // If b is reached,
          // we've found the
          // shortest path from
          // a to b already
          ok = false;
          break;
        }
        q.add(child);
        vis[child] = true;
      }
    }
    // If required task 
    // is done
    if (ok == false)
      break;
  }

  // Cycle starting from a
  simple_cycle.add(a);
  int x = b;

  // Until we reach 
  // a again
  while (x != a) 
  {
    simple_cycle.add(x);
    x = par[x];
  }
}

// Driver Code
public static void main(String[] args)
{
  for (int i = 0; i < adj.length; i++)
    adj[i] = new Vector<Integer>();

  // Creating the graph
  addedge(1, 2);
  addedge(2, 3);
  addedge(3, 4);
  addedge(4, 1);
  addedge(1, 3);

  if (detect_cycle(1, -1) == true) 
  {
    // If cycle is present
    // Resetting the visited array
    // for simple cycle finding
    Arrays.fill(vis, false);
    find_simple_cycle(a, b);

    // Printing the simple cycle
    System.out.print("A simple cycle: ");

    for (int node : simple_cycle) 
    {
      System.out.print(node + " => ");
    }
    System.out.print(a);
    System.out.print("\n");
  }
  else
  {
    System.out.print("The Graph doesn't " + 
                     "contain a cycle.\n");
  }
}
}

// This code is contributed by shikhasingrajput

```

## C＃

```

// C# implementation to 
// find the simple cycle 
// in the given path
using System;
using System.Collections.Generic;

class GFG{

static readonly int MAXN = 1005;

// Declaration of the 
// Graph
static List<int> []adj = new List<int>[MAXN];

// Declaration of visited 
// array
static bool []vis = new bool[MAXN];

static int a, b;

// Function to add edges
// connecting 'a' and 'b'
// to the graph
static void addedge(int a, int b)
{
  adj[a].Add(b);
  adj[b].Add(a);
}

// Function to detect if the
// graph contains a cycle or not
static bool detect_cycle(int node, 
                         int par)
{

  // Marking the current 
  // node visited
  vis[node] = true;

  // Traversing to the childs
  // of the current node
  // Simple DFS approach
  foreach(int child in adj[node]) 
  {
    if (vis[child] == false) 
    {
      if (detect_cycle(child, 
                       node))
        return true;
    }

    // Checking for a back-edge
    else if (child != par) 
    {

      // A cycle is detected
      // Marking the end-vertices
      // of the cycle
      a = child;
      b = node;
      return true;
    }
  }
  return false;
}

static List<int> simple_cycle = new List<int>();

// Function to get the simple 
// cycle from the end-vertices 
//of the cycle we found from DFS
static void find_simple_cycle(int a, 
                              int b)
{

  // Parent array to get the path
  int []par = new int[MAXN];

  // Queue for BFS
  Queue<int> q = new Queue<int>();

  q.Enqueue(a);
  bool ok = true;

  while (q.Count != 0) 
  {
    int node = q.Peek();
    q.Dequeue();
    vis[node] = true;

    foreach(int child in adj[node]) 
    {
      if (node == a && 
          child == b)

        // Ignoring the direct edge
        // between a and b
        continue;

      if (vis[child] == false) 
      {

        // Updating the parent 
        // array
        par[child] = node;

        if (child == b) 
        {

          // If b is reached,
          // we've found the
          // shortest path from
          // a to b already
          ok = false;
          break;
        }
        q.Enqueue(child);
        vis[child] = true;
      }
    }

    // If required task 
    // is done
    if (ok == false)
      break;
  }

  // Cycle starting from a
  simple_cycle.Add(a);
  int x = b;

  // Until we reach 
  // a again
  while (x != a) 
  {
    simple_cycle.Add(x);
    x = par[x];
  }
}

// Driver Code
public static void Main(String[] args)
{
  for(int i = 0; i < adj.Length; i++)
    adj[i] = new List<int>();

  // Creating the graph
  addedge(1, 2);
  addedge(2, 3);
  addedge(3, 4);
  addedge(4, 1);
  addedge(1, 3);

  if (detect_cycle(1, -1) == true) 
  {

    // If cycle is present
    // Resetting the visited array
    // for simple cycle finding
    for(int i = 0; i < vis.Length; i++)
        vis[i] = false;

    find_simple_cycle(a, b);

    // Printing the simple cycle
    Console.Write("A simple cycle: ");

    foreach(int node in simple_cycle) 
    {
      Console.Write(node + " => ");
    }
    Console.Write(a);
    Console.Write("\n");
  }
  else
  {
    Console.Write("The Graph doesn't " + 
                  "contain a cycle.\n");
  }
}
}

// This code is contributed by gauravrajput1

```

**Output:** 

```
A simple cycle: 1 => 4 => 3 => 1

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。