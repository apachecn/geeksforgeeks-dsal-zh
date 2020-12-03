# 包含顶点 V 的路径中黑白顶点数量的最大差异

> 原文： [https://www.geeksforgeeks.org/maximum-difference-of-count-of-black-and-white-vertices-in-a-path-containing-vertex-v/](https://www.geeksforgeeks.org/maximum-difference-of-count-of-black-and-white-vertices-in-a-path-containing-vertex-v/)

给定一棵具有`N`个顶点和 **N – 1** 边的树，其中顶点从 **0 到 N – 1** 编号，并且顶点`V`存在于树中。 假定树中的每个顶点具有分配给它的颜色，即**白色或黑色**，并且各个顶点的颜色由数组 **arr []** 表示。 任务是从包含给定顶点`V`的给定树的任何可能的子树中找到白色顶点数量和黑色顶点数量之间的最大差异。

**示例**：

```
Input: V = 0,
arr[] = {'b', 'w', 'w', 'w', 'b',
         'b', 'b', 'b', 'w'}
Tree:
           0 b
         /   \
       /       \
     1 w        2 w
    /          / \
   /          /   \
  5 b      w 3     4 b
  |          |     |
  |          |     |
  7 b      b 6     8 w
Output: 2
Explanation:
We can take the subtree
containing the vertex 0 
which contains vertices
0, 1, 2, 3 such that 
the difference between
the number of white 
and the number of black vertices
is maximum which is equal to 2.

Input:
V = 2,
arr[] = {'b', 'b', 'w', 'b'}
Tree:
        0 b
     /  |  \
    /   |   \
   1    2    3
   b    w     b
Output: 1 

```

**方法**：的想法是使用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)的概念来解决此问题。

*   首先，为颜色阵列和白色创建向量，按 1，对于黑色，按-1。

*   创建一个数组 dp []，以计算包含顶点 V 的某些子树中白色和黑色顶点数目之间的最大可能差。

*   现在，使用[深度遍历树，首先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历并更新 dp []数组中的值。

*   最后，dp []数组中存在的最小值是必需的答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V

#include <bits/stdc++.h>
using namespace std;

// Defining the tree class
class tree {
    vector<int> dp;
    vector<vector<int> > g;
    vector<int> c;

public:
    // Constructor
    tree(int n)
    {
        dp = vector<int>(n);
        g = vector<vector<int> >(n);
        c = vector<int>(n);
    }

    // Function for adding edges
    void addEdge(int u, int v)
    {
        g[u].push_back(v);
        g[v].push_back(u);
    }

    // Function to perform DFS
    // on the given tree
    void dfs(int v, int p = -1)
    {
        dp[v] = c[v];

        for (auto i : g[v]) {
            if (i == p)
                continue;

            dfs(i, v);

            // Returning calculated maximum
            // difference between white
            // and black for current vertex
            dp[v] += max(0, dp[i]);
        }
    }

    // Function that prints the
    // maximum difference between
    // white and black vertices
    void maximumDifference(int v,
                           char color[],
                           int n)
    {
        for (int i = 0; i < n; i++) {

            // Condition for white vertex
            if (color[i] == 'w')
                c[i] = 1;

            // Condition for black vertex
            else
                c[i] = -1;
        }

        // Calling dfs function for vertex v
        dfs(v);

        // Printing maximum difference between
        // white and black vertices
        cout << dp[v] << "\n";
    }
};

// Driver code
int main()
{
    tree t(9);

    t.addEdge(0, 1);
    t.addEdge(0, 2);
    t.addEdge(2, 3);
    t.addEdge(2, 4);
    t.addEdge(1, 5);
    t.addEdge(3, 6);
    t.addEdge(5, 7);
    t.addEdge(4, 8);

    int V = 0;

    char color[] = { 'b', 'w', 'w',
                     'w', 'b', 'b',
                     'b', 'b', 'w' };

    t.maximumDifference(V, color, 9);

    return 0;
}

```

## Java

```java

// Java program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V
import java.util.*;

// Defining the 
// tree class
class GFG{

static int []dp;
static Vector<Integer> []g;
static int[] c;

// Constructor
GFG(int n)
{
  dp = new int[n];
  g =  new Vector[n];

  for (int i = 0; i < g.length; i++)
    g[i] = new Vector<Integer>();

  c = new int[n];
}

// Function for adding edges
void addEdge(int u, int v)
{
  g[u].add(v);
  g[v].add(u);
}

// Function to perform DFS
// on the given tree
static void dfs(int v, int p)
{
  dp[v] = c[v];

  for (int i : g[v]) 
  {
    if (i == p)
      continue;

    dfs(i, v);

    // Returning calculated maximum
    // difference between white
    // and black for current vertex
    dp[v] += Math.max(0, dp[i]);
  }
}

// Function that prints the
// maximum difference between
// white and black vertices
void maximumDifference(int v,
                       char color[],
                       int n)
{
  for (int i = 0; i < n; i++) 
  {
    // Condition for 
    // white vertex
    if (color[i] == 'w')
      c[i] = 1;

    // Condition for 
    // black vertex
    else
      c[i] = -1;
  }

  // Calling dfs function 
  // for vertex v
  dfs(v, -1);

  // Printing maximum difference 
  // between white and black vertices
  System.out.print(dp[v] + "\n");
}

// Driver code
public static void main(String[] args)
{
  GFG t = new GFG(9);

  t.addEdge(0, 1);
  t.addEdge(0, 2);
  t.addEdge(2, 3);
  t.addEdge(2, 4);
  t.addEdge(1, 5);
  t.addEdge(3, 6);
  t.addEdge(5, 7);
  t.addEdge(4, 8);

  int V = 0;

  char color[] = {'b', 'w', 'w',
                  'w', 'b', 'b',
                  'b', 'b', 'w'};
  t.maximumDifference(V, color, 9);
}
}

// This code is contributed by 29AjayKumar

```

## Python

```py

# Python3 program to find maximum 
# difference between count of 
# black and white vertices in 
# a path containing vertex V 

# Function for adding edges
def addEdge(g, u, v):

    g[u].append(v)
    g[v].append(u)

# Function to perform DFS 
# on the given tree
def dfs(v, p, dp, c, g):

    dp[v] = c[v]

    for i in g[v]:
        if i == p:
            continue

        dfs(i, v, dp, c, g)

        # Returning calculated maximum 
        # difference between white 
        # and black for current vertex 
        dp[v] += max(0, dp[i])

# Function that prints the 
# maximum difference between 
# white and black vertices 
def maximumDifference(v, color, n, dp, c, g):

    for i in range(n):

        # Condition for white vertex 
        if(color[i] == 'w'):
            c[i] = 1

        # Condition for black vertex
        else:
            c[i] = -1

    # Calling dfs function for vertex v
    dfs(v, -1, dp, c, g)

    # Printing maximum difference between 
    # white and black vertices
    print(dp[v])

# Driver code
n = 9
g = {}
dp = [0] * n
c = [0] * n

for i in range(0, n + 1):
    g[i] = []

addEdge(g, 0, 1)
addEdge(g, 0, 2)
addEdge(g, 2, 2)
addEdge(g, 2, 4)
addEdge(g, 1, 5)
addEdge(g, 3, 6)
addEdge(g, 5, 7)
addEdge(g, 4, 8)

V = 0

color = [ 'b', 'w', 'w', 
          'w', 'b', 'b', 
          'b', 'b', 'w' ]

maximumDifference(V, color, 9, dp, c, g)

# This code is contributed by avanitrachhadiya2155

```

## C#

```cs

// C# program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V
using System;
using System.Collections.Generic;

// Defining the 
// tree class
class GFG{

static int []dp;
static List<int> []g;
static int[] c;

// Constructor
GFG(int n)
{
  dp = new int[n];
  g = new List<int>[n];

  for (int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  c = new int[n];
}

// Function for adding edges
void addEdge(int u, int v)
{
  g[u].Add(v);
  g[v].Add(u);
}

// Function to perform DFS
// on the given tree
static void dfs(int v, int p)
{
  dp[v] = c[v];

  foreach (int i in g[v]) 
  {
    if (i == p)
      continue;

    dfs(i, v);

    // Returning calculated maximum
    // difference between white
    // and black for current vertex
    dp[v] += Math.Max(0, dp[i]);
  }
}

// Function that prints the
// maximum difference between
// white and black vertices
void maximumDifference(int v,
                       char []color,
                       int n)
{
  for (int i = 0; i < n; i++) 
  {
    // Condition for 
    // white vertex
    if (color[i] == 'w')
      c[i] = 1;

    // Condition for 
    // black vertex
    else
      c[i] = -1;
  }

  // Calling dfs function 
  // for vertex v
  dfs(v, -1);

  // Printing maximum difference 
  // between white and black vertices
  Console.Write(dp[v] + "\n");
}

// Driver code
public static void Main(String[] args)
{
  GFG t = new GFG(9);

  t.addEdge(0, 1);
  t.addEdge(0, 2);
  t.addEdge(2, 3);
  t.addEdge(2, 4);
  t.addEdge(1, 5);
  t.addEdge(3, 6);
  t.addEdge(5, 7);
  t.addEdge(4, 8);

  int V = 0;

  char []color = {'b', 'w', 'w',
                  'w', 'b', 'b',
                  'b', 'b', 'w'};
  t.maximumDifference(V, color, 9);
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
2

```

**时间复杂度**：*`O(N)`*，其中 N 是树中的顶点数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。