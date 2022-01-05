# 在从根到 U 的路径的大气距离 1 处，找到包含集合 V 中所有节点的节点 U

> 原文:[https://www . geesforgeks . org/find-node-u-包含所有节点-从集合-v-at-Atmos-distance-1-从根到 u 的路径/](https://www.geeksforgeeks.org/find-node-u-containing-all-nodes-from-a-set-v-at-atmost-distance-1-from-the-path-from-root-to-u/)

给定一个 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，其中 **N** 顶点以 **1** 和为根，一组顶点为**V【】**，任务是打印任何这样的顶点 **U** ，使得从根到 **U** 的路径由从**V【】**到最远距离 **1** 的所有顶点组成。如果没有得到顶点，则打印**“否”**。否则，打印 **U** 的值。

**示例:**

> **输入:** N = 10，边[][] = {{1，2}，{1，3}，{1，4}，{2，5}，{2，6}，{3，7}，{7，8}，{7，9}，{9，10}}，V[] = {4，3，8，9，10}
> 
> [![](img/4a068c70103fe4698896edaf8dbd5045.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200824193453/UntitledDiagram1.png)
> 
> **输出:** 10
> **说明:**从根到节点 10 的路径包含{1，3，7，9，10} 和8 与此路径相距 1 。
> 
> **输入:** N = 10，边[][] = {{1，2}，{1，3}，{1，4}，{2，5}，{2，6}，{3，7}，{7，8}，{7，9}，{9，10}}，V[] = {3，4，2，8}
> 
> [![](img/4a068c70103fe4698896edaf8dbd5045.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200824193453/UntitledDiagram1.png)
> 
> **输出:** 8
> **说明:**从根到节点 8 的路径包含{1，3，7，8}。现在，4 和 2 离这条路径的距离是 1。

**天真方法:**天真的想法是[找到从根 1 到每个节点](https://www.geeksforgeeks.org/sum-numbers-formed-root-leaf-paths/)的所有可能路径，并在从根到所选顶点的路径中选择包含给定集合**的所有所需顶点的路径或与该路径有距离 1 的路径。
***时间复杂度:** O(N！)*
***辅助空间:** O(N <sup>2</sup> )***

**有效方法:**上述方法可以通过预计算每个顶点到根的[距离](https://www.geeksforgeeks.org/find-distance-of-nodes-from-root-in-a-tree-for-multiple-queries/)来优化。这种预先计算有助于发现某个顶点 **P** 是否是给定树中某个其他顶点 **C** 的父节点。以下是步骤:

1.  从根节点 1 开始执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并将每个节点的[访问前和访问后时间存储在给定的树中。](https://www.geeksforgeeks.org/printing-pre-and-post-visited-times-in-dfs-of-a-graph/)
2.  现在，当且仅当 **V** 的前置时间小于或等于 **U** 的前置时间且 **U** 的后置时间大于或等于 **V** 的后置时间时，顶点 **V** 即为顶点 **U** 的父顶点。
3.  可以注意到，给定集合 **V[]** 中最深顶点从根顶点开始的路径是需要的结果。
4.  现在，问题简化为检查给定集合 **V[]** 中每个顶点的父顶点是否是集合 **V[]** 中最深顶点的祖先。
5.  因此，将每个顶点替换为其父顶点(除了**根**)，并通过上述属性检查每个父顶点是否是最深顶点的祖先。
6.  如果条件满足则打印最深顶点，否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// To store the time
int timeT = 0;

// Function to perform DFS
// to store times, distance
// and parent of each node
void dfs(int u, int p, int dis,
         vector<int>& vis,
         vector<int>& distance,
         vector<int>& parent,
         vector<int>& preTime,
         vector<int>& postTime,
         vector<int> Adj[])
{
    // Update the distance of node u
    distance[u] = dis;

    // Update parent of node u
    parent[u] = p;
    vis[u] = 1;

    // Increment time timeT
    timeT++;

    // Discovery time of node u
    preTime[u] = timeT;

    // Traverse the adjacency list
    // of current node and recursively
    // call DFS for each vertex
    for (int i = 0; i < Adj[u].size(); i++) {

        // If current node Adj[u][i]
        // is unvisited
        if (vis[Adj[u][i]] == 0) {

            dfs(Adj[u][i], u, dis + 1,
                vis, distance, parent,
                preTime, postTime, Adj);
        }
    }

    timeT++;

    // Update the finishing time
    postTime[u] = timeT;
}

// Function to add edges between
// nodes u and v
void addEdge(vector<int> Adj[],
             int u, int v)
{
    Adj[u].push_back(v);
    Adj[v].push_back(u);
}

// Function to find the node U
// such that path from root to U
// contains nodes in V[]
void findNodeU(int N, int V,
               int Vertices[],
               int Edges[][2])
{

    // Initialise vis, dis, parent,
    // preTime, and postTime
    vector<int> vis(N + 1, 0);
    vector<int> distance(N + 1, 0);
    vector<int> parent(N + 1, 0);
    vector<int> preTime(N + 1, 0);
    vector<int> postTime(N + 1, 0);

    // Store Adjacency List
    vector<int> Adj[N + 1];

    int u, v;

    // Create adjacency List
    for (int i = 0; i < N - 1; i++) {
        addEdge(Adj, Edges[i][0],
                Edges[i][1]);
    }

    // Perform DFS Traversal
    dfs(1, 0, 0, vis, distance, parent,
        preTime, postTime, Adj);

    int maximumDistance = 0;

    // Stores the distance
    // of deepest vertex 'u'
    maximumDistance = 0;

    // Update the deepest node by
    // traversing the qu[]
    for (int k = 0; k < V; k++) {

        // Find deepest vertex
        if (maximumDistance
            < distance[Vertices[k]]) {

            maximumDistance
                = distance[Vertices[k]];
            u = Vertices[k];
        }

        // Replace each vertex with it's
        // corresponding parent except
        // the root vertex
        if (parent[Vertices[k]] != 0) {
            Vertices[k]
                = parent[Vertices[k]];
        }
    }

    bool ans = true;

    bool flag;

    for (int k = 0; k < V; k++) {

        // Checks if the ancestor
        // with respect to deepest
        // vertex u
        if (preTime[Vertices[k]]
                <= preTime[u]
            && postTime[Vertices[k]]
                   >= postTime[u])
            flag = true;
        else
            flag = false;

        // Update ans
        ans = ans & flag;
    }

    // Print the result
    if (ans)
        cout << u;
    else
        cout << "NO";
}

// Driver Code
int main()
{
    // Total vertices
    int N = 10;

    int V = 5;

    // Given set of vertices
    int Vertices[] = { 4, 3, 8, 9, 10 };

    // Given edges
    int Edges[][2] = { { 1, 2 }, { 1, 3 },
                       { 1, 4 }, { 2, 5 },
                       { 2, 6 }, { 3, 7 },
                       { 7, 8 }, { 7, 9 }, 
                       { 9, 10 } };

    // Function Call
    findNodeU(N, V, Vertices, Edges);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// To store the time
static int timeT = 0;

// Function to perform DFS
// to store times, distance
// and parent of each node
static void dfs(int u, int p, int dis, int vis[],
                int distance[], int parent[],
                int preTime[], int postTime[],
                ArrayList<ArrayList<Integer>> Adj)
{

    // Update the distance of node u
    distance[u] = dis;

    // Update parent of node u
    parent[u] = p;
    vis[u] = 1;

    // Increment time timeT
    timeT++;

    // Discovery time of node u
    preTime[u] = timeT;

    // Traverse the adjacency list
    // of current node and recursively
    // call DFS for each vertex
    for(int i = 0; i < Adj.get(u).size(); i++)
    {

        // If current node Adj[u][i]
        // is unvisited
        if (vis[Adj.get(u).get(i)] == 0)
        {
            dfs(Adj.get(u).get(i), u, dis + 1,
                vis, distance, parent, preTime,
                postTime, Adj);
        }
    }

    timeT++;

    // Update the finishing time
    postTime[u] = timeT;
}

// Function to add edges between
// nodes u and v
static void addEdge(ArrayList<ArrayList<Integer>> Adj,
                    int u, int v)
{
    Adj.get(u).add(v);
    Adj.get(v).add(u);
}

// Function to find the node U
// such that path from root to U
// contains nodes in V[]
static void findNodeU(int N, int V,
                      int Vertices[],
                      int Edges[][])
{

    // Initialise vis, dis, parent,
    // preTime, and postTime
    int vis[] = new int[N + 1];
    int distance[] = new int[N + 1];
    int parent[] = new int[N + 1];
    int preTime[] = new int[N + 1];
    int postTime[] = new int[N + 1];

    // Store Adjacency List
    ArrayList<
    ArrayList<Integer>> Adj = new ArrayList<>();
    for(int i = 0; i < N + 1; i++)
        Adj.add(new ArrayList<Integer>());

    int u = 0, v;

    // Create adjacency List
    for(int i = 0; i < N - 1; i++)
    {
        addEdge(Adj, Edges[i][0], Edges[i][1]);
    }

    // Perform DFS Traversal
    dfs(1, 0, 0, vis, distance,
        parent, preTime, postTime, Adj);

    int maximumDistance = 0;

    // Stores the distance
    // of deepest vertex 'u'
    maximumDistance = 0;

    // Update the deepest node by
    // traversing the qu[]
    for(int k = 0; k < V; k++)
    {

        // Find deepest vertex
        if (maximumDistance <
            distance[Vertices[k]])
        {
            maximumDistance =
            distance[Vertices[k]];
            u = Vertices[k];
        }

        // Replace each vertex with it's
        // corresponding parent except
        // the root vertex
        if (parent[Vertices[k]] != 0)
        {
            Vertices[k] = parent[Vertices[k]];
        }
    }

    boolean ans = true;
    boolean flag;

    for(int k = 0; k < V; k++)
    {

        // Checks if the ancestor
        // with respect to deepest
        // vertex u
        if (preTime[Vertices[k]] <= preTime[u] &&
           postTime[Vertices[k]] >= postTime[u])
            flag = true;
        else
            flag = false;

        // Update ans
        ans = ans & flag;
    }

    // Print the result
    if (ans)
        System.out.println(u);
    else
        System.out.println("NO");
}

// Driver Code
public static void main(String[] args)
{

    // Total vertices
    int N = 10;

    int V = 5;

    // Given set of vertices
    int Vertices[] = { 4, 3, 8, 9, 10 };

    // Given edges
    int Edges[][] = { { 1, 2 }, { 1, 3 },
                      { 1, 4 }, { 2, 5 },
                      { 2, 6 }, { 3, 7 },
                      { 7, 8 }, { 7, 9 },
                      { 9, 10 } };

    // Function call
    findNodeU(N, V, Vertices, Edges);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To store the time
timeT = 0;

# Function to perform DFS
# to store times, distance
# and parent of each node
def dfs(u, p, dis,
          vis,
          distance,
          parent,
          preTime,
          postTime,
          Adj):

    global timeT

    # Update the distance of node u
    distance[u] = dis;

    # Update parent of node u
    parent[u] = p;
    vis[u] = 1;

    # Increment time timeT
    timeT += 1

    # Discovery time of node u
    preTime[u] = timeT;

    # Traverse the adjacency list
    # of current node and recursively
    # call DFS for each vertex
    for i in range(len(Adj[u])):

        # If current node Adj[u][i]
        # is unvisited
        if (vis[Adj[u][i]] == 0):

            dfs(Adj[u][i], u, dis + 1,
                vis, distance, parent,
                preTime, postTime, Adj);

    timeT += 1

    # Update the finishing time
    postTime[u] = timeT;

# Function to add edges between
# nodes u and v
def addEdge(Adj,u, v):

    Adj[u].append(v);
    Adj[v].append(u);

# Function to find the node U
# such that path from root to U
# contains nodes in V[]
def findNodeU(N, V, Vertices, Edges):

    # Initialise vis, dis, parent,
    # preTime, and postTime
    vis = [0 for i in range(N + 1)]
    distance = [0 for i in range(N + 1)]
    parent = [0 for i in range(N + 1)]
    preTime = [0 for i in range(N + 1)]
    postTime = [0 for i in range(N + 1)]

    # Store Adjacency List
    Adj = [[] for i in range(N + 1)]

    u = 0
    v = 0

    # Create adjacency List
    for i in range(N - 1):

        addEdge(Adj, Edges[i][0],
                Edges[i][1]);

    # Perform DFS Traversal
    dfs(1, 0, 0, vis, distance, parent,
        preTime, postTime, Adj);

    maximumDistance = 0;

    # Stores the distance
    # of deepest vertex 'u'
    maximumDistance = 0;

    # Update the deepest node by
    # traversing the qu[]
    for k in range(V):

        # Find deepest vertex
        if (maximumDistance < distance[Vertices[k]]):

            maximumDistance= distance[Vertices[k]];
            u = Vertices[k];

        # Replace each vertex with it's
        # corresponding parent except
        # the root vertex
        if (parent[Vertices[k]] != 0):
            Vertices[k]= parent[Vertices[k]];

    ans = True;

    flag = False

    for k in range(V):

        # Checks if the ancestor
        # with respect to deepest
        # vertex u
        if (preTime[Vertices[k]] <= preTime[u]
                and postTime[Vertices[k]]
                   >= postTime[u]):
            flag = True;
        else:
            flag = False;

        # Update ans
        ans = ans & flag;

    # Print the result
    if (ans):
        print(u)
    else:
        print('No')

# Driver Code
if __name__=='__main__':

    # Total vertices
    N = 10;

    V = 5;

    # Given set of vertices
    Vertices = [ 4, 3, 8, 9, 10 ];

    # Given edges
    Edges = [ [ 1, 2 ], [ 1, 3 ],
                       [ 1, 4 ], [ 2, 5 ],
                       [ 2, 6 ], [ 3, 7 ],
                       [ 7, 8 ], [ 7, 9 ], 
                       [ 9, 10 ] ];

    # Function Call
    findNodeU(N, V, Vertices, Edges);

  # This code is contributed by rutvik_56
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// To store the time
static int timeT = 0;

// Function to perform DFS
// to store times, distance
// and parent of each node
static void dfs(int u, int p, int dis, int []vis,
                int []distance, int []parent,
                int []preTime, int []postTime,
                List<List<int>> Adj)
{
  // Update the distance of node u
  distance[u] = dis;

  // Update parent of node u
  parent[u] = p;
  vis[u] = 1;

  // Increment time timeT
  timeT++;

  // Discovery time of node u
  preTime[u] = timeT;

  // Traverse the adjacency list
  // of current node and recursively
  // call DFS for each vertex
  for(int i = 0; i < Adj[u].Count; i++)
  {
    // If current node Adj[u,i]
    // is unvisited
    if (vis[Adj[u][i]] == 0)
    {
      dfs(Adj[u][i], u, dis + 1,
          vis, distance, parent, preTime,
          postTime, Adj);
    }
  }

  timeT++;

  // Update the finishing time
  postTime[u] = timeT;
}

// Function to add edges between
// nodes u and v
static void addEdge(List<List<int>> Adj,
                    int u, int v)
{
  Adj[u].Add(v);
  Adj[v].Add(u);
}

// Function to find the node U
// such that path from root to U
// contains nodes in V[]
static void findNodeU(int N, int V,
                      int []Vertices,
                      int [,]Edges)
{
  // Initialise vis, dis, parent,
  // preTime, and postTime
  int []vis = new int[N + 1];
  int []distance = new int[N + 1];
  int []parent = new int[N + 1];
  int []preTime = new int[N + 1];
  int []postTime = new int[N + 1];

  // Store Adjacency List
  List<List<int>> Adj = new List<List<int>>();
  for(int i = 0; i < N + 1; i++)
    Adj.Add(new List<int>());

  int u = 0, v;

  // Create adjacency List
  for(int i = 0; i < N - 1; i++)
  {
    addEdge(Adj, Edges[i, 0], Edges[i, 1]);
  }

  // Perform DFS Traversal
  dfs(1, 0, 0, vis, distance,
      parent, preTime, postTime, Adj);

  int maximumDistance = 0;

  // Stores the distance
  // of deepest vertex 'u'
  maximumDistance = 0;

  // Update the deepest node by
  // traversing the qu[]
  for(int k = 0; k < V; k++)
  {
    // Find deepest vertex
    if (maximumDistance <
        distance[Vertices[k]])
    {
      maximumDistance = distance[Vertices[k]];
      u = Vertices[k];
    }

    // Replace each vertex with it's
    // corresponding parent except
    // the root vertex
    if (parent[Vertices[k]] != 0)
    {
      Vertices[k] = parent[Vertices[k]];
    }
  }

  bool ans = true;
  bool flag;

  for(int k = 0; k < V; k++)
  {
    // Checks if the ancestor
    // with respect to deepest
    // vertex u
    if (preTime[Vertices[k]] <= preTime[u] &&
        postTime[Vertices[k]] >= postTime[u])
      flag = true;
    else
      flag = false;

    // Update ans
    ans = ans & flag;
  }

  // Print the result
  if (ans)
    Console.WriteLine(u);
  else
    Console.WriteLine("NO");
}

// Driver Code
public static void Main(String[] args)
{    
  // Total vertices
  int N = 10;

  int V = 5;

  // Given set of vertices
  int []Vertices = {4, 3, 8, 9, 10};

  // Given edges
  int [,]Edges = {{1, 2}, {1, 3},
                  {1, 4}, {2, 5},
                  {2, 6}, {3, 7},
                  {7, 8}, {7, 9},
                  {9, 10}};

  // Function call
  findNodeU(N, V, Vertices, Edges);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // To store the time
    let timeT = 0;

    // Function to perform DFS
    // to store times, distance
    // and parent of each node
    function dfs(u, p, dis, vis, distance, parent,
    preTime, postTime, Adj)
    {
      // Update the distance of node u
      distance[u] = dis;

      // Update parent of node u
      parent[u] = p;
      vis[u] = 1;

      // Increment time timeT
      timeT++;

      // Discovery time of node u
      preTime[u] = timeT;

      // Traverse the adjacency list
      // of current node and recursively
      // call DFS for each vertex
      for(let i = 0; i < Adj[u].length; i++)
      {
        // If current node Adj[u,i]
        // is unvisited
        if (vis[Adj[u][i]] == 0)
        {
          dfs(Adj[u][i], u, dis + 1,
              vis, distance, parent, preTime,
              postTime, Adj);
        }
      }

      timeT++;

      // Update the finishing time
      postTime[u] = timeT;
    }

    // Function to add edges between
    // nodes u and v
    function addEdge(Adj, u, v)
    {
      Adj[u].push(v);
      Adj[v].push(u);
    }

    // Function to find the node U
    // such that path from root to U
    // contains nodes in V[]
    function findNodeU(N, V, Vertices, Edges)
    {
      // Initialise vis, dis, parent,
      // preTime, and postTime
      let vis = new Array(N + 1);
      vis.fill(0);
      let distance = new Array(N + 1);
      distance.fill(0);
      let parent = new Array(N + 1);
      parent.fill(0);
      let preTime = new Array(N + 1);
      preTime.fill(0);
      let postTime = new Array(N + 1);
      postTime.fill(0);

      // Store Adjacency List
      let Adj = [];
      for(let i = 0; i < N + 1; i++)
        Adj.push([]);

      let u = 0, v;

      // Create adjacency List
      for(let i = 0; i < N - 1; i++)
      {
        addEdge(Adj, Edges[i][0], Edges[i][1]);
      }

      // Perform DFS Traversal
      dfs(1, 0, 0, vis, distance,
          parent, preTime, postTime, Adj);

      let maximumDistance = 0;

      // Stores the distance
      // of deepest vertex 'u'
      maximumDistance = 0;

      // Update the deepest node by
      // traversing the qu[]
      for(let k = 0; k < V; k++)
      {
        // Find deepest vertex
        if (maximumDistance < distance[Vertices[k]])
        {
          maximumDistance = distance[Vertices[k]];
          u = Vertices[k];
        }

        // Replace each vertex with it's
        // corresponding parent except
        // the root vertex
        if (parent[Vertices[k]] != 0)
        {
          Vertices[k] = parent[Vertices[k]];
        }
      }

      let ans = true;
      let flag;

      for(let k = 0; k < V; k++)
      {
        // Checks if the ancestor
        // with respect to deepest
        // vertex u
        if (preTime[Vertices[k]] <= preTime[u] &&
            postTime[Vertices[k]] >= postTime[u])
          flag = true;
        else
          flag = false;

        // Update ans
        ans = ans & flag;
      }

      // Print the result
      if (ans)
        document.write(u);
      else
        document.write("NO");
    }

    // Total vertices
    let N = 10;

    let V = 5;

    // Given set of vertices
    let Vertices = [4, 3, 8, 9, 10];

    // Given edges
    let Edges = [[1, 2], [1, 3],
      [1, 4], [2, 5],
      [2, 6], [3, 7],
      [7, 8], [7, 9],
      [9, 10]];

    // Function call
    findNodeU(N, V, Vertices, Edges);

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N + V)，其中 N 是顶点总数，V 是给定集合的大小。*
***辅助空间:** O(5*N)*